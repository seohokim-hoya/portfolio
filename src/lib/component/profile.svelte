<svelte:options customElement={{
	tag: 'drawer-profile',
}} />

<script>
	import profile from '$lib/static/profile.png';
	import { envelopeSquare, github, instagram, phone } from 'svelte-awesome/icons';
	import Item from '$lib/component/introduction/item.svelte';
	import Icon from 'svelte-awesome';
	import Content from '$lib/component/introduction/_item.svelte';
</script>

<div class="flex h-full gap-4 w-full">
	<div class="flex flex-col h-full justify-between items-center border-r pr-4 w-fit">
		<div class="flex flex-col space-y-2 items-center">
			<img
				alt="profile"
				src={profile}
				class="rounded-xl w-72"
			/>
			<div class="h3 font-serif">
				Kim Seoho
			</div>
			<div class="h5 text-gray-400 font-mono">
				Developer
			</div>
		</div>
		<div class="w-full grid grid-rows-4 gap-x-4 grid-flow-col items-center">
			<div class="flex items-end justify-end">
				<Icon data={phone} scale={1.5} />
			</div>
			<div class="flex items-end justify-end">
				<Icon data={envelopeSquare} scale={1.5} />
			</div>
			<div class="flex items-end justify-end">
				<a
					href="https://github.com/seohokim-hoya"
					target="_blank"
					rel="noreferrer"
				>
					<Icon data={github} scale={1.5} />
				</a>
			</div>
			<div class="flex items-end justify-end">
				<a
					href="https://instagram.com/bellis_perennis_._l"
					target="_blank"
					rel="noreferrer"
				>
					<Icon data={instagram} scale={1.5} />
				</a>
			</div>
			<div class="text-gray-400">
				<p>Please contact me by email</p>
			</div>
			<div class="">
				<p>seoho7777.kim@gmail.com</p>
				<p>seohokim@kaist.ac.kr</p>
			</div>
			<div class="">
				<p>github.com/seohokim-hoya</p>
			</div>
			<div class="">
				<p>instagram.com/bellis_perennis_._l</p>
			</div>
		</div>
	</div>
	<div class="flex flex-col h-full items-center flex-1 space-y-4">
		<div class="border-b border-gray-700 w-full pb-4 flex flex-col space-y-2">
			<div class="font-brush h1 p-4 flex items-center justify-center">
				안녕하세요, 김서호입니다.
			</div>
		</div>
		<Item>
			<svelte:fragment slot="title">
				<div class="font-bold">
					학력
				</div>
				<div>
					Education
				</div>
			</svelte:fragment>
			<svelte:fragment slot="description">
				<Content content="경기북과학고등학교 졸업" />
				<Content content="KAIST 재학" />
			</svelte:fragment>
		</Item>
	</div>
</div>