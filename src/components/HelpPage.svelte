<script>

//We are going to add an on mount to get the questions from the FAQ API

//We need to create the modal that displays the questions from the FAQ API

//When we click a question from the modal, it needs to display the question page on the entire screen with the question's body

//The page that displays the body of the question needs to have a back button to return to the main menu of the questions

//When we click the X or outside of the modal, we need to close out the modal and show the exerciseList

import { onMount } from "svelte";
import { state } from "./Store.svelte";
import QuestionListItem from "./QuestionListItem.svelte"

let questions = [];


onMount(async () => {
        try {
            const res = await fetch('https://learnpack.herokuapp.com/v1/support/question');
            $state.questions = await res.json();
            questions = $state.questions.map((question) => {
        return { value: question.title, component: QuestionListItem };
    });
        } catch(err){
            console.log("There was an error loading the questions", err)
        }  
	});



$:{
        console.log($state.questions)
    }



</script>

<div class="back-nav">
    <div class="back-container">
    <div class="image">
        <img alt="arrow" src="https://icongr.am/feather/arrow-left.svg?size=40&color=currentColor">
      </div>
    <div class="back-button">
        <p>back</p>
    </div>
    <p>Frequently Asked Questions</p>
</div>
</div>

<div id="question-item">
    {#each questions as question}
  <svelte:component this={question.component} {...question}/>
{/each}
</div>



<style>

.back-container{
  align-items: center;
  display: flex;
  height: 85px;
  width: 100%;
  background-color: #F5F5F5;
  padding: 12px 12px 12px 12px;
}




</style>
