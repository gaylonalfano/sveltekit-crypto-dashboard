<script>
	export let articles;
</script>

<div class="news-feed">
	<h1>News Feed</h1>
	<ul>
		{#each articles as { title, url, source }, i}
			{#if i < 7}
				<li>
					<a target="_blank" href={url}>
						<h4>{title}</h4>
					</a>
				</li>
			{/if}
		{/each}
	</ul>
</div>

<style>
	.news-feed {
		background-color: rgb(204, 204, 231);
		padding: 10px;
		margin: 5px;
		border-radius: 10px;
		box-shadow: 0 2px 5px rgb(0, 0, 0);
		max-width: 300px;
	}

	.news-feed ul {
		list-style-type: none;
		margin: 0;
		padding: 0;
	}
</style>
