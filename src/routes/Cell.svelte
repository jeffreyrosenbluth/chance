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
	let anim = (win: boolean) => (win ? 'animate__winner' : 'animate__ciao');
</script>

{#if started}
	<div class={anim(winner)} style:animation-delay={delay} style:background-color={color()}>
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

	@keyframes ciao {
		0% {
			opacity: 1;
		}
		40% {
			opacity: 0.4;
			-webkit-transform: rotate3d(0, 0, 1, 360deg) scale3d(0.475, 0.475, 0.475)
				translate3d(-60px, -60px, 0);
			transform: rotate3d(0, 0, 1, 360deg) scale3d(0.475, 0.475, 0.475) translate3d(-60px, -60px, 0);
			-webkit-animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
			animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
		}

		to {
			-webkit-transform: rotate3d(0, 0, 1, 360deg) scale3d(0.1, 0.1, 0.1)
				translate3d(2000px, 1500px, 0);
			transform: rotate3d(0, 0, 1, 360deg) scale3d(0.1, 0.1, 0.1) translate3d(2000px, 1500px, 0);
			-webkit-animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
			animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
			opacity: 0;
		}
	}

	.animate__ciao {
		animation-name: ciao;
		transform-origin: center;
		animation-fill-mode: both;
	}

	@keyframes winner {
		from {
			-webkit-transform: scale3d(1, 1, 1);
			transform: scale3d(1, 1, 1);
		}

		10%,
		20% {
			-webkit-transform: scale3d(0.9, 0.9, 0.9) rotate3d(0, 0, 1, -3deg);
			transform: scale3d(0.9, 0.9, 0.9) rotate3d(0, 0, 1, -3deg);
		}

		30%,
		50%,
		70%,
		90% {
			-webkit-transform: scale3d(1.1, 1.1, 1.1) rotate3d(0, 0, 1, 3deg);
			transform: scale3d(1.1, 1.1, 1.1) rotate3d(0, 0, 1, 3deg);
		}

		40%,
		60%,
		80% {
			-webkit-transform: scale3d(1.1, 1.1, 1.1) rotate3d(0, 0, 1, -3deg);
			transform: scale3d(1.1, 1.1, 1.1) rotate3d(0, 0, 1, -3deg);
		}

		to {
			-webkit-transform: scale3d(1.5, 1.5, 1.5);
			transform: translate3d(50px, 50px, 0) scale3d(1.5, 1.5, 1.5);
		}
	}

	.animate__winner {
		-webkit-animation-name: winner;
		animation-name: winner;
		transform-origin: center;
		animation-fill-mode: both;
	}
</style>
