<script>
	import Players from './Players.svelte';
	import Table from './Table.svelte';

	let playersString = '';
	$: players = playersString === '' ? [] : playersString.split(',');

	let started = false;

	function handlePlayClick() {
		started = !started;
	}

	$: show = started ? 'none' : 'block';
	$: buttonLabel = started ? 'Reset' : 'Play';
</script>

<div class="flex-container">
	<h1>Lottery</h1>
</div>

<div class="flex-container">
	<button on:click={handlePlayClick}> {buttonLabel} </button>
</div>

<div class="flex-container">
	<div><Table names={players} {started} /></div>
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

	:global(body) {
		background: linear-gradient(90deg, rgb(10, 5, 40) 0%, rgb(25, 50, 95) 50%, rgb(10, 5, 40) 100%);
	}
</style>
