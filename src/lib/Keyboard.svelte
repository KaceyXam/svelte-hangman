<script lang="ts">
  export let guessedLetters: string[]
  export let incorrectLetters: string[];
  export let addGuessedLetter: (letter: string) => void;
  export let gameOver: boolean;

  const KEYS = [
    "a",
    "b",
    "c",
    "d",
    "e",
    "f",
    "g",
    "h",
    "i",
    "j",
    "k",
    "l",
    "m",
    "n",
    "o",
    "p",
    "q",
    "r",
    "s",
    "t",
    "u",
    "v",
    "w",
    "x",
    "y",
    "z",
  ];
</script>

<div>
{#each KEYS as letter}
  <button 
    class:active={guessedLetters.includes(letter)} 
    class:invalid={incorrectLetters.includes(letter)} 
    on:click={() => addGuessedLetter(letter)}
    disabled={guessedLetters.includes(letter) || incorrectLetters.includes(letter) || gameOver}
  >
    {letter}
  </button>
{/each}
</div>

<style lang="scss">
  div {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: .5em;
    max-width: 700px;
    button {
      text-transform: uppercase;
      font-size: 1.5rem;
      width: 2em;
      background-color: white;
      border: solid black 2px;
      aspect-ratio: 1 / 1;
      :hover {
        background-color: hsl(200, 100%, 75%);
      }
    }
    button:hover:not(:disabled),
    button:focus:not(:disabled) {
      background-color: hsl(200, 100%, 75%);
    }
    .active {
      background-color: hsl(200, 100%, 50%);
      color: white;
    }
    .invalid {
      opacity: .3;
    }
  }
</style>