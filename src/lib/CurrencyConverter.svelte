<script lang="ts">
	import ExchangeRateDisplay from '$lib/ExchangeRateDisplay.svelte';

	const currencies = ['BTC', 'SOL', 'ETH', 'USD', 'XRP', 'LTC', 'ADA', 'AVAX'];
	let selectedPrimaryCurrency: string;
	let selectedSecondaryCurrency = 'USD';
	let primaryCurrencyAmount = 1;
	let secondaryCurrencyAmount: number;
	let exchangeRate: number;

	async function convert() {
		const response = await fetch(
			`https://alpha-vantage.p.rapidapi.com/query?from_currency=${selectedPrimaryCurrency}&function=CURRENCY_EXCHANGE_RATE&to_currency=${selectedSecondaryCurrency}`,
			{
				method: 'GET',
				headers: {
					'x-rapidapi-host': 'alpha-vantage.p.rapidapi.com',
					'x-rapidapi-key': import.meta.env.VITE_RAPID_API_KEY as string
				}
			}
		);
		const data = await response.json();
		console.log(data);
		// Update secondaryCurrencyAmount input display
		exchangeRate = data['Realtime Currency Exchange Rate']['5. Exchange Rate'];
		secondaryCurrencyAmount = +exchangeRate * primaryCurrencyAmount;
	}
</script>

<div class="currency-converter">
	<h2>Currency Converter</h2>

	<div class="input-box">
		<table>
			<tr>
				<td>Primary Currency:</td>
				<td>
					<input type="number" name="currency-amount-1" bind:value={primaryCurrencyAmount} />
				</td>
				<td>
					<select
						name="currency-option-1"
						id=""
						class="currency-options"
						bind:value={selectedPrimaryCurrency}
						on:change={() => console.log('p:', selectedPrimaryCurrency)}
					>
						{#each currencies as currency, i}
							<option value={currency}>{currency} </option>{/each}
					</select>
				</td>
			</tr>
			<tr>
				<td>Secondary Currency:</td>
				<td>
					<input
						type="number"
						name="currency-amount-2"
						bind:value={secondaryCurrencyAmount}
						disabled
					/>
				</td>
				<td>
					<select
						name="currency-option-2"
						id=""
						class="currency-options"
						bind:value={selectedSecondaryCurrency}
						on:change={() => console.log('s:', selectedSecondaryCurrency)}
					>
						{#each currencies as currency, i}
							<option value={currency}>{currency}</option>
						{/each}
					</select>
				</td>
			</tr>
		</table>
		<button on:click={convert}>Convert</button>
	</div>
	<ExchangeRateDisplay {exchangeRate} {selectedPrimaryCurrency} {selectedSecondaryCurrency} />
</div>

<style>
	.currency-converter {
		background-color: rgb(230, 223, 211);
		padding: 10px;
		margin: 5px;
		border-radius: 10px;
		box-shadow: 0 2px 5px rgb(0, 0, 0);
		text-align: center;
	}

	.input-box {
		background-color: rgb(218, 227, 238);
		padding: 30px;
		border-radius: 10px;
		box-shadow: 0 2px 5px rgb(0, 0, 0);
	}

	button {
		border: none;
		float: right;
		margin: 2px;
	}

	button:hover {
		background-color: coral;
	}

	input,
	select {
		border: none;
	}
</style>
