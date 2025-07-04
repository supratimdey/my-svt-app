<script>
  let count = 0;
  function increment() {
    count += 1;
  }
</script>

<main>
  <h1>Test</h1>
  <button on:click={increment}>Count: {count}</button>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
  }
</style>
