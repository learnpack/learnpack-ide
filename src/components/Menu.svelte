<script>
  export let exercises = [];
	export let onClick = null;
	export let className = "";
</script>


<div className={`left-menu ${className}`}>
{#if exercises.length > 0} 
        <ul>
            <li on:click={() => onClick({ slug: "help" })}><i className="fas fa-question-circle"></i> Help</li>
            {#each exercises as {e}} 
            (<li key={e.slug} on:click={() => onClick && onClick(e)}>
                {#if e.done} <i className="fas fa-check text-success"></i>
                    {:else} <i className="fas fa-circle text-dark"></i>
                {/if}
                <span className="ml-2">{e.title}</span>
            </li>)
            {/each}
        </ul>
        {:else}
        <div>No exercises have been loaded.</div>
    {/if}
</div>



<style>
  .left-menu{
    color: #ffffff;
    background: #333333;
    height: 0vh;
    max-height: 0vh;
    overflow-y: auto;
    transition: max-height 1s ease, height 1s ease;    
    
}

</style>