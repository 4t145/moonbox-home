<script lang="ts">
	import { ButtonGroup, Button, Skeleton, ImagePlaceholder } from 'flowbite-svelte';
    import { ProfileCardSolid, AdjustmentsVerticalOutline, DownloadSolid } from 'flowbite-svelte-icons';
	export let color: string;
</script>
<div>
    <div class="flex flex-row justify-between">
        <Skeleton class="py-4 flex-grow" />
        <ImagePlaceholder class="pb-20" />
    </div>
</div>
<div style="background-color: {color};">
     {color}
</div>

<ButtonGroup class="card-button">
    <Button pill={true} class="!p-2"><ProfileCardSolid/> bilibili </Button>
    <Button pill={true} class="!p-2"><ProfileCardSolid/>tape</Button>
    <Button pill={true} class="!p-2"><ProfileCardSolid/>qq频道</Button>
</ButtonGroup>