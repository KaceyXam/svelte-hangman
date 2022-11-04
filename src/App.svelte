<script lang="ts">
  import HangmanDrawing from "./lib/HangmanDrawing.svelte";
  import HangmanWord from "./lib/HangmanWord.svelte";
  import Keyboard from "./lib/Keyboard.svelte";

  import words from "./assets/word-list.json"

  let randomWord = words[Math.floor(Math.random() * words.length)]
  console.log(randomWord);
  let guessedLetters: string[] = [];
  let incorrectLetters = guessedLetters.filter(
    letter => !randomWord.includes(letter)
  )
  $: isLoser = incorrectLetters.length >= 6;
  $: isWinner = randomWord.split("").every(letter => guessedLetters.includes(letter));
  $: gameOver = isLoser || isWinner

  function addGuessedLetter(letter: string) { 
    if (guessedLetters.includes(letter) || isLoser || isWinner) return;

    guessedLetters = [...guessedLetters, letter]
    console.log(guessedLetters)
    incorrectLetters = guessedLetters.filter(
      letter => !randomWord.includes(letter)
    )
    console.log(incorrectLetters)
  }

  document.addEventListener("keypress", (e) => {
    const key = e.key;
    if (!key.match(/^[a-z]$/)) return;
    e.preventDefault();
    console.log(key)
    addGuessedLetter(key)
  })
</script>

<main>
  <h1>
    {#if isWinner}
      You have won! Refresh the page to play again!
    {/if}
    {#if isLoser}
      You have lost! Refresh the page to try again!
    {/if}
  </h1>
  <HangmanDrawing guessesWrong={incorrectLetters.length} />
  <HangmanWord wordToGuess={randomWord} guessedLetters={guessedLetters} />
  <Keyboard 
    guessedLetters={guessedLetters.filter(letter => randomWord.includes(letter))} 
    incorrectLetters={incorrectLetters} 
    addGuessedLetter={addGuessedLetter}
    gameOver={gameOver}
  />
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: black;
    gap: 1rem
  }
  h1 {
    font-size: 2rem;
  }
</style>