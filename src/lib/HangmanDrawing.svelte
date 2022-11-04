<script lang="ts">
  export let guessesWrong;

  const bodyParts = ["head", "body", "right-arm", "left-arm", "right-leg", "left-leg"]
  $: bodySlice = bodyParts.slice(0, guessesWrong)
</script>

<div class="hangman-drawing">
  {#each bodySlice as part}
    <div class={part} class:body-part={true} />
  {/each}
  <div class="rope" />
  <div class="bar" />
  <div class="pole" />
  <div class="base" />
</div>

<style lang="scss">
  .hangman-drawing {
    position: relative;
    .body-part {
      position: absolute;
    }
    .rope {
      height: 50px;
      width: 10px;
      background: black;
      position: absolute;
      top: 0;
      right: 0;
    }
    .bar {
      height: 10px;
      width: 200px;
      background: black;
      margin-left: 120px;
    }
    .pole {
      height: 400px;
      width: 10px;
      margin-left: 120px;
      background: black;
    }
    .base {
      height: 10px;
      width: 250px;
      background: black;
    }

    .head {
      width: 50px;
			height: 50px;
			border-radius: 100%;
			border: 10px solid black;
			top: 50px;
			right: -30px;
    }
    .body {
		  width: 10px;
			height: 100px;
			background: black;
			top: 120px;
			right: 0;
    }
    .right-arm {
      width: 100px;
			height: 10px;
			background: black;
			top: 150px;
			right: -100px;
			rotate: -30deg;
			transform-origin: left bottom;
    }
    .left-arm {
      width: 100px;
			height: 10px;
			background: black;
			top: 150px;
			right: 10px;
			rotate: 30deg;
			transform-origin: right bottom;
    }
    .right-leg {
			width: 100px;
			height: 10px;
			background: black;
			position: absolute;
			top: 210px;
			right: -90px;
			rotate: 45deg;
			transform-origin: left bottom;
    }
    .left-leg {
			width: 100px;
			height: 10px;
			background: black;
			position: absolute;
			top: 210px;
			right: 0px;
			rotate: -45deg;
			transform-origin: right bottom;
    }
  }
</style>