<script>
	let randomCat = getCat();
	let API_KEY = 'YOUR_API_KEY';

	async function getCat() {
		const res = await fetch(`http://api.giphy.com/v1/gifs/random?api_key=${API_KEY}&tag=cat`);
		const data = await res.json();

		if (res.ok) {
			return data.data;
		} else {
			throw new Error(data);
		}
	}

	function handleClick() {
		randomCat = getCat()
	}
</script>
<div class="container">
	<h1>Get Cat ^._.^</h1>
	<button on:click={handleClick}>
		generate random cat gif
	</button><br>

	{#await randomCat}
		<p>...waiting</p>
	{:then cat}
		<br>
		<img src="https://media.giphy.com/media/{cat.id}/giphy.gif" alt="{cat.title}" class="img-gif">
	{:catch error}
		<p style="color: red">{error.message}</p>
	{/await}

	<p>@ api by <a href="https://giphy.com/">GIPHY</a></p>

</div>


