<script>
  import { Socket } from "./components/Socket.svelte";
  import {
    getHost,
    loadConfig,
    showTheExercise,
    getIndex,
    hideElement,
    showElement
  } from "./components/Utils.svelte";
  import { onMount } from "svelte";
  import Navbar from "./components/Navbar.svelte";
  import NavbarItem from "./components/NavbarItem.svelte";
  import { state } from "./components/Store.svelte";

  let exercises = [];


  onMount(async () => {
    $state.config = await loadConfig();
    $state.exercises = $state.config.exercises;
    exercises = $state.exercises.map((exercise) => {
      return { value: exercise.slug, component: NavbarItem };
    });
    console.log(exercises);
    Socket.start($state.host, () => {
      // <-- On Disconnect Callback!
      const consoleStatus = {
        code: "internal-error",
        message: "It seems that the exercise engine is disconnected",
        solution: "Run on your terminal the command: $ learnpack start",
      };
      return consoleStatus;
    });

    $state.compilerSocket = Socket.createScope("compiler");

    $state.compilerSocket.onStatus("compiler-success", (data) => {
      console.log(data);
    });
  });


  $: {
    showTheExercise($state.currentSlug);
    const i = getIndex($state) + 1;
    let rightArrow = document.getElementById("right-container")
    let leftArrow = document.getElementById("left-container")
    if(i === $state.exercises.length) hideElement(rightArrow)
    else showElement(rightArrow)
    if(i === 1) hideElement(leftArrow)
    else showElement(leftArrow)
  }



 


</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->
<main>
  <Navbar {exercises} />
  <div id="theBody" />
</main>

<style>
  body {
    margin: 0;
  }
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }
</style>
