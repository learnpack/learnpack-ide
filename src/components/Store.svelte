<script context="module">
import { writable } from 'svelte/store';
import {getHost, loadReadme} from "./Utils.svelte"

export const state = writable(
    {
    config: {},
    exercises: [],
    host: getHost(),
    load: loadReadme(),
    possibleActions: [],
    tutorial: null,
    intro: null,
    introOpen: true,
    questions: [],
    currentQuestionSlug: null,
    currentSlug: "",
    compilerSocket: null,
    language: "us",
}
)

</script>