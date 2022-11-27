<script>
    import { onMount, validate_dynamic_element } from "svelte/internal";
    import {state} from "./Store.svelte"
    
    export let value;

        onMount(async ({slug}) => {
        try {
            const res = await fetch(`https://learnpack.herokuapp.com/v1/support/question/${slug}`);
            console.log(res)
            $state.currentQuestionSlug = await res.json();
            console.log($state.currentQuestionSlug)
        } catch(err){
            console.log("There was an error loading the questions", err)
        }  
	});


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
    