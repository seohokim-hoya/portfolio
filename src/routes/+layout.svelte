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
	import { bars } from 'svelte-awesome/icons';

	initializeStores();

	const drawerStore: DrawerStore = getDrawerStore();

	const profileDrawerSettings: DrawerSettings = {
		id: '1',
		bgDrawer: 'text-white border-2 border-white',
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
		bgDrawer: 'text-white border-2 border-white bg-surface-900 p-4',
		// blur: 'backdrop-blur',
		// bgBackdrop: 'bg-gradient-to-tr from-indigo-500/50 via-purple-500/50 to-pink-500/50',
		width: 'w-[280px] md:w-[480px]',
		padding: 'p-4 pt-28',
		rounded: 'rounded-xl'
	};

	// drawerStore.open(sideMenuSettings);

	function openSideMenu() {
		drawerStore.open(sideMenuSettings);
	}
</script>

<Drawer>
	{#if ($drawerStore.id === '1')}
		<p>
			profile
		</p>
	{:else if ($drawerStore.id === '2')}
		<div class="flex flex-col gap-4">
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
			<TableOfContents />
		</div>
	{/if}
</Drawer>

<AppShell>
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
