<script>
import { useParams } from "svelte-navigator";
const params = useParams();
$: console.log($params);

let question;

async function load(slug){
    const res = await fetch(`https://learnpack.herokuapp.com/v1/support/question/${slug}`)
    question = await res.json()
    
  }

$: load($params.questionSlug)

</script>



<div>
<h1>{question ? question.title : ""}</h1>
<p>test paragraph</p>
</div>


