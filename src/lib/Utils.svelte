<script context="module">
    export const fullURL =
        location.protocol +
        "//" +
        location.hostname +
        (location.port ? ":" + location.port : "");

    export const getHost = () => {
        let preConfig = getParams("config");
        if (preConfig && preConfig !== "")
            preConfig = JSON.parse(atob(preConfig));

        console.log("host", getParams("host"));
        const HOST = preConfig
            ? `${preConfig.address}:${preConfig.port}`
            : process.env.HOST || getParams("host") || fullURL;
        return HOST;
    };

    export const loadExercises = function () {
        return new Promise((resolve, reject) =>
            fetch(getHost() + "/exercise")
                .then((resp) => {
                    if (resp.ok) return resp.json();
                    else
                        throw new Error(
                            "There seems to be an error connecting with the server"
                        );
                })
                .then((details) => {
                    const exercises = Array.isArray(details)
                        ? details
                        : details.exercises;

                    if (Array.isArray(exercises)) resolve(exercises);
                    else
                        throw new Error(
                            "No exercises where found on the currect directory"
                        );
                })
                .catch((error) => {
                    reject(error);
                })
        );
    };

    export const loadSingleExercise = function (exerciseSlug) {
        return new Promise((resolve, reject) =>
            fetch(getHost() + "/exercise/" + exerciseSlug)
                .then((resp) => {
                    if (resp.status >= 200 && resp.status < 400)
                        return resp.json();
                    else if (resp.status === 400) {
                        resp.json()
                            .then((error) => {
                                if (error.type == "not-found-error") {
                                    const _savedSlug =
                                        sessionStorage.getItem("exercise-slug");
                                    if (_savedSlug) {
                                        sessionStorage.clear();
                                        window.location.href = "/";
                                    }
                                }
                                throw new Error(error.message);
                            })
                            .catch((error) => {
                                throw new Error(
                                    "There seems to be an error connecting with the server"
                                );
                            });
                    } else
                        throw new Error(
                            "There seems to be an error connecting with the server"
                        );
                })
                .then((exercise) => {
                    if (exercise && Array.isArray(exercise.files))
                        resolve(exercise);
                    else {
                        throw new Error(
                            "Invalid array of files found for the exercise",
                            exercise
                        );
                    }
                })
                .catch((error) => {
                    reject(error);
                })
        );
    };

    export const loadFile = function (exerciseSlug, file) {
        return new Promise((resolve, reject) =>
            fetch(
                getHost() +
                    "/exercise/" +
                    exerciseSlug +
                    "/file/" +
                    (file.name || file)
            )
                .then((resp) => {
                    resolve(resp.text());
                })
                .catch((error) => reject(error))
        );
    };

    export const loadReadme = function (exerciseSlug, language = "us") {
        return new Promise((resolve, reject) =>
            fetch(
                getHost() +
                    "/exercise/" +
                    exerciseSlug +
                    "/readme?lang=" +
                    language
            )
                .then((resp) => {
                    if (resp.status == 200) {
                        resp.text().then((originalText) => {
                            try {
                                const data = JSON.parse(originalText);
                                resolve(data);
                            } catch (e) {
                                console.log("Error", originalText);
                                resolve(originalText);
                            }
                        });
                    } else reject();
                })
                .catch((error) => reject(error))
        );
    };

    export const saveFile = function (exerciseSlug, file, content) {
        return new Promise((resolve, reject) =>
            fetch(
                getHost() +
                    "/exercise/" +
                    exerciseSlug +
                    "/file/" +
                    (file.name || file),
                {
                    method: "PUT",
                    body: content,
                }
            )
                .then((resp) => resolve(resp.text()))
                .catch((error) => reject(error))
        );
    };

    export const LearnPackError = function (message) {
        this.details = message;
    };

    export function getParams(opts) {
        if (!Array.isArray(opts)) opts = [opts];
        const urlParams = new URLSearchParams(window.location.search);
        let obj = {};
        opts.forEach((name) => (obj[name] = urlParams.get(name)));
        return opts.length == 1 ? obj[opts[0]] : obj;
    }

    export function deepMerge(...sources) {
        let acc = {};
        for (const source of sources) {
            if (Array.isArray(source)) {
                if (!Array.isArray(acc)) {
                    acc = [];
                }
                acc = [...source];
            } else if (source instanceof Object) {
                for (let [key, value] of Object.entries(source)) {
                    if (value instanceof Object && key in acc) {
                        value = deepMerge(acc[key], value);
                    }
                    if (value != undefined) {
                        acc = Object.assign(acc, { [key]: value });
                    }
                }
            }
        }
        return acc;
    }
</script>
