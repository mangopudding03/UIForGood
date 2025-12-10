<script>
  import './app.css';
  import lottie from 'lottie-web';
  import { onMount } from 'svelte';
  import gamesData from './Games.json';
  import communitiesData from './Community.json';
  import mindfullnessData from './Mindfullness.json';
  

  const mindfullness = mindfullnessData.mindfullness;
  const communities = communitiesData.community;
  const games = gamesData.games;
  

  let currentpage = 'home';

  function navigateTo(page) {
    currentpage = page;
  }

  let container;

  const rightimg = ["/images/imageone.jpg", "/images/imagethree.jpg"];
  const leftimg = ["/images/imagetwo.jpeg", "/images/imagefour.avif"];

  let randomImgRight = rightimg[0];
  let randomImgLeft = leftimg[0];

  function randomimages() {
    randomImgRight = rightimg[Math.floor(Math.random() * rightimg.length)];
    randomImgLeft = leftimg[Math.floor(Math.random() * leftimg.length)];
  }

  onMount(() => {
    randomimages();
    const interval = setInterval(randomimages, 3000);

    return () => {
      clearInterval(interval);
    };
  });

  // Makes sure Max doesnt dissapear when i reroute
  $: if (currentpage === 'home' && container) {

    const anim = lottie.loadAnimation({
      container: container,
      renderer: 'svg',
      loop: true,
      autoplay: true,
      path: '/Digi.json'
    
    });
  }

</script>

<main>  
  {#if currentpage === 'home'}
    <div class="gridone">
      <div class="griditem">
        <div class="navbar">
           <button class="button" on:click={() => navigateTo('CopingStrategies')}>Relax</button>
          <button class="button" on:click={() => navigateTo('Community')}>Community</button>
          <button class="button" on:click={() => navigateTo('Games')}>Games</button>
        </div>
      </div>

      <div class="griditem">
        <div class="gridtwo">
          <div class="slide">
            <img src={randomImgRight} alt="RightImage" />
          </div>
          <div class="griditem">
            <div bind:this={container} class="container"></div>
          </div>
          <div class="slide">
            <img src={randomImgLeft} alt="LeftImage" />
          </div>
        </div>
        
      </div>
    </div>  


  {:else if currentpage === 'CopingStrategies'}
    <div class="homeicon" on:click={() => navigateTo('home')}>
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
        <path stroke-linecap="round" stroke-linejoin="round" d="m2.25 12 8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25" />
      </svg>
    </div>

    <div>
      <h3 class="quote"><i>"There is hope, even when your brain tells you there isn't"</i></h3>
      <h4 class="quoteorigin">- John Green</h4>
      {#each mindfullness as mind}
        <div class="communitycard">
          <h3>{mind.title}</h3>
          <p>{mind.description}</p>
          <div>
            <iframe src= {mind.url} frameborder="0" allowfullscreen></iframe>
          </div>

        </div>
      {/each}
    </div>



  {:else if currentpage === 'Community'}
    <div class="homeicon" on:click={() => navigateTo('home')}>
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
        <path stroke-linecap="round" stroke-linejoin="round" d="m2.25 12 8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25" />
      </svg>
      </div>
    <h3 class="quote"><i>"Your now is not your forever"</i></h3>
    <h4 class="quoteorigin">-John Green</h4>
    <div>
      {#each communities as comm}
        <div class="communitycard">
          <h3>{comm.title}</h3>
          <p>{comm.description}</p>
          <p>{comm.address}</p>
        </div>
      {/each}
    </div>



  {:else if currentpage === 'Games'}
    <div class="homeicon" on:click={() => navigateTo('home')}>
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
        <path stroke-linecap="round" stroke-linejoin="round" d="m2.25 12 8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25" />
      </svg>
    </div>
    <div class="gamessection">
      {#each games as game}
        <div class="gamecard">
          <img class="gameimage" src={game.image} alt={game.title} />
          <h3>{game.title}</h3>
        </div>
      {/each}
    </div>


{/if}


</main>



