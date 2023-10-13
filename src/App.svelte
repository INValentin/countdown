<!-- Countdown.svelte -->
<script>
  import { onDestroy } from "svelte";

  let countdownDate = new Date("2023-11-25 23:59:59").getTime();
  let timeRemaining = countdownDate - new Date().getTime();

  let days = Math.floor(timeRemaining / (1000 * 60 * 60 * 24));
  let hours = Math.floor((timeRemaining / (1000 * 60 * 60)) % 24);
  let minutes = Math.floor((timeRemaining / 1000 / 60) % 60);
  let seconds = Math.floor((timeRemaining / 1000) % 60);

  const updateCountdown = () => {
    timeRemaining = countdownDate - new Date().getTime();
    hours = Math.floor((timeRemaining / (1000 * 60 * 60)) % 24);
    minutes = Math.floor((timeRemaining / 1000 / 60) % 60);
    seconds = Math.floor((timeRemaining / 1000) % 60);
  };

  let interval = setInterval(updateCountdown, 1000);
  onDestroy(() => clearInterval(interval));
</script>

<div class="countdown-container">
  <div class="road r1">
    <div class="left-track" />
    <div class="right-track" />
    <div class="middle-track" />
  </div>
  <div class="road">
    <div class="left-track" />
    <div class="right-track" />
    <div class="middle-track" />
  </div>
  <div class="countdown-timer">
    {#if timeRemaining > 0}
      <p>{days}d {hours}h {minutes}m {seconds}s</p>
    {:else}
      <p>Countdown Complete!</p>
    {/if}
  </div>
</div>

<style>
  .countdown-container {
    position: relative;
    text-align: center;
    font-family: Arial, sans-serif;
    color: #fff;
    margin: 0;
    justify-content: space-around;
    align-items: center;
    transform-style: preserve-3d;
    perspective: 1000px;
    height: 100vh;
    width: 100vw;
  }

  .countdown-timer {
    font-size: 50px;
    width: 300px;
    left: 50%;
    display: flex;
    justify-content: center;
    justify-items: center;
    top: 10%;
    height: 200px;
    font-weight: bold;
    position: absolute;
    right: 0;
    flex: 1;
    background-color: blue;
    align-self: flex-start;
    padding: 20px;
    border: 5px solid #fff;
    border-radius: 1rem;
    position: relative;
    transform-style: preserve-3d;
    filter: drop-shadow(0 0 10px #fff);
    transform: translateZ(-100px) translateX(-50%) rotateX(-40deg)
      rotateY(-20deg);
  }

  .countdown-timer::after {
    position: absolute;
    content: "";
    top: 100%;
    left: 50%;
    height: 100px;
    border-radius: 10px;
    width: 40px;
    transform: translateX(-50%) rotateY(0deg);
    background-color: white;
    z-index: 1;
  }

  .road {
    position: absolute;
    top: 42%;
    z-index: -1;
    width: 100px;
    left: 50%;
    height: 300px;
    align-self: flex-end;
    transform: translateX(-50%);
    display: flex;
    justify-content: space-between;
  }

  .road.r1 {
    top: 67.5%;
    left: 39.65%;
    gap: 1rem;
    width: 400px;
    padding: 0;
    flex-direction: column;
    height: 100px;
  }

  .road:not(.r1) {
    position: absolute;
    top: 42%;
    z-index: -1;
    width: 100px;
    left: 50%;
    height: 300px;
    align-self: flex-end;
    transform: translateX(-50%);
    display: flex;
    justify-content: space-between;
  }
  .road > div {
    z-index: -1;
    border-left: dotted 5px white;
    height: 69%;
    margin-left: 10px;
    filter: drop-shadow(0 0 4px #fff);
    width: 10px;
  }
  .road:not(.r1) > div:last-of-type {
    height: unset;
  }
  .road:not(.r1) > div:last-of-type:after {
    content: "";
    position: absolute;
    top: 100%;
    left: 50%;
    height: 20px;
    background-color: white;
    width: 20px;
    border-radius: 50%;
    transform: translateX(-63px) translateY(-63px);
  }
  .road.r1 > div {
    width: 76.4%;
    border-left: unset;
    border-top: dotted 5px white;
    height: unset;
  }
  .road.r1 > div:last-of-type {
    width: unset;
    border-left: unset;
    border-top: dotted 5px white;
    height: unset;
  }
</style>
