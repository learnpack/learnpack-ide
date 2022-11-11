<script context="module">
import { writable } from 'svelte/store';
import {getHost, loadReadme} from "./Utils.svelte"

export const state = writable(
    {
    config: {},
    exercises: [],
    host: getHost(),
    load: loadReadme(),
    questions: [],
    currentQuestionSlug: "",
    currentSlug: "",
    compilerSocket: null,
    language: "us",
}
)

</script>