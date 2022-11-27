<script>
  import { Socket } from "./Socket.svelte";
  import {
    getHost,
    loadConfig,
    showTheExercise,
    getIndex,
    hideElement,
    showElement
  } from "./Utils.svelte";
  import { onMount } from "svelte";
  import NavbarItem from "./NavbarItem.svelte";
  import { state } from "./Store.svelte";
  import { Router, Route, Link } from "svelte-navigator";
  import HelpPage from './HelpPage.svelte';
  import Navbar from "./Navbar.svelte";

  let exercises = [];



  onMount(async () => {
    $state.config = await loadConfig();
    $state.exercises = $state.config.exercises;
    console.log($state.exercises)
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

<Router>
	  <Route path="/">
		<Navbar {exercises}/>
	  </Route>
	  <Route path="/help">
		<HelpPage/>
	  </Route>
  </Router>