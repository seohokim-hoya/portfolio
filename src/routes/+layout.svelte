<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar, initializeStores } from '@skeletonlabs/skeleton';
	import { Drawer, getDrawerStore } from '@skeletonlabs/skeleton';
	import type { DrawerSettings, DrawerStore } from '@skeletonlabs/skeleton';
	import { Avatar } from '@skeletonlabs/skeleton';
	import { cn } from '$lib/utils/cn';
	import { page } from '$app/state';
	import { TableOfContents } from '@skeletonlabs/skeleton';

	import Icon from 'svelte-awesome';
	import { bars, github, instagram, envelope, phone } from 'svelte-awesome/icons';
	import { onMount } from 'svelte';

	onMount(() => {
		const isFirstVisit = sessionStorage.getItem('isFirstVisit');
		if (!isFirstVisit) {
			openProfile();
			sessionStorage.setItem('isFirstVisit', 'true');
		}
	});

	initializeStores();

	const drawerStore: DrawerStore = getDrawerStore();

	const profileDrawerSettings: DrawerSettings = {
		id: '1',
		bgDrawer: 'text-white border-2 border-white bg-surface-900 p-4',
		// blur: 'backdrop-blur',
		width: 'w-full',
		height: 'h-full',
		padding: 'p-4 pt-28',
		rounded: 'rounded-xl',
		position: 'bottom'
	};

	function openProfile() {
		drawerStore.open(profileDrawerSettings);
	}

	const sideMenuSettings: DrawerSettings = {
		id: '2',
		bgDrawer: 'text-white border-2 border-white bg-surface-900 p-4 opacity-90',
		// blur: 'backdrop-blur',
		// bgBackdrop: 'opacity-90',
		width: 'w-[280px] md:w-[480px]',
		padding: 'p-4 pt-28',
		rounded: 'rounded-xl'
	};

	drawerStore.open(profileDrawerSettings);

	function openSideMenu() {
		drawerStore.open(sideMenuSettings);
	}

	import profile from '$lib/static/profile.png';
</script>

<Drawer>
	{#if ($drawerStore.id === '1')}
		<div class="grid grid-cols-5 h-full gap-4">
			<div class="flex flex-col h-full justify-between items-center border-r pr-4">
				<div class="flex flex-col space-y-2 items-center">
					<img
						alt="profile"
						src={profile}
						class="rounded-xl"
					/>
					<div class="h3 font-serif">
						Kim, Seoho
					</div>
					<div class="h5 text-gray-400 font-mono">
						Developer
					</div>
				</div>
				<div class="w-full flex flex-col space-y-4">
					<div class="grid grid-cols-10 w-full gap-2 items-center">
						<div class="flex items-end justify-center">
							<Icon data={phone} scale={1.5} />
						</div>
						<div class="col-span-9 text-gray-400">
							<p>Please contact me by email</p>
						</div>
					</div>
					<div class="grid grid-cols-10 w-full gap-2 items-center">
						<div class="flex items-end justify-center">
							<Icon data={envelope} scale={1.5} />
						</div>
						<div class="col-span-9">
							<p>seoho7777.kim@gmail.com</p>
							<p>seohokim@kaist.ac.kr</p>
						</div>
					</div>
					<a
						href="https://github.com/seohokim-hoya"
						target="_blank"
						rel="noreferrer"
						class="grid grid-cols-10 w-full gap-2 items-center"
					>
						<div class="flex items-end justify-center">
							<Icon data={github} scale={1.5} />
						</div>
						<div class="col-span-9">
							<p>github.com/seohokim-hoya</p>
						</div>
					</a>
					<a
						href="https://instagram.com/bellis_perennis_._l"
						target="_blank"
						rel="noreferrer"
						class="grid grid-cols-10 w-full gap-2 items-center"
					>
						<div class="flex items-end justify-center">
							<Icon data={instagram} scale={1.5} />
						</div>
						<div class="col-span-9">
							<p>instagram.com/bellis_perennis_._l</p>
						</div>
					</a>
				</div>
			</div>
			<div class="flex flex-col h-full items-center col-span-4 space-y-4">
				<div class="font-serif h4">
					About Me
				</div>
			</div>
		</div>
	{:else if ($drawerStore.id === '2')}
		<div class="flex flex-col gap-4">
			<a
				class={cn("w-full flex items-center justify-center", (page.url.pathname === '/') ? "text-primary-500" : "hover:text-primary-500")}
				href="/"
				target="_self"
				rel="noreferrer"
			>
				History
			</a>
			<hr />
			<a
				class={cn("w-full flex items-center justify-center", (page.url.pathname === '/management') ? "text-primary-500" : "hover:text-primary-500")}
				href="/management"
				target="_self"
				rel="noreferrer"
			>
				Management
			</a>
			<hr />
			<a
				class={cn("w-full flex items-center justify-center", (page.url.pathname === '/development') ? "text-primary-500" : "hover:text-primary-500")}
				href="/development"
				target="_self"
				rel="noreferrer"
			>
				Development
			</a>
			<hr />
			<a
				class={cn("w-full flex items-center justify-center", (page.url.pathname === '/research') ? "text-primary-500" : "hover:text-primary-500")}
				href="/research"
				target="_self"
				rel="noreferrer"
			>
				Research
			</a>
			<hr />
			<TableOfContents />
		</div>
	{/if}
</Drawer>

<AppShell regionPage="scroll-smooth">
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar gridColumns="grid-cols-3" slotDefault="place-self-center" slotTrail="place-content-end">
			<svelte:fragment slot="lead">
				<button
					type="button"
					class="btn-icon variant-filled"
					on:click={openSideMenu}
				>
					<Icon
						data="{bars}"
					/>
				</button>
			</svelte:fragment>
			<a
				href="/"
				target="_self"
				class="cursor-pointer hover:text-primary-500"
			>
				<strong class="text-xl uppercase">Seoho Kim</strong>
			</a>
			<svelte:fragment slot="trail">
				<button
					class="rounded-full"
					on:click={openProfile}
				>
					<Avatar
						rounded="rounded-xl"
						initials="SH"
						background="bg-primary-500"
						src="https://avatars.githubusercontent.com/u/108274577?v=4"
					/>
				</button>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>
