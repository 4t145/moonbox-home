<script lang="ts">
	import { Listgroup, ListgroupItem, Avatar } from 'flowbite-svelte';
	import HeroPickerCard from '$lib/components/HeroPickerCard.svelte';
	const heroes = [
		{
			color: 'cyan'
		},
		{
			color: 'pink'
		},
		{
			color: 'violet'
		},
		{
			color: 'cyan'
		}
		/* 英雄数据 */
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

	$: calculateRotation = (index: number): string => {
		return `${(index - pick) * 10}deg`; 
	};

	$: calculateScale = (index: number): number => {
		return 1 - Math.abs(index - pick) * 0.05; 
	};

	$: calculateBrightness = (index: number): number => {
		return 1 - Math.abs(index - pick) * 0.1; 
	};
</script>

<div class="fixed left-0 m-5 w-36">
	<Listgroup>
		<ListgroupItem class="gap-2 text-base font-semibold">Section 1</ListgroupItem>
		<ListgroupItem class="gap-2 text-base font-semibold">Section 2</ListgroupItem>
		<ListgroupItem class="gap-2 text-base font-semibold">Section 3</ListgroupItem>
	</Listgroup>
</div>
<div class="hero-picker-container" on:wheel={handleWheel}>
	{#each heroes as hero, index}
		<div
			class="hero-picker-card"
			style="transform: rotateZ({calculateRotation(index)}) rotateY({calculateRotation(
				index
			)}) scale({calculateScale(index)}); filter: brightness({calculateBrightness(index)});
            z-index: {heroes.length - Math.abs(index - pick)}; /* 根据位置调整层级 */
            "
		>
			<HeroPickerCard {...hero} />
		</div>
	{/each}
</div>

<style>
	.hero-picker-container {
		perspective: 1000px; /* 提供足够的透视深度 */
		position: relative;
		justify-content: center; /* 居中显示 */
		align-items: center; /* 居中显示 */
		height: 300px; /* 根据需要调整 */
	}

	.hero-picker-card {
		position: absolute;
		transform-style: preserve-3d; /* 保持3D效果 */
		transform-origin: -30% 0%;
		transition:
			transform 0.5s ease,
			filter 0.5s ease,
			z-index 0s;
		/* 根据卡片位置调整以下属性 */
		transform: rotateY(20deg) scale(0.9); /* 示例：向右旋转并稍微缩小 */
		filter: brightness(0.8); /* 颜色变暗 */
	}
</style>
