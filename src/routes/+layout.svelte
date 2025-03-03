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
	import { bars, infoCircle } from 'svelte-awesome/icons';
	import { onMount } from 'svelte';

	import Profile from '$lib/component/profile.svelte';

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
</script>

<Drawer>
	{#if ($drawerStore.id === '1')}
		<Profile />
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
