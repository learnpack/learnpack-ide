<script>
import { validate_dynamic_element } from "svelte/internal";
import {showTheExercise} from "./Utils.svelte"
import {state} from "./Store.svelte"

export let value;

// function hideNavbar() {
//     let test = document.getElementById("navbar");
//     test.style.display = "none" 
     
//   }



</script>

<div id="navbar-item" on:click={() => {
    state.set({...$state,currentSlug:value})
    showTheExercise(value)
    console.log(value)
}}>
    {value}
</div>



<style>
    #navbar-item {
        color: white;
        padding: 14px 16px;
        text-decoration: none;
        font-size: 17px;
        display: block;
    }

    #navbar-item:hover {
        background-color: #ddd;
        color: black;
    }
</style>
