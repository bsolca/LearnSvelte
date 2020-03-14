<script>
  import 'uikit';
  import ContactCard from './ContactCard.svelte';
  let name = "Benjamin";
  let age = 29;
  let uppercaseName;

  $: uppercaseName = name.toUpperCase();
  $: console.log(name);

  function changeAge() {
    age += 1;
    name = "Sofia";
  }

  function nameInput(event) {
    name = event.target.value;
  }
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <h1>Hello {name}! I am {age}</h1>
  <p>ok ay {uppercaseName} !!!</p>
  <button on:click={changeAge}>NOOOOOOO</button>
  <input type="text" bind:value={name}>
  <div uk-alert>Bonjour</div>
  <ContactCard />
</main>
