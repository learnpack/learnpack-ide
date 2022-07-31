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

<!-- <div class="navbar-component">
    <div id="navbar">
        {#each exercises as exercise}
            <svelte:component this={exercise.component} {...exercise} />
        {/each}
    </div>
    <button class="navbar-button" on:click={showExercises}><img src="https://icongr.am/fontawesome/align-justify.svg?size=25&color=ffffff"></button>
    <br>
    
</div> -->

<nav>
         <div class="menu">
             <!-- svelte-ignore a11y-invalid-attribute -->
            <a href="#" on:click={showExercises}><img alt="menu" src="https://icongr.am/fontawesome/align-justify.svg?size=25&color=ffffff"></a>
         </div>
         <div id="navbar">
            {#each exercises as exercise}
                <svelte:component this={exercise.component} {...exercise} />
            {/each}
        </div>
         <ul>
            <!-- <li><a class="active" href="#">Language</a></li> -->
            <!-- svelte-ignore a11y-invalid-attribute -->
            <li><a href="#"><img alt="play" src="https://icongr.am/fontawesome/play-circle-o.svg?size=30&color=ffffff"></a></li>
            <!-- svelte-ignore a11y-invalid-attribute -->
            <li><a href="#"><img alt="tutorial" src="https://icongr.am/fontawesome/graduation-cap.svg?size=30&color=ffffff"></a></li>
            <!-- svelte-ignore a11y-invalid-attribute -->
            <li><a href="#"><img alt="left-arrow" src="https://icongr.am/fontawesome/arrow-left.svg?size=30&color=ffffff"></a></li>
            <!-- svelte-ignore a11y-invalid-attribute -->
            <li><a href="#"><img alt="right arrow" src="https://icongr.am/fontawesome/arrow-right.svg?size=30&color=ffffff"></a></li>
         </ul>
      </nav>

<style>

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
} 
nav{
  display: flex;
  height: 80px;
  width: 100%;
  background: #1b1b1b;
  align-items: center;
  justify-content: space-between;
  padding: 0 50px 0 100px;
  flex-wrap: wrap;
}
nav .menu{
  color: #fff;
  font-size: 35px;
  font-weight: 600;
}
nav ul{
  display: flex;
  flex-wrap: wrap;
  list-style: none;
}
nav ul li{
  margin: 0 5px;
}
nav ul li a{
  color: #f2f2f2;
  text-decoration: none;
  font-size: 18px;
  font-weight: 500;
  padding: 8px 15px;
  border-radius: 5px;
  letter-spacing: 1px;
  transition: all 0.3s ease;
}
/* nav ul li a.active, */
nav ul li a:hover{
  color: black;
  
}

@media (max-width: 1000px){
  nav{
    padding: 0 40px 0 50px;
  }
}
@media (max-width: 920px) {
  nav .menu-btn i{
    display: block;
  }

  nav ul{
    position: fixed;
    top: 80px;
    left: -100%;
    background: #111;
    height: 100vh;
    width: 100%;
    text-align: center;
    display: block;
    transition: all 0.3s ease;
  }
  nav ul li{
    width: 100%;
    margin: 40px 0;
  }
  nav ul li a{
    width: 100%;
    margin-left: -100%;
    display: block;
    font-size: 20px;
    transition: 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  }
  #click:checked ~ ul li a{
    margin-left: 0px;
  }
  nav ul li a.active,
  nav ul li a:hover{
    background: none;
    color: cyan;
  }
}


    #navbar {
        display: none;
    }


</style>