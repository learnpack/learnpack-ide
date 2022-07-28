<script>
    export let exercises;

    function showExercises() {
        let navbar = document.getElementById("navbar");
        if (navbar.style.display === "block") {
            navbar.style.display = "none";
        } else {
            navbar.style.display = "block";
        }
    }
</script>

<div class="navbar-component">
    <div id="navbar">
        {#each exercises as exercise}
            <svelte:component this={exercise.component} {...exercise} />
        {/each}
    </div>
    <button class="navbar-button" on:click={showExercises}>Open</button>
</div>

<style>
    .navbar-component {
        width: 100%;
        min-height: 2rem;
        background-color: #333;
    }

    #navbar {
        display: none;
    }

    .navbar-button {
        background: black;
        color: white;
        display: block;
        width: 10%;
        height: 2rem;
        position: absolute;
        top: 0;
        right: 0;
    }

    .active {
        background-color: #04aa6d;
        color: white;
    }
</style>
