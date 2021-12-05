<script>
	export let exchangeRate;
	export let selectedPrimaryCurrency;
	export let selectedSecondaryCurrency;
</script>

<div class="exchange-rate">
	<h3>Exchange Rate:</h3>
	<h1>{exchangeRate ? Math.round(exchangeRate * 100) / 100 : ''}</h1>
	<p>{selectedPrimaryCurrency} to {selectedSecondaryCurrency}</p>
</div>

<style>
	.exchange-rate {
		background-color: grey;
	}
</style>
