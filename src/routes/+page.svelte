<script>
	import Balls from './Balls.svelte';
	import Players from './Players.svelte';
	import Table from './Table.svelte';

	let playersString = '';
	$: players = playersString === '' ? [] : playersString.split(',');

	let started = false;
	let table = false;
	$: notTable = !table;

	function handlePlayClick() {
		started = !started;
	}

	$: show = started ? 'none' : 'block';
	$: buttonLabel = started ? 'Reset' : 'Play';
</script>

<div class="flex-container">
	<h1>Lottery</h1>
</div>

<label>
	<input type="radio" name="table" value={true} bind:group={table} />
	Grid
</label>
<label>
	<input type="radio" name="p5js" value={false} bind:group={table} />
	Space
</label>

<div class="flex-container">
	<button on:click={handlePlayClick}> {buttonLabel} </button>
</div>

<div class="flex-container">
	{#if table}
		<div><Table names={players} {started} /></div>
	{:else if started}
		<div><Balls names={players} /></div>
	{:else}
		<div><Balls names={[]} /></div>
	{/if}

	<div><Players bind:players={playersString} {show} /></div>
</div>

<style>
	.flex-container {
		display: flex;
		flex-direction: row;
		gap: 3vw;
		margin: 1vw;
		color: white;
	}

	h1 {
		font-family: Arial, Helvetica, sans-serif;
		font-weight: normal;
		font-size: 4vw;
		color: white;
		margin: 1vw;
		width: 75vw;
	}

	button {
		padding: 8px;
		background-color: slategray;
		color: white;
		font-size: 1rem;
		border: 2.5px solid slategray;
		width: 10rem;
	}

	label {
		font-family: Arial, Helvetica, sans-serif;
		font-size: 1.7vw;
		color: white;
		margin: 1vw;
	}

	:global(body) {
		background: linear-gradient(90deg, rgb(10, 5, 40) 0%, rgb(25, 50, 95) 50%, rgb(10, 5, 40) 100%);
	}
</style>
