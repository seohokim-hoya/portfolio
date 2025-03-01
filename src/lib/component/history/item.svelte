<svelte:options customElement={{
	tag: 'history-item',
	props: {
		summary: {reflect: true, type: "String"},
		content: {reflect: true, type: 'String'},
		href: {reflect: true, type: 'String'},
	}
}} />

<script lang="ts">
	import { AccordionItem } from '@skeletonlabs/skeleton';
	import Icon from 'svelte-awesome';
	import { minus, plus } from 'svelte-awesome/icons';

	export let summary;
</script>

<AccordionItem disabled={!($$slots.content)}>
	<svelte:fragment slot="summary">
		<p class="h3">
			{summary}
		</p>
	</svelte:fragment>
	<svelte:fragment slot="content">
		<div class="whitespace-break-spaces flex flex-col space-y-2">
			<hr />
			<slot name="content" />
			<hr />
		</div>
	</svelte:fragment>
	<svelte:fragment slot="iconOpen">
		{#if Boolean($$slots.content)}
			<Icon data={plus} />
		{/if}
	</svelte:fragment>
	<svelte:fragment slot="iconClosed">
		{#if Boolean($$slots.content)}
			<Icon data={minus} />
		{/if}
	</svelte:fragment>
</AccordionItem>