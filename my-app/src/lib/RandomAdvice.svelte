<script>
	import { onMount } from 'svelte';
	import translate from 'translate';

	let advice = '';
	let id = '';
	let currentDate = new Date().toLocaleDateString();
	let isTranslated = false; // Etat pour suivre si le texte est traduit ou pas

	onMount(() => {
		const savedAdvice = localStorage.getItem('advice');
		const savedDate = localStorage.getItem('adviceDate');

		if (savedAdvice && savedDate === currentDate) {
			advice = savedAdvice;
			id = localStorage.getItem('adviceId');
		} else {
			fetch('https://api.adviceslip.com/advice')
				.then((response) => response.json())
				.then((data) => {
					advice = data.slip.advice;
					id = data.slip.id;
					localStorage.setItem('advice', advice);
					localStorage.setItem('adviceId', id);
					localStorage.setItem('adviceDate', currentDate);
				});
		}
	});

	// Configure DeepL API
	translate.engine = 'deepl';
	translate.key = 'bc4e5390-b178-9e86-e298-0c27fa9cbe0d:fx';

	async function toggleTranslation() {
		if (!isTranslated) {
			const translatedAdvice = await translate(advice, { from: 'en', to: 'fr' });
			advice = translatedAdvice;
		} else {
			advice = localStorage.getItem('advice');
		}
		isTranslated = !isTranslated;
	}
</script>

<section class="advice-section">
	<h2 class="advice-section__title">Advice of the Day</h2>
	<time class="advice-section__date" datetime={currentDate}>{currentDate}</time>
	<p class="advice-section__id">#{id}</p>
	<p class="advice-section__text">{advice}</p>
	<button on:click={toggleTranslation}>
		{#if isTranslated}
			<img
				width="50"
				height="50"
				src="https://img.icons8.com/clouds/100/great-britain.png"
				alt="Traduire en anglais"
				title="Traduire en anglais"
			/>
		{:else}
			<img
				width="50"
				height="50"
				src="https://img.icons8.com/clouds/100/france.png"
				alt="Traduire en français"
				title="Traduire en anglais"
			/>
		{/if}
	</button>
	<img class="advice-section__separator advice-section__separator--image" alt="" />
</section>

<style lang="scss">
	section {
		display: flex;
		flex-direction: column;
		align-items: center;
		max-width: 60vw;
		margin: 0 auto;
		color: #313a49;
		padding: 3rem;
		font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
			Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;

		/* From https://css.glass */
		background: rgba(255, 255, 255, 0.2);
		border-radius: 16px;
		box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
		border: 1px solid rgba(255, 255, 255, 0.3);
		h2 {
			display: flex;
			justify-content: center;
			text-align: center;
			margin-bottom: 1rem;
			font-size: 1.8rem;
		}
		time {
			font-size: 1.4rem;
			margin-bottom: 1rem;
		}
		.advice-section__id {
		}
		.advice-section__text {
			font-size: 1.6rem;
			margin-bottom: 1.5rem;
			line-height: 1.5rem;
		}
		.advice-section__separator {
			margin: 2rem 0 1rem 0;
		}

		.advice-section__separator--image {
			content: url('/src/images/pattern-divider-desktop.svg');
			display: block;
		}

		@media only screen and (max-width: 768px) {
			.advice-section__separator--image {
				content: url('/src/images/pattern-divider-mobile.svg');
			}
		}

		button {
			border: none;
			background-color: transparent;
			cursor: pointer;
			transition: box-shadow 0.3s ease;
		}

		button:hover {
			transform: scale(1.3);
		}
	}
</style>
