<script>
	import Item from "./Item.svelte";
	import AddItem from "./AddItem.svelte";
	import { onMount } from "svelte";

	let items = [];
	onMount(async () => {
		const res = await fetch(
			`https://tech-catalog-backend.herokuapp.com/get_items`
		);
		items = await res.json();
	});
</script>

<main>
	<AddItem />
	{#each items as item}
		<Item
			key={item.key}
			name={item.name}
			desc={item.description}
			quantity={item.quantity}
			categories={item.categories}
			image_url={"https://tech-catalog-images.s3.us-west-1.amazonaws.com/" +
				item.key +
				".png"}
		/>
	{/each}
</main>

<style>
	:global(body) {
		background-color: #eeeeee;
	}

	main {
		display: flex;
		flex-wrap: wrap;
		flex-shrink: 1;
		justify-content: center;
	}
</style>
