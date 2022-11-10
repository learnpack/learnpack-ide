<script>

//We are going to add an on mount to get the questions from the FAQ API

//We need to create the modal that displays the questions from the FAQ API

//When we click a question from the modal, it needs to display the question page on the entire screen with the question's body

//The page that displays the body of the question needs to have a back button to return to the main menu of the questions

//When we click the X or outside of the modal, we need to close out the modal and show the exerciseList

import { onMount } from "svelte";
import { state } from "./Store.svelte";
import loading from "public/loading.gif"

let loadingImage = {loading}


onMount(async () => {
		const res = await fetch('https://learnpack.herokuapp.com/v1/support/question');
        if(res.status === 200){
            $state.questions = await res.json();
            return $state.questions
        } else{
            return loadingImage;
        }    
        //create a validation just in case $state.questions doesn't exist. If it doesn't exist include a loading icon
	});


</script>

<div id="question-item">

</div>


<style>


</style>
