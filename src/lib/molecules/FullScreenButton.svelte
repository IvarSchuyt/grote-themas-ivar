<script>
  import { onMount } from 'svelte';

  // Controleert of localStorage beschikbaar is
  let isLocalStorageAvailable = typeof localStorage !== 'undefined';
  let isFullscreen = isLocalStorageAvailable && localStorage.getItem('isFullscreen') === 'true';

  onMount(async () => {
    // Vergroot de tekst op de site
    const fullScreen = document.querySelector('#fullScreen');
    const visual = document.querySelector('html');

    // Updated de knoptekst op basis van de opgeslagen status
    updateButtonText();

    // Event bij volledig scherm knop
    fullScreen.addEventListener('click', () => {
      if (!isFullscreen) {
        visual.requestFullscreen();
      } else {
        document.exitFullscreen();
      }
    });

    // Luistert naar fullscreenchange event om de fullscreen status bij te houden
    document.addEventListener('fullscreenchange', () => {
      isFullscreen = document.fullscreenElement !== null;
      updateButtonText();
      // Bewaart de status in de Local Storage
      localStorage.setItem('isFullscreen', isFullscreen);
    });
  });

  function updateButtonText() {
    // Update de knoptekst op basis van de huidige status
    const buttonText = document.querySelector('.fullscreen-span');
    buttonText.textContent = isFullscreen ? 'verklein scherm' : 'vergroot scherm';
  }
</script>
  
  <button id="fullScreen">
    {#if isFullscreen}
      <div class="fullscreen-div">
        <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-arrows-minimize" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">
            <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
            <path d="M5 9l4 0l0 -4" />
            <path d="M3 3l6 6" />
            <path d="M5 15l4 0l0 4" />
            <path d="M3 21l6 -6" />
            <path d="M19 9l-4 0l0 -4" />
            <path d="M15 9l6 -6" />
            <path d="M19 15l-4 0l0 4" />
            <path d="M15 15l6 6" />
        </svg>
        <span class="fullscreen-span">verklein scherm</span>
      </div>
    {:else}
    <div class="fullscreen-div">
        <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-arrows-maximize" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round"><path stroke="none" d="M0 0h24v24H0z" fill="none"/><path d="M16 4l4 0l0 4" />
            <path d="M14 10l6 -6" /><path d="M8 20l-4 0l0 -4" />
            <path d="M4 20l6 -6" />
            <path d="M16 20l4 0l0 -4" />
            <path d="M14 14l6 6" />
            <path d="M8 4l-4 0l0 4" />
            <path d="M4 4l6 6" />
        </svg>
        <span class="fullscreen-span">vergroot scherm</span>
      </div>
    {/if}
  </button>
  

<style>
button {
    position: fixed;
    bottom: 84px;
    right: 32px;
    padding: var(--unit-micro) var(--unit-small);
    background-color: var(--color-hva-pink);
    border: 2px solid var(--color-hva-pink);
    color: var(--color-white);
    box-shadow: var(--unit-small) var(--unit-small) #1e1649;
    transition: var(--animation-default) ease-in-out;
    z-index: 5;
    color: black;

    /* Enhanced kleuren binnen @supports */
    @supports (--css: variables) {
        background-color: var(--color-hva-yellow-contrast);
        border: 2px solid var(--color-hva-yellow-contrast);
    }
}

button .fullscreen-div {
    display: flex;
    flex-direction: row;
    align-items: center;
    font-size: var(--unit-default);
    text-transform: capitalize;
    margin: 0 var(--unit-micro);
}

button .fullscreen-div span {
    visibility: hidden;
    width: 0px;
}

/* Interactive states */
button:hover {
    background-color: var(--color-hva-pink);
    border: 2px solid var(--color-hva-pink);
    color: white;

    /* Enhanced kleuren binnen @supports */
    @supports (--css: variables) {
        background-color: var(--color-hva-pink-enhanced);
        border: 2px solid var(--color-hva-pink-enhanced);
    }

    box-shadow: 0px 0px #1e1649;
    transition: var(--animation-default) ease-in-out;
}

button:focus {
    border: 2px solid var(--color-hva-pink);
    background-color: var(--color-hva-blue-secundary);

    /* Enhanced kleuren binnen @supports */
    @supports (--css: variables) {
        border: 2px solid var(--color-hva-pink-enhanced);
        background-color: var(--color-hva-blue-secundary-enhanced);
    }
}

@media (min-width: 40rem) {
    button {
        padding-left: var(--unit-small);
    }

    button .fullscreen-div {
        gap: var(--unit-small);
    }

    button .fullscreen-div span {
        visibility: visible;
        width: fit-content;
    }
}

@media (min-width: 170rem) {
    button {
      width: 16rem;
      height: 5rem;
    }

    button .fullscreen-div span {
      font-size: 150%;   
    }
}

</style>