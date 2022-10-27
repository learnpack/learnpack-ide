<script>
import { validate_dynamic_element } from "svelte/internal";
import {showTheExercise} from "./Utils.svelte"
import {state} from "./Store.svelte"

export let value;

// function itemClicked() {
//     let navbarItem = document.getElementById("navbar-item");

//     if(navbarItem.style.display === "block"){

//     }
// }



</script>

<div id="navbar-item" on:click={() => {
    state.set({...$state,currentSlug:value})
    showTheExercise(value)
    console.log(value)
}}>
    {value}
</div>

<span class="line"></span>



<style>

.line {
  display: inline-block;
  width:60%;
  border-top: 1px solid #0097CD;
}
    #navbar-item {
        color: black;
        padding: 14px 16px;
        font-size: 17px;
        display: block;
        font-weight: bold;
    }

    #navbar-item:hover {
        background-color: #ddd;
        color: black;
    }
</style>
