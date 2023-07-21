<script lang="ts">
	import 'animate.css';

	export let name = '';
	export let index = 0;
	$: delay = 2 + 2 * index + 's';

	export let started = false;
	export let winner = false;

	const randRange = (min: number, max: number) => Math.random() * (max - min) + min;
	const randInt = (min: number, max: number) => Math.floor(randRange(min, max));

	const color = () => '#' + Math.floor(randRange(0.1, 0.9) * 16777215).toString(16);
	let anim = (win: boolean) => (win ? 'animate__tada' : 'animate__rotateOut');
</script>

{#if started}
	<div
		style:background-color={color()}
		style:animation-delay={delay}
		class="animate__animated {anim(winner)}"
	>
		{name}
	</div>
{:else}
	<div style:border="2.5px solid slategray">
		{name}
	</div>
{/if}

<style>
	div {
		display: flex;
		justify-content: center;
		align-items: center;
		text-align: center;
		overflow: hidden;
		font-family: Arial, Helvetica, sans-serif;
		font-weight: bold;
		font-size: 2vw;
		height: 11vw;
		color: white;
		border-radius: 0.5rem;
		animation-duration: 2s;
	}
</style>
