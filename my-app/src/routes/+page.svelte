<script>
	import RandomAdvice from '$lib/RandomAdvice.svelte';
</script>

<main>
	<RandomAdvice />
</main>

<style lang="scss">
	main {
		height: calc(100dvh - 16px);
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
</style>
