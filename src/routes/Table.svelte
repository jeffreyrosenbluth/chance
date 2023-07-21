<script lang="ts">
	import Cell from './Cell.svelte';

	export let names: Array<string>;
	export let started = false;

	const range = (start: number, stop: number, step: number) =>
		Array.from({ length: (stop - start) / step }, (_, i) => start + i * step);

	function shuffle(array: Array<number>) {
		let currentIndex = array.length,
			randomIndex;
		while (currentIndex != 0) {
			randomIndex = Math.floor(Math.random() * currentIndex);
			currentIndex--;
			[array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
		}
		return array;
	}

	$: n = names.length - 1;
	// This is a hack to force a reshuffle when the table is reset.
	$: idxs = !started ? shuffle(range(0, names.length, 1)) : shuffle(range(0, names.length, 1));
</script>

<div>
	{#each names as name, i}
		<Cell {name} index={idxs[i]} {started} winner={idxs[i] === n} />
	{/each}
</div>

<style>
	div {
		display: grid;
		grid-template-columns: repeat(4, 16vw);
		gap: 1vw 1vw;
		width: 67vw;
	}
</style>
