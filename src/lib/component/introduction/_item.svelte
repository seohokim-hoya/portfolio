<svelte:options customElement={{
	tag: 'introduce-item-item',
	props: {
		content: {reflect: true, type: 'String'},
	}
}} />

<script>
	import Icon from 'svelte-awesome';
	import { check } from 'svelte-awesome/icons';

	export let content;
</script>

<div class="flex flex-row gap-2 items-center">
	<Icon data={check} />
	<div>
		{content}
	</div>
</div>