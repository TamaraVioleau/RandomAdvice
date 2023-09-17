<script>
	import RandomAdvice from '$lib/RandomAdvice.svelte';
</script>

<main>
	<h1>Random Advice Generator</h1>
	<RandomAdvice />
</main>

<style lang="scss">
	main {
		height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
		background-image: radial-gradient(at 0% 0%, rgba(79, 70, 229, 0.33) 0px, transparent 50%),
			radial-gradient(at 98% 1%, rgba(212, 25, 118, 0.33) 0px, transparent 50%);
		background-attachment: fixed;
		background-position: center;
		background-repeat: no-repeat;
		background-size: cover;
		background-color: rgb(228 230 238);
	}

	h1 {
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		padding-bottom: 2rem;
		color: #313a49;
		line-height: 2.5rem;
		font-size: 2.5rem;
		margin-bottom: 2rem;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;

	}
</style>
