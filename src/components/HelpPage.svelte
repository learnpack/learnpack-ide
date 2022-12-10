<script>
import { onMount } from "svelte";
import { state } from "./Store.svelte";
import QuestionListItem from "./QuestionListItem.svelte"
    import { Link } from "svelte-navigator";

let questions = [];


onMount(async () => {
        try {
            const res = await fetch('https://learnpack.herokuapp.com/v1/support/question');
            $state.questions = await res.json();
            questions = $state.questions.map((question) => {
        return { value: question.title, slug: question.slug, answer: question.answer, component: QuestionListItem };
    });
        } catch(err){
            console.log("There was an error loading the questions", err)
        }  
	});



$:{
        console.log($state.questions)
    }



</script>

<div id="back-nav">
    <div id="back-container">
    <div class="image">
        <img alt="arrow" src="https://icongr.am/feather/arrow-left.svg?size=41&color=currentColor">
      </div>
    <div id="faq-text">
        <p>Frequently Asked Questions</p>
    </div>
</div>
</div>


<div id="question-item">
    {#each questions as question}
    <a href={`/help/${question.slug}`}>
  <svelte:component this={question.component} {...question}/>
    </a>
{/each}
</div>




<style>

#back-nav{
  height: 85px;
  width: 100%;
  background-color: #F5F5F5;
  padding: 12px 12px 12px 12px;
  box-sizing: border-box;
  margin-bottom: 2rem;
}

#back-container{
  display: flex;
  float: left;
  margin-right: 18px;
  align-items: center;
  justify-content: center;
}

#faq-text{
    font-size: 18px;
    margin-left: 3rem;
}


</style>
