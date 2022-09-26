<script>
	import Input from './Card.svelte';

	let loading = false
  let characters
	let pagination

	const handlePager = (newUrl) => {
		if (newUrl=== null) return
    url = newUrl
  }

	let url = 'https://rickandmortyapi.com/api/character'

  $: if(url.length > 0) {
    loading = true
    fetch(url)
      .then(res => res.json())
      .then(data => {
				characters = data.results
				pagination = {next: data.info.next, prev: data.info.prev}
				loading = false
			})
  }

</script>

<main>
	<h1>Rick and Morty API</h1>

	{#if loading}
		<p>Loading...</p>
	{:else}
	<div class="wrapper_cards">
		{#each characters as {image, name}}
			<Input {image} {name} />
		{/each}		
	</div>
	<div class="wrapper_buttons">
		<button on:click={handlePager(pagination.prev)}>prev</button>
		<button on:click={handlePager(pagination.next)}>next</button>
	</div>
	{/if}

</main>

<style>
	h1 {
		text-align: center; 
		color: #1b1b1b;
		font-size: 50px;
	}

	.wrapper_cards {
		max-width: 1060px;
		margin: 0 auto;
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
		gap: 20px;
	}

	.wrapper_buttons {
		max-width: 1000px;
		margin: 50px auto;
		display: flex;
		justify-content: center;
		gap: 20px;
	}

	.wrapper_buttons button {
		width: 100%;
	}
</style>