<script lang="ts">
  import { onMount } from 'svelte';
  import * as Tone from 'tone';
    import Knob from './lib/Knob.svelte';


  let volume = 0.5; // Valeur initiale du volume
  let detune = 0; // Valeur initiale du détune

  const synth = new Tone.Synth();

  onMount(() => {
     synth.toDestination();
  });


  function updateSynth() {
    if (synth) {
      synth.volume.value = volume; // Appliquer la valeur du volume
      synth.detune.value = detune; // Appliquer la valeur du détune
    }
  }

  function playSound() {
    console.log(volume)
    console.log(detune)
    updateSynth();
    synth.triggerAttackRelease('C4', '8n');
  }
</script>

<main>
  <h1>Tone.js Demo</h1>
  <div class="controls">
    <Knob bind:value={volume}  min={0} max={100}/>
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label>Volume</label>
  </div>
  <div class="controls">
    <Knob bind:value={detune} min={-100} max={100} />
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label>Detune</label>
  </div>
  <button id="playButton" on:click={playSound}>Play Sound</button>
</main>

<style>
  .controls {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    margin-bottom: 1rem;
  }
</style>