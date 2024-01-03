<script lang="ts">
	import { onMount } from 'svelte';
	import Logo from '$lib/components/template/logo.svelte';
	import { fade } from 'svelte/transition';

	let quote: { text: string; quoteAuthor: string; apiAuthor: string } | undefined;

	const getQuote = async () => {
		const res = await fetch('https://type.fit/api/quotes');
		const data = await res.json();
		// random number from 0-15
		const random = Math.floor(Math.random() * 15);
		const authorArray = data[random].author.split(', ');

		quote = {
			text: data[random].text,
			quoteAuthor: authorArray[0],
			apiAuthor: authorArray[1]
		};
	};
	onMount(() => {
		getQuote();
	});
</script>

<footer
	class="flex flex-col justify-between w-full h-full gap-8 px-10 py-4 border-t sm:gap-0 sm:flex-row bg-base-200 text-base-content border-base-300"
/>
