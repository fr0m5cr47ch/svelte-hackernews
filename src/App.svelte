<script>
	import {onMount} from 'svelte'
	import List from './List.svelte'
	import Item from './Item.svelte'

	export let name;

	let item;
	let page;

	async function hashchange() {
		// the poor man's router!
		const path = window.location.hash.slice(1);
		if (path.startsWith('/item')) {
			const id = path.slice(6);
			item = await fetch(`https://node-hnapi.herokuapp.com/item/${id}`).then(r => r.json());
			window.scrollTo(0,0);
		} else if (path.startsWith('/top')) {
			page = +path.slice(5);
			item = null;
		} else {
			window.location.hash = '/top/1';
		}
	}

	onMount(hashchange);
</script>

<style>
	:global(body) {
		background: rgb(0,0,0);
	}
	main {
		position: relative;
		max-width: 1200px;
		margin: 0 auto;
	}

	main :global(.meta) {
		color: #c0c0c0;
		font-size: 1rem;
	}

	main :global(a) {
		color: rgb(255, 255, 255);
	}
</style>

<svelte:window on:hashchange={hashchange}/>

<main>
	<h1><a href="/">{name}</a></h1>
	{#if item}
		<Item {item} returnTo={page ? `#/top/${page}` : null}/>
	{:else if page}
		<List {page}/>
	{/if}
</main>
