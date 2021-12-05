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
						<h3>{title}</h3>
					</a>
				</li>
			{/if}
		{/each}
	</ul>
</div>

<style>
	.news-feed {
		background-color: red;
	}
</style>
