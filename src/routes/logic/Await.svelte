<script lang="ts">
  async function getRandomNumber() {
    const response = await fetch("https://www.randomnumberapi.com/api/v1.0/random");
    const data = await response.text();

    if (response.ok) {
      return data;
    } else {
      throw Error(data);
    }
  }

  function handleClick() {
    randomNumberPromise = getRandomNumber();
  }

  let randomNumberPromise = getRandomNumber();

</script>

<button on:click={handleClick}>Generate random number</button>

{#await randomNumberPromise}
  <p>Waiting for random number</p>
{:then randomNumber}
  <p>{randomNumber}</p>
{:catch error}
  <p>Failed to load random number: {error}</p>
{/await}