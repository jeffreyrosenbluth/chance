<script lang="ts">
	export let players = '';
	export let show = 'block';
</script>

<textarea
	bind:value={players}
	style:display={show}
	placeholder="A comma separated list of players, e.g. Alice, Bob, Charlie"
	spellcheck="false"
/>

<style>
	textarea {
		width: 25vw;
		height: 25vw;
		font-family: Arial, Helvetica, sans-serif;
		font-size: 1.5vw;
		color: slategray;
		background-color: transparent;
		border-color: slategray;
		border-radius: 0.25rem;
	}
</style>
