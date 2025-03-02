<svelte:options customElement={{
	tag: 'history-year',
	props: {
		year: {reflect: true, type: 'String'},
	}
}} />

<script lang="ts">
	import { Accordion } from '@skeletonlabs/skeleton';
	import { setContext } from 'svelte';

	export let year: string = '2000';
	setContext('year', year);
</script>

<div class="flex flex-row w-full">
	<h2 class="h2 whitespace-nowrap border-r-2 pr-6 mr-4">
		{year}
	</h2>
	<Accordion class="flex-1 space-y-4">
		<slot />
	</Accordion>
</div>