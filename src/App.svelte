<script lang="ts">
	import data from './data';

	let search: string;
	let res = new Array<string>();
	function s(search: string): Array<string> {
		const exact = data.get(search);
		if (exact) {
			return new Array<string>(search);
		}
		const res = new Array<string>();
		let search2 = search;
		a: while (search2.length > 0) {
			for (let i = 0; i <= search2.length; i++) {
				const term = search2.substr(0, i);
				const r = data.get(term);
				if (r) {
					search2 = search2.substr(i, search2.length-i);
					res.push(r);
					continue a;
				}
			}
			search2 = search2.substr(1);
		}
		// TODO: get by prefix, exhaust
		if (res.length == 0 || search2.length !== 0) {
			return new Array<string>(search);
		}
		return res;
	}
	function doSearch() {
		res = search.split(/\s/).map(s).flat();
	}
</script>

<svelte:head>
	<title>Acronyms</title>
	<link rel="icon" type="image/vnd.microsoft.icon" href="favicon.ico" />
</svelte:head>
<header>
	<img id="favicon" src="/favicon.svg" alt="" />
</header>
<main>
	<h1>Acronyms</h1>
	<input type="text" placeholder="jpq mpls is pre gud" bind:value={search} on:input={() => doSearch()} />
	{#if res.length > 0}
		<p>{res.join(' ')}</p>
	{:else}
		<p>No result</p>
	{/if}
	<h2>Legend</h2>
	<ul>
		{#each [...data] as [key, value]}
		<li>{key} → {value}</li>
		{/each}
	</ul>
</main>
<p style="display: none;">yes I know it sucks; that's a TODO</p>

<style>
	#favicon {
		width: 5rem;
		margin: 0 auto;
		float: right;
	}
</style>
