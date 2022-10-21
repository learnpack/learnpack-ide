<script>
import { loop_guard, validate_component } from "svelte/internal";
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

  function showExercises() {
    let navbar = document.getElementById("navbar");
    let nav = document.getElementById("nav")
    let list = document.getElementById("exerciseList")
    if (navbar.style.display === "block") {
      navbar.style.display = "none";
      nav.style.height = "50px";
    } else {
      navbar.style.display = "block";
      nav.style.height = "auto";
      list.style.backgroundColor = "#C7F3FD";
      list.style.paddingLeft = "50px"
      list.style.paddingTop = "100px"
    }
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

<!-- <div>
  <nav id="nav">
    <div class="row">
      <div>
      <div class="background-menu">
      <div class="menu">
        <img
            on:click={showExercises}
            alt="menu"
            src="https://icongr.am/fontawesome/align-justify.svg?size=25&color=ffffff"
          />
      </div>
    </div>
    </div>
      <div class="icon">
        <div class="languages">
          <p>Eng</p>
        </div>
      </div> 
      <div class="icon">
        <img
          alt="bug"
          src="https://icongr.am/fontawesome/bug.svg?size=30&color=6b6b6b"
        />
      </div>
      <div class="icon">
        <img
          alt="question"
          src="https://icongr.am/fontawesome/question-circle-o.svg?size=30&color=6b6b6b"
        />
      </div>
      <div class="icon" id="leftArrow">
        <div
        on:click={previous}
        >
        <p>Previous</p>
        </div>
      </div>
      <div class="icon" id="rightArrow">
       
        <div 
        on:click={next}
        >
        <p>Next</p>
        </div>
        </div>

    <div id="navbar" >
      {#each exercises as exercise}
        <svelte:component this={exercise.component} {...exercise}/>
      {/each}
    </div>

    </div>
  </nav>


</div> -->



<!-- sample nav -->

<div id="nav">
  <input type="checkbox" id="nav-check">
  <div class="nav-header">
    <div class="nav-title">
      <div>
      <img
            on:click={showExercises}
            alt="menu"
            src="https://icongr.am/fontawesome/align-justify.svg?size=25&color=ffffff"
          />
    </div>
  </div>
    <!-- <div class="nav-title" id="theLanguage">
      <p>Eng</p>
    </div> -->
    <div class="nav-title" id="theBug">
      <img
      alt="bug"
      src="https://icongr.am/fontawesome/bug.svg?size=30&color=6b6b6b"
    />
    </div>
    <div class="nav-title" id="theQuestion">
      <img
          alt="question"
          src="https://icongr.am/fontawesome/question-circle-o.svg?size=30&color=6b6b6b"
        />
    </div>
  </div>
  <div class="nav-btn">
    <label for="nav-check">
      <span></span>
      <span></span>
      <span></span>
    </label>
  </div>
  
  <div class="nav-links">
    <div class="right-links" id="leftArrow" on:click={previous}>Previous</div>
    <div class="right-links" id="rightArrow" on:click={next}>Next</div>
  </div>
  <div id="navbar" >
    <div id="exerciseList">
      <div class="theQuestion">
        <div class="test">
        <img
            alt="question"
            src="https://icongr.am/fontawesome/question-circle-o.svg?size=30&color=6b6b6b"
          />
        </div>
          <div class="test"><p>Help</p></div>
      </div>
      {#each exercises as exercise}
      <svelte:component this={exercise.component} {...exercise}/>
    {/each}
  </div>
  </div>
</div>


<style>

  /* Sample nav style */

  * {
  box-sizing: border-box;
}


#nav {
  height: 50px;
  width: 100%;
  background-color: #F5F5F5;
  position: relative;
}


#nav > .nav-header {
  display: inline;
}

#nav > .nav-header > .nav-title {
  display: inline-block;
  float: left;
  font-size: 0px;
  color: #fff;
  padding: 10px 10px 10px 10px;
}

#nav > .nav-btn {
  display: none;
}

#nav > .nav-links {
  display: inline;
  float: right;
  font-size: 18px;
}

#nav > .nav-links > .right-links {
  display: inline-block;
  padding: 13px 10px 13px 10px;
  text-decoration: none;
  color: 6b6b6b;
}

#nav > .nav-links > .right-links:hover {
  background-color: rgba(0, 0, 0, 0.3);
}

.theQuestion{
  display: flex;
}

#nav > #nav-check {
  display: none;
}
#navbar {
    display: none;
  }
@media (max-width:600px) {
  #nav > .nav-btn {
    display: inline-block;
    position: absolute;
    right: 0px;
    top: 0px;
  }
  #nav > .nav-btn > label {
    display: inline-block;
    width: 50px;
    height: 50px;
    padding: 13px;
  }
  #nav > .nav-btn > label:hover,#nav  #nav-check:checked ~ .nav-btn > label {
    background-color: rgba(0, 0, 0, 0.3);
  }
  #nav > .nav-btn > label > span {
    display: block;
    width: 25px;
    height: 10px;
    border-top: 2px solid #eee;
  }
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
  #nav > .nav-links > .right-links {
    display: block;
    width: 100%;
  }
  #nav > #nav-check:not(:checked) ~ .nav-links {
    height: 0px;
  }
  #nav > #nav-check:checked ~ .nav-links {
    height: calc(100vh - 50px);
    overflow-y: auto;
  }
}
/* 
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Poppins", sans-serif;

  }
  .languages{
    border-color: #6b6b6b;
    border-style: solid;
    border-radius: 3px;
  }

  #rightArrow{
    position: absolute;
    right: 0px;
  }

  #leftArrow{
    position: absolute;
    right: 115px;
  }

  .row {
    display: flex;
    width: 100%;
    position: relative;
  }

  .row .icon {
    width: 12%;
    padding: 2.5%;
  
  }

  .row .icon img{
    cursor: pointer;
  }

  .background-menu{
    display: flex;
    justify-content: center;
    width: 3rem;
    height: 3rem;
    background: #0097CD;
    border-radius: 3px;
  }

  nav {
    text-align: center;
    height: 80px;
    width: 100%;
    background: #F5F5F5;
    align-items: center;
    justify-content: space-between;
    padding: 0 50px 0 100px;
    flex-wrap: wrap;
  }
  
  nav .menu {
    color: #fff;
    font-weight: 600;
    padding-left: 5%;
    padding: 2.5%;
    margin: auto;
  }
  nav ul {
    display: flex;
    flex-wrap: wrap;
    list-style: none;
  }
  nav ul li {
    margin: 0 5px;
  }
  nav ul li a {
    color: #f2f2f2;
    text-decoration: none;
    font-size: 18px;
    font-weight: 500;
    padding: 8px 15px;
    border-radius: 5px;
    letter-spacing: 1px;
    transition: all 0.3s ease;
  }
  nav ul li a.active,
  nav ul li a:hover {
    color: black;
  }

  @media (max-width: 1000px) {
    nav {
      padding: 0 40px 0 50px;
    }
  }
  @media (max-width: 920px) {
    nav .menu-btn i {
      display: block;
    }

    nav ul {
      position: fixed;
      top: 80px;
      left: -100%;
      background: #111;
      height: 100vh;
      width: 100%;
      text-align: center;
      display: block;
      transition: all 0.3s ease;
    }
    nav ul li {
      width: 100%;
      margin: 40px 0;
    }
    nav ul li a {
      width: 100%;
      margin-left: -100%;
      display: block;
      font-size: 20px;
      transition: 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
    }
    #click:checked ~ ul li a {
      margin-left: 0px;
    }
    nav ul li a.active,
    nav ul li a:hover {
      background: none;
      color: cyan;
    }
  }

  #navbar {
    display: none;
  } */




  
</style>
