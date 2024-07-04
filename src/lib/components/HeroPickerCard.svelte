<script lang="ts">
	export let color: string;
	$: className = `bg-${color}-200 card-shape`;
</script>

<div class={className}>card</div>

<style scoped>
	.card-shape {
		width: 400px;
		height: 200px;
		clip-path: polygon(0% 0%, 90% 10%, 100% 100%, 0% 70%);
	}
</style>
