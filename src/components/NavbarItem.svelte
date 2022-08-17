<script>
import { validate_dynamic_element } from "svelte/internal";

export let value;

export function showTheExercise(){
    let theItem = document.getElementById("theBody").innerHTML = value;
    console.log(theItem)

    }

export function hideNavbar() {
    let test = document.getElementById("nav");
    test.style.display = "none" 
     
  }


</script>

<div id="navbar-item" on:click={showTheExercise}>
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
