<script>
 import { onMount } from "svelte";
//  import { state } from "src/components/Store.svelte";

//We are going to add an on mount to get the questions from the FAQ API

//We need to create the modal that displays the questions from the FAQ API

//When we click a question from the modal, it needs to display the question page on the entire screen with the question's body

//The page that displays the body of the question needs to have a back button to return to the main menu of the questions

//When we click the X or outside of the modal, we need to close out the modal and show the exerciseList


let questions = [];

onMount(async () => {
		const res = await fetch('https://learnpack.herokuapp.com/v1/support/question');
        console.log(res)
		questions = await res.json();
        console.log(questions)
	});


</script>

<div>
    <h1>{questions}</h1>
</div>


