<script>
    import { Link } from "svelte-navigator";
import { onMount, validate_dynamic_element } from "svelte/internal";
    import {state} from "./Store.svelte"
    
    export let value;

 

    //     onMount(async () => {
    //     try {
    //     //     for (let i = 0; i < $state.questions.length; i++) {
    //     // if ($state.questions[i].title === $state.currentQuestionSlug) return i;
    //     // }
    //         const res = await fetch(`https://learnpack.herokuapp.com/v1/support/question/`);
    //         q = await res.json();
    //     } catch(err){
    //         console.log("There was an error loading the questions", err)
    //     }  
	// });

$:{
        console.log($state.currentQuestionSlug)
    }

    
    </script>
    
    <div id="navbar-item" on:click={() => {
        state.set({... $state,currentQuestionSlug:value})
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
    