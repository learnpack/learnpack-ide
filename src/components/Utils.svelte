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
        const HOST = preConfig
            ? `${preConfig.address}:${preConfig.port}`
            : getParams("host") || fullURL;
        return HOST;
    };
    export async function showTheExercise(slug){
    let readMe = await loadReadme(slug)
    console.log(readMe)
    document.getElementById("theBody").innerHTML = readMe.body;
    }
    

    export const loadConfig = async function(){
        let response = await fetch(getHost() + '/config')
        let config = await response.json();
        return config;
    } 

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

    export function hideElement(element){
    if(element) element.style.visibility = "hidden"
    else console.log(`The element (${element}) does not exist`)
  }

  export function showElement(element){
    if(element) element.style.visibility = "visible"
    else console.log(`The element (${element}) does not exist`)
  }

  export function getIndex(state) {
    for (let i = 0; i < state.exercises.length; i++) {
      if (state.exercises[i].slug === state.currentSlug) return i;
    }
  }

</script>
