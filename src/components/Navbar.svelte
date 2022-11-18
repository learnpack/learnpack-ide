<script>
import { loop_guard, validate_component } from "svelte/internal";
import {Link, Route, Router } from "/Users/karlacuevas/Documents/learnpack-ide/node_modules/svelte-navigator"
// import Router, {location, link} from 'svelte-spa-router';
import HelpPage from "./HelpPage.svelte";
import {
    getHost,
    loadConfig,
    showTheExercise,
    hideElement,
    showElement,
    getIndex
  } from "../components/Utils.svelte";
  import { state } from "../components/Store.svelte";



  export let exercises;

  let routes = {
    "help": HelpPage
  }



  const actions = [
    { slug: 'build', label: 'Build', icon: "https://icongr.am/feather/play-circle.svg?size=27&color=6b6b6b" },
    { slug: 'run', label: 'Compile', icon: 'fas fa-play' },
    { slug: 'preview', label: 'Preview', icon: "https://icongr.am/entypo/youtube.svg?size=27&color=6b6b6b" },
    { slug: 'pretty', label: 'Pretty', icon: 'fas fa-paint-brush' },
    { slug: 'test', label: 'Test', icon: "https://icongr.am/clarity/checkbox-list.svg?size=27&color=6b6b6b" },
    { slug: 'reset', label: 'Reset', icon: "https://icongr.am/clarity/refresh.svg?size=27&color=6b6b6b", confirm: true, refresh: true }
];

  function showExercises() {
    let navbar = document.getElementById("navbar");
    let nav = document.getElementById("nav")
    let list = document.getElementById("exerciseList")
    if (navbar.style.display === "block") {
      navbar.style.display = "none";
      nav.style.height = "85px";
    } else {
      navbar.style.display = "block";
      list.style.backgroundColor = "#C7F3FD";
      list.style.paddingLeft = "50px"
      list.style.paddingTop = "50px"
    }


  }
  

  function hide(){
    let theContainer = document.getElementById("question")
    let navbar = document.getElementById("navbar");

    theContainer.style.display= "none"
  
  }
  

  export function next() {
    const i = getIndex($state) + 1;
    if ($state.exercises[i].slug) {
      state.set({ ...$state, currentSlug: $state.exercises[i].slug });
    }

  }

  export function previous() {
    const i = getIndex($state) - 1;
    if ($state.exercises[i].slug) {
      state.set({ ...$state, currentSlug: $state.exercises[i].slug });
    }
   
  }


</script>
<div id="nav">
  <input type="checkbox" id="nav-check">
  <div class="nav-header">
    <div class="nav-title">
      <div id="menu-background">
      <img
            on:click={showExercises}
            alt="menu"
            src="https://icongr.am/fontawesome/align-justify.svg?size=30&color=ffffff"
          />
    </div>
  </div>
  <div class="nav-title" id="dropdown">
    <button class="dropbtn">Eng</button>
    <div class="dropdown-content">
      <a href="">Esp</a>
      <a href="">Ita</a>
    </div>
  </div>
    <div class="nav-title">
      <img
      id="theBug"
      alt="bug"
      src="https://icongr.am/fontawesome/bug.svg?size=30&color=6b6b6b"
    />
    </div>
    <div class="nav-title">
      <img
          id="theQuestion"
          alt="question"
          src="https://icongr.am/fontawesome/question-circle-o.svg?size=30&color=6b6b6b"
        />
    </div>
  </div>
  <div class="nav-links">
        <div class="container" id="left-container" on:click={previous}>
          <div class="image">
            <img alt="arrow" src="https://icongr.am/feather/arrow-left.svg?size=40&color=currentColor">
          </div>
          <div class="text" id="left-text">
            <p>Previous</p>
          </div>
        </div>
   

      <div class="container"id="right-container" on:click={next}>
        <div class="text" id="right-text">
          <p>Next</p>
        </div>
        <div class="image">
          <img alt="arrow" src="https://icongr.am/feather/arrow-right.svg?size=40&color=currentColor">
        </div>
      </div>
  
      
</div>
</div>

<div class="available-actions-section">
  <div class="actions">
    <img class="active-actions" src="https://icongr.am/feather/play-circle.svg?size=27&color=6b6b6b"/>
    <img class="active-actions" src="https://icongr.am/clarity/checkbox-list.svg?size=27&color=6b6b6b"/>
    <img class="active-actions" src="https://icongr.am/clarity/refresh.svg?size=27&color=6b6b6b"/>
    <img class="active-actions" src="https://icongr.am/entypo/youtube.svg?size=27&color=6b6b6b"/>
  </div>

  <div class="ready-wrapper">
  <div  id= "ready" >
    <p id="ready-text">Ready...</p>
  </div>
  </div>
</div>

<div id="navbar">
<div id="exerciseList" >

  <!-- <Router>
    <Link to="help" on:click={hide}>
      <div class="container-question" id="question">
        <div class="image">
          <img
                alt="question"
                src="https://icongr.am/fontawesome/question-circle-o.svg?size=30&color=000000"
              />
        </div>
        <div class="text" id="help-text">
          <p>Help</p>
        </div>
      </div>
    </Link>

<Route path="help" primary={true}>
  <HelpPage/>
</Route>

</Router> -->

  {#each exercises as exercise}
  <svelte:component this={exercise.component} {...exercise}/>
{/each}
</div>
</div>


<Router>
    <Link to="help" on:click={hide}>
      <div class="container-question" id="question">
        <div class="image">
          <img
                alt="question"
                src="https://icongr.am/fontawesome/question-circle-o.svg?size=30&color=000000"
              />
        </div>
        <div class="text" id="help-text">
          <p>Help</p>
        </div>
      </div>
    </Link>

<Route path="help" primary={true}>
  <HelpPage/>
</Route>

</Router>


<!-- 
  <a href="/#/help">
    <div class="container-question" id="question">
      <div class="image">
        <img
              alt="question"
              src="https://icongr.am/fontawesome/question-circle-o.svg?size=30&color=000000"
            />
      </div>
      <div class="text" id="help-text">
        <p>Help</p>
      </div>
    </div>
  </a>

  <Router routes={{
    '/help': HelpPage,
  }} />
  
  <hr>
  {$location} -->









<style>

#help-text{
  padding-right: 20px;
  padding-left: 20px;
  font-size: 18px;
  font-weight: bold;
}

.container-question{
  display: flex;
  align-items: center;
  justify-content: center;
  width: 5rem;
  height: 3rem;
}


#exerciseList{
  background-color: #C7F3FD;
  padding-left:50px;
}

  .container {
  display: flex;
  align-items: center;
  justify-content: center;
  border-style: solid;
  width: 10rem;
  height: 3rem;
  border-radius: 3px;
  border-color: #A4A4A4;
}


#left-container{
  margin-right: 18px;
}

.image {
  flex-basis: 5%
}

#left-text, #right-text{
  padding-right: 20px;
  padding-left: 20px;
  font-size: 18px;
}

.dropbtn {
  color: #606060;
  font-size: 16px;
  border: none;
  cursor: pointer;
  border-radius: 3px;
  width: 50px;
  height: 40px;
  border-style: solid;
}

#dropdown {
  position: relative;
  display: inline-block;
}


.dropdown-content {
  display: none;
  position: absolute;
  background-color: #606060;
  min-width: 50px;
  z-index: 1;
}


.dropdown-content a {
  color: #606060;
  text-decoration: none;
  background-color: #C4C4C4;
  display: block;
  text-align: center;
  padding: 5px 0px 5px 0px;
}

.dropdown-content a:hover {
  background-color: #606060;
  color: white;
}

#dropdown:hover .dropdown-content {
  display: block;
}


#dropdown:hover .dropbtn {
  background-color: #606060;
  color: white;
}


  * {
  box-sizing: border-box;
}

:global(body){
  margin: 0;
}

#nav > .nav-header{
  background-color: white;
  margin-left: 18px;
}


#nav {
  height: 85px;
  width: 100%;
  background-color: #F5F5F5;
  padding: 12px 12px 12px 12px;
}

.available-actions-section{
  background-color: #C7F3FD;
  padding: 12px 12px 12px 40px;
  display: flex;
  height: 85px;
}

.active-actions{
  margin-top: 0;
  padding: 8px;;
}

.actions{
  border: solid #0097CD;
  padding: 12px 12px 12px 12px;
  border-radius: 5px;
}

.ready-wrapper{
  background-color: #0097CD;
  margin: auto 20px;
  border-radius: 5px;
  width: 80px;
  text-align: center;
;
}

#ready{
  color: white;
  padding: 5px;
}

#ready-text{
  margin: 0;
}

#nav > .nav-header > .nav-title {
  float: left;
  font-size: 15px;
  color: #fff;
  padding: 10px 10px 10px 10px;
}

#menu-background{
  background-color: #0097CD;
  width: 50px;
  height: 40px;
  text-align: center;
  padding: 6px;
  border-radius: 3px;
}

#theBug, #theQuestion{
  padding-top: 6px;
}


#nav > .nav-links {
  float: right;
  font-size: 18px;
  display: flex;
  justify-content: center;
  margin-right: 40px;
  padding-top: 6px;
}


#nav > #nav-check {
  display: none;
}
#navbar {
    display: none;
  }


@media (max-width:600px) {
  #nav > .nav-links {
    position: absolute;
    display: block;
    width: 100%;
    background-color: #333;
    height: 0px;
    transition: all 0.3s ease-in;
    overflow-y: hidden;
    top: 50px;
    left: 0px;
  }
  #nav > #nav-check:not(:checked) ~ .nav-links {
    height: 0px;
  }
  #nav > #nav-check:checked ~ .nav-links {
    height: calc(100vh - 50px);
    overflow-y: auto;
  }
}

</style>
