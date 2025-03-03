<svelte:options customElement={{
	tag: 'introduce-item',
}} />

<div class="border-b border-gray-700 w-full pb-4 flex flex-col space-y-4">
	<div class="font-serif h3 flex items-center gap-4">
		<slot name="title">
			title
		</slot>
	</div>
	<div class="flex flex-col space-y-2">
		<slot name="description">
			description
		</slot>
	</div>
</div>