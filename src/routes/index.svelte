<script context="module">
	export async function load({ fetch }) {
		const response = await fetch('https://crypto-news-live.p.rapidapi.com/news', {
			method: 'GET',
			headers: {
				'x-rapidapi-host': 'crypto-news-live.p.rapidapi.com',
				'x-rapidapi-key': import.meta.env.VITE_RAPID_API_KEY
			}
		});
		console.log('response:', response);
		const data = await response.json();
		console.log(data);
		return {
			props: { data }
		};
	}
</script>

<script>
	import NewsFeed from '$lib/NewsFeed.svelte';
	import CurrencyConverter from '$lib/CurrencyConverter.svelte';
	export let data;
</script>

<h1>Dashboard</h1>
<CurrencyConverter />
<NewsFeed articles={data} />
