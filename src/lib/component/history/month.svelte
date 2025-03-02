<svelte:options customElement={{
	tag: 'history-month',
	props: {
		month: {reflect: true, type: 'String'},
	}
}} />

<script lang="ts">
	import { Accordion } from '@skeletonlabs/skeleton';
	import { getContext } from 'svelte';

	export let month;
	let year: string = getContext('year');
</script>

<div class="flex flex-row">
	<h3 id={year + "-" + month} class="h3 whitespace-nowrap border-r pr-4 mr-2 py-2">
		{month}
	</h3>
	<Accordion class="flex-1">
		<slot />
	</Accordion>
</div>