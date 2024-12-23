<script>
  //@ts-nocheck
  import { Card, CardText, Button, Icon, Dialog } from "svelte-materialify";
  import { mdiBook, mdiPlay, mdiPause } from "@mdi/js";
  export let textarab;
  export let arti;
  export let tafsiran;
  export let long;
  export let audiodata;
  export let num;

  let play = false;
  let tafsir = false;

  let audionya = new Audio(audiodata);

  function PlayAudio() {
    audionya.play();
    play = true;
  }

  function PauseAudio() {
    audionya.pause();
    play = false;
  }

  audionya.onended = () => {
    play = false;
  };
</script>

<Card class="elevation-2 rounded-lg ma-2">
  <div class="pa-3 pa-sm-4">
    <div class="d-flex align-center mb-3">
      <span class="text-h6 primary--text font-weight-bold">{num}</span>
      <div class="ml-auto d-flex">
        <Button
          text
          fab
          small
          depressed
          class="mr-2 hover-elevation-2"
          on:click={() => (tafsir = true)}
          aria-label="Lihat Tafsir"
        >
          <Icon path={mdiBook} class="primary--text" />
        </Button>
        {#if play}
          <Button
            text
            fab
            small
            depressed
            class="primary hover-elevation-2"
            on:click={PauseAudio}
            aria-label="Pause Audio"
          >
            <Icon path={mdiPause} class="white--text" />
          </Button>
        {:else}
          <Button
            text
            fab
            small
            depressed
            class="primary hover-elevation-2"
            on:click={PlayAudio}
            aria-label="Play Audio"
          >
            <Icon path={mdiPlay} class="white--text" />
          </Button>
        {/if}
      </div>
    </div>
    <div class="text-center my-3 my-sm-4">
      <p class="font-kitab-bold ayat mb-3 mb-sm-4">{textarab}</p>
      <p class="grey--text text--darken-1 translation">{arti}</p>
    </div>
  </div>
</Card>

<Dialog
  class="rounded-lg"
  bind:active={tafsir}
  persistent
  width="90vw"
  maxWidth="500"
  fullscreen="xs"
>
  <div class="pa-4 pa-sm-6">
    <h3 class="text-h5 primary--text mb-3 mb-sm-4 font-weight-bold">
      Tafsir Ayat
    </h3>
    <div class="text-body-1 mb-3 mb-sm-4 tafsir-text">
      {tafsiran}
    </div>
    <div class="grey--text text--darken-1 mb-3 mb-sm-4 source-text">
      {long}
    </div>
    <div class="text-center">
      <Button
        class="primary elevation-1"
        depressed
        block="xs"
        on:click={() => (tafsir = false)}
      >
        Tutup
      </Button>
    </div>
  </div>
</Dialog>

<style>
  .ayat {
    font-size: clamp(24px, 5vw, 28px);
    line-height: 1.8;
    color: #2c3e50;
    word-wrap: break-word;
  }

  .translation {
    font-size: clamp(14px, 4vw, 16px);
    line-height: 1.6;
  }

  .tafsir-text {
    font-size: clamp(14px, 4vw, 16px);
    line-height: 1.8;
  }

  .source-text {
    font-size: clamp(12px, 3.5vw, 14px);
    line-height: 1.6;
  }

  :global(.primary) {
    background-color: #159d00 !important;
    transition: all 0.2s ease-in-out;
  }

  :global(.primary--text) {
    color: #1976d2 !important;
  }

  :global(.hover-elevation-2:hover) {
    box-shadow:
      0 3px 6px rgba(0, 0, 0, 0.16),
      0 3px 6px rgba(0, 0, 0, 0.23) !important;
  }

  @media (max-width: 600px) {
    :global(.v-dialog) {
      margin: 0 !important;
    }
  }
</style>
