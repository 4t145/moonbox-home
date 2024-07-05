<script lang="ts">
	import { ButtonGroup, Button } from 'flowbite-svelte';

	export let color: string;
</script>

<div class="card-shape border-black-200 border border-solid" style={`background: ${color};`}>

</div>

<style scoped>
	.card-shape {
		width: 400px;
		height: 200px;
		clip-path: polygon(0% 0%, 90% 10%, 100% 100%, 0% 70%);
	}
</style>
