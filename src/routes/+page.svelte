<script lang="ts">
	import { Listgroup, ListgroupItem, Avatar } from 'flowbite-svelte';
	import HeroPickerCard from '$lib/components/HeroPickerCard.svelte';
	import HeroIntro from '$lib/components/HeroIntro.svelte';
	import { onMount, onDestroy } from 'svelte';

	const heroes = [
		{
			color: 'cyan',
			name: '汉字Alphabet'
		},
		{
			color: 'pink',
			name: '汉字Alphabet',

		},
		{
			color: 'violet',
			name: '汉字Alphabet',

		},
		{
			color: 'yellow',
			name: '汉字Alphabet'

		}
	];
	$: pick = 0;
	function handleWheel(event: WheelEvent) {
		if (event.deltaY < 0) {
			if (pick > 0) {
				pick -= 1;
			} else {
				pick = heroes.length - 1;
			}
		} else {
			if (pick < heroes.length - 1) {
				pick += 1;
			} else {
				pick = 0;
			}
		}
	}

	$: getDisplayIndex = (index: number): number => {
		if (index < pick) {
			return heroes.length - pick + index;
		} else {
			return index - pick;
		}
	};
	$: calculateRotation = (index: number): string => {
		const display_index = getDisplayIndex(index);
		const deg_increment = 60 / heroes.length;
		return `${display_index * deg_increment}deg`;
	};

	$: calculateScale = (index: number): number => {
		const display_index = getDisplayIndex(index);
		const scale_decrement = 0.3 / heroes.length;
		return 1 - display_index * scale_decrement;
	};

	$: calculateBrightness = (index: number): number => {
		const display_index = getDisplayIndex(index);
		const brightness_decrement = 0.3 / heroes.length;
		return 1 - display_index * brightness_decrement;
	};
	let container: HTMLDivElement;

	onMount(() => {
		container.addEventListener('wheel', handleWheel, { passive: true });
	});

	onDestroy(() => {
		if (container) {
			container.removeEventListener('wheel', handleWheel);
		}
	});
</script>
<div class="flex flex-row content-center align-middle justify-between">
	<div class="hero-picker-container content-center" bind:this={container} on:wheel={handleWheel}>
		{#each heroes as hero, index}
			<div
				class="hero-picker-card"
				style="transform: rotateZ({calculateRotation(index)}) rotateY({calculateRotation(
					index
				)}) scale({calculateScale(index)}); 
	filter: brightness({calculateBrightness(index)});
	z-index: {heroes.length - getDisplayIndex(index)};"
			>
				<HeroPickerCard {...hero} />
			</div>
		{/each}
	</div>
	<div class="flex-grow py-12">
		<HeroIntro {...heroes[pick]} />
	</div>
</div>

<style>
	.hero-picker-container {
		perspective: 1000px;
		min-width: 35vw;
	}

	.hero-picker-card {
		position: absolute;
		transform-style: preserve-3d;
		transform-origin: -30% 0%;
		transition:
			transform 0.5s ease,
			filter 0.5s ease,
			z-index 0s;
	}
</style>
