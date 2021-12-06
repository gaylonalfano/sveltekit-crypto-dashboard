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
		background-color: rgb(221, 230, 221);
		padding: 20px;
		margin-top: 10px;
		border-radius: 10px;
		box-shadow: 0 2px 5px rgb(0, 0, 0);
	}
</style>
