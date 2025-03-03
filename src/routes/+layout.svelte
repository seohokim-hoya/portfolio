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
	import { bars, github, instagram, envelope, phone, infoCircle } from 'svelte-awesome/icons';
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
		<div class="flex h-full gap-4 w-full">
			<div class="flex flex-col h-full justify-between items-center border-r pr-4 w-fit">
				<div class="flex flex-col space-y-2 items-center">
					<img
						alt="profile"
						src={profile}
						class="rounded-xl w-60"
					/>
					<div class="h3 font-serif">
						Kim, Seoho
					</div>
					<div class="h5 text-gray-400 font-mono">
						Developer
					</div>
				</div>
				<div class="w-full grid grid-rows-4 gap-2 grid-flow-col items-center">
					<div class="flex items-end justify-end">
						<Icon data={phone} scale={1.5} />
					</div>
					<div class="flex items-end justify-end">
						<Icon data={envelope} scale={1.5} />
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
					<div class="font-serif h3">
						About Me
					</div>
					<div class="">
						안녕하세요,
					</div>
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
				<div class="flex items-center justify-center gap-4">
					<button
						type="button"
						class="btn-icon variant-filled"
						on:click={openSideMenu}
					>
						<Icon
							data="{bars}"
						/>
					</button>
					<button
						type="button"
						on:click={openSideMenu}
					>
						<Icon
							data="{infoCircle}"
							scale={1.5}
						/>
					</button>
				</div>
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
					class="flex items-center justify-center gap-4"
					on:click={openProfile}
				>
					<span class="font-serif h4">
						About Me
					</span>
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
