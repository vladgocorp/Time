<script>
  import { onMount } from "svelte";
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";
  let time = new Date();

  $: hours = time.getHours();
  $: minutes = time.getMinutes();
  $: seconds = time.getSeconds();

  onMount(() => {
    const interval = setInterval(() => {
      time = new Date();
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  });

  const progress = tweened(0, {
    duration: 400,
    easing: cubicOut,
  });

  import { createEventDispatcher } from "svelte";

  let progres = 0;
  let showModal = false;
  let modalMessage = "";
  let modalButton = "";

  const dispatch = createEventDispatcher();

  function handleYes() {
    showModal = false;
    dispatch("confirm", { value: true });
  }

  function handleNo() {
    showModal = false;
    dispatch("confirm", { value: false });
  }

  $: modalButton =
    progres === 0.5
      ? "Accept"
      : progres === 0.75
        ? "Yes"
        : progres === 1
          ? "Love u"
          : "";
  $: modalMessage =
    progres === 0.5
      ? "mehh"
      : progres === 0.75
        ? "I have to improve"
        : progres === 1
          ? "Thanks"
          : "";

  /**
   * @param {number} value
   */
  function updateProgress(value) {
    progres = value;
    showModal = true;
  }
</script>

<div class="center-content"></div>
<div class="clock-container">
  <svg viewBox="-50 -50 100 100">
    <circle class="clock-face" r="48" />

    {#each [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55] as minute}
      <line class="major" y1="35" y2="45" transform="rotate({30 * minute})" />

      {#each [1, 2, 3, 4] as offset}
        <line
          class="minor"
          y1="42"
          y2="45"
          transform="rotate({6 * (minute + offset)})"
        />
      {/each}
    {/each}

    <line
      class="hour"
      y1="2"
      y2="-20"
      transform="rotate({30 * hours + minutes / 2})"
    />

    <line
      class="minute"
      y1="4"
      y2="-30"
      transform="rotate({6 * minutes + seconds / 10})"
    />

    <g transform="rotate({6 * seconds})">
      <line class="second" y1="10" y2="-38" />
      <line class="second-counterweight" y1="10" y2="2" />
    </g>
  </svg>

  <div style="position: relative;">
    <h1>How much do you like the Watch?</h1>
    <progress value={$progress} />

    {#if showModal}
      <div class="modal">
        <div class="modal-content">
          {#if progres === 0}
            <p>Do you want to see it in a way that you do understand?</p>
            <button on:click={handleYes}>Sí</button>
            <button on:click={handleNo}>No</button>
          {:else if progres === 0.25}
            <p>Do you want to see it digitally?</p>
            <button on:click={handleYes}>Sí</button>
            <button on:click={handleNo}>No</button>
          {:else if progres === 0.5}
            <p>mehh</p>
            <button on:click={handleYes}>Accept</button>
          {:else if progres === 0.75}
            <p>I have to improve</p>
            <button on:click={handleYes}>Sí</button>
            <button on:click={handleNo}>No</button>
          {:else if progres === 1}
            <p>Thanks</p>
            <button on:click={handleYes}>Love u</button>
          {/if}
        </div>
      </div>
    {/if}
  </div>

  <button on:click={() => updateProgress(0)}>0%</button>
  <button on:click={() => updateProgress(0.25)}>25%</button>
  <button on:click={() => updateProgress(0.5)}>50%</button>
  <button on:click={() => updateProgress(0.75)}>75%</button>
  <button on:click={() => updateProgress(1)}>100%</button>
</div>

<style>
  .center-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
  }
  .modal {
    position: absolute;
    top: calc(30% + 10px);
    left: 50%;
    transform: translateX(-50%);
    z-index: 1;
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
  }
  .modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
  }

  h1 {
    margin-right: 50%;
    margin-top: 200px;
    margin-bottom: -80px;
  }

  progress {
    display: block;
    width: 50%;
    margin-top: 80px;
  }

  .clock-container {
    margin-left: 40%;
  }
  svg {
    width: 50%;
    height: 50%;
  }

  .clock-face {
    stroke: #333;
    fill: white;
  }

  .minor {
    stroke: #999;
    stroke-width: 0.5;
  }

  .major {
    stroke: #333;
    stroke-width: 1;
  }

  .hour {
    stroke: #333;
  }

  .minute {
    stroke: #666;
  }

  .second,
  .second-counterweight {
    stroke: rgb(180, 0, 0);
  }

  .second-counterweight {
    stroke-width: 3;
  }
</style>
