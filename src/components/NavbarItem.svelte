<script>
import { validate_dynamic_element } from "svelte/internal";
import {loadReadme} from "./Utils.svelte"

export let value;


async function showTheExercise(){
    let readMe = await loadReadme(value)
    console.log(readMe)
    document.getElementById("theBody").innerHTML = readMe.body;
    }

function hideNavbar() {
    let test = document.getElementById("navbar");
    test.style.display = "none" 
     
  }


</script>

<div id="navbar-item" on:click={() => {
    showTheExercise()
    hideNavbar()
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
