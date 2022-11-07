<script>

//We are going to add an on mount to get the questions from the FAQ API

//We need to create the modal that displays the questions from the FAQ API

//When we click a question from the modal, it needs to display the question page on the entire screen with the question's body

//The page that displays the body of the question needs to have a back button to return to the main menu of the questions

//When we click the X or outside of the modal, we need to close out the modal and show the exerciseList

import { onMount } from "svelte";
import { state } from "./Store.svelte";
// import Modal from './Modal.svelte';

// let showModal = false;
// export let questions;


</script>

<!-- <div class="container-question" id="question" on:click="{() => showModal = true}">
    <div class="image">
      <img
            alt="question"
            src="https://icongr.am/fontawesome/question-circle-o.svg?size=30&color=000000"
          />
    </div>
    <div class="text" id="help-text">
      <p>Help</p>
    </div>
  </div>


{#if showModal}
	<Modal on:close="{() => showModal = false}">
		<h2 slot="header">
			Frequently Asked Questions
			{#each questions as question}
  <svelte:component this={question.component} {...question}/>
{/each}
		</h2>
	</Modal>
{/if} -->

<div id="question-item">

</div>


<style>


</style>
