<script>
  import ProgressBar from "./ProgressBar.svelte";

  const TOTAL = 5;

  let secondsTotal = TOTAL;
  let secondsLeft = secondsTotal;
  
  let isRunning = false;

  $: progress = (secondsTotal - secondsLeft) / secondsTotal * 100;

  const startTimer = () => {
    const timer = setInterval(() => {
      isRunning = true;
      secondsLeft -= 1;

      if (secondsLeft === -1) {
        clearInterval(timer);
        secondsLeft = TOTAL;
        isRunning = false;
      }
    }, 1000);
  };
</script>

<style>
  h2 {
    margin: 0;
  }
  .start {
    background-color: rgb(154, 73, 73);
    width: 100%;
    margin: 10px 0;
  }

  .start[disabled] {
    background-color: rgb(194,194,194);
    cursor: not-allowed;
  }
</style>

<div bp="grid">
  <h2 bp="offset-5@md 4@md 12@sm">Seconds Left: { secondsLeft }</h2>
</div>

<ProgressBar {progress} />

<div bp="grid">
  <button class="start" bp="offset-5@md 4@md 12@sm" disabled={ isRunning } on:click={ startTimer }>Start</button>
</div>
