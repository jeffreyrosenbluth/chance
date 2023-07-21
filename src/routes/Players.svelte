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
		width: 300px;
		height: 365px;
		font-family: Arial, Helvetica, sans-serif;
		font-size: 1.5vw;
		color: white;
		background-color: transparent;
		border-color: white;
		border-radius: 0.5em;
	}
</style>
