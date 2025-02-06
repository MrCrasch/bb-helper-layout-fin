<script>
	import { dndzone } from 'svelte-dnd-action';
	import { flip } from 'svelte/animate';
	import { createEventDispatcher } from 'svelte';

	const flipDurationMs = 200;

	export let items = [];
	export let nCol = 1;

	const dispatch = createEventDispatcher();

	function handleSort(e) {
		items = [...e.detail.items];
		dispatch('updateSort', { sortedItems: items });
	}

	function updateAlias(id, event) {
		dispatch('updateAlias', { id, newAlias: event.target.value });
	}

	function updateCol(event) {
		dispatch('updateCol', { col: parseInt(event.target.value, 10) || 1 });
	}
</script>

Number of Columns
<input
	type="number"
	min="1"
	bind:value={nCol}
	on:input={updateCol}
	class="col-input"
	placeholder="Columns..."
/>

<section
	use:dndzone={{ items, flipDurationMs }}
	on:consider={handleSort}
	on:finalize={handleSort}
	class="grid-container"
	style="grid-template-columns: repeat({nCol}, 1fr);"
>
	{#each items as item (item.id)}
		<div class="item" animate:flip={{ duration: flipDurationMs }}>
			<input
				type="text"
				bind:value={item.Alias}
				on:input={(e) => updateAlias(item.id, e)}
				class="alias-input"
				placeholder="Enter alias..."
			/>
			<span class="tooltip">{item.DefaultName}</span>
		</div>
	{/each}
</section>

<style>
	section {
		display: grid;
        align-content: center;
        border-color: black;
		gap: 10px;
		padding: 10px;
		min-height: 12em;
	}

	.item {
        display: flex;
        justify-content: center;
		background: #ffffff;
		border-radius: 8px;
		box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
		padding: 10px;
		position: relative;
		text-align: center;
        height: fit-content;
        width: fit-content;
		transition:
			transform 0.2s ease-in-out,
			box-shadow 0.2s ease-in-out;
	
        }

	.item:hover {
		transform: scale(1.05);
		box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
	}

	.alias-input {
		width: 100%;
		padding: 2px;
		border: none;
		border-radius: 5px;
		font-size: 1em;
		text-align: center;
		background: rgba(0, 0, 0, 0.05);
		transition: background 0.2s ease-in-out;
	}

	.alias-input:focus {
		background: rgba(0, 0, 0, 0.1);
		outline: none;
	}

	.tooltip {
		visibility: hidden;
		background-color: black;
		color: white;
		font-size: 0.85em;
		text-align: center;
		border-radius: 6px;
		padding: 5px 8px;
		position: absolute;
		z-index: 1;
		bottom: 140%;
		left: 50%;
		transform: translateX(-50%);
		opacity: 0;
		transition:
			opacity 0.3s,
			transform 0.3s;
		white-space: nowrap;
	}

	.item:hover .tooltip {
		visibility: visible;
		opacity: 1;
		transform: translateX(-50%) translateY(-5px);
	}
</style>
