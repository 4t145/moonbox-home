<script lang="ts">
	import { ButtonGroup, Button } from 'flowbite-svelte';

	export let color: string;
	export let name: string;
</script>

<div class="card-shape border-black-200 border border-solid" style={`background: ${color};`}>
	<div class="flex justify-center items-center h-full">
		<h1 class="text-5xl font-bold text-white shadow-slate-700  text-shadow">{name}</h1>
	</div>
</div>

<style scoped>
	.card-shape {
		width: 30vw;
		height: 20vw;
		clip-path: polygon(0% 0%, 90% 10%, 100% 100%, 0% 70%);
	}
	.text-shadow {
        text-shadow: 4px 4px 2px #000000; 
		transform: rotateZ(5deg);
    }
</style>
