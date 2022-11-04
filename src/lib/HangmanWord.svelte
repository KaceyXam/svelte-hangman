<script lang="ts">
  export let wordToGuess: string;
  export let guessedLetters: string[];

  let wordArray = wordToGuess.split("");
</script>

<div class="word">
{#each wordArray as letter}
  <span class="underline">
    <span class:show={guessedLetters.includes(letter)}>{letter}</span>
  </span>
{/each}
</div>

<style lang="scss">
  .word {
    display: flex;
    gap: 1em;
    text-transform: uppercase;
    font-family: monospace;
    .underline {
      font-size: 4rem;
      border-bottom: .1em solid black;
      .show {
        visibility: visible;
      }
      :not(.show) {
        visibility: hidden;
      }
    }
  }
</style>