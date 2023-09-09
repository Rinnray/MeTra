<script lang="ts">
	import '../app.postcss';
	import * as config from '$lib/config';
	import { IconMenu2 } from '@tabler/icons-svelte';
	import Navigation from '$lib/components/navigation.svelte';
	import { AppBar, AppShell, initializeStores, Drawer, getDrawerStore, popup, storePopup } from '@skeletonlabs/skeleton';
	import { computePosition, autoUpdate, offset, shift, flip, arrow } from '@floating-ui/dom';

	
	import type { PopupSettings } from '@skeletonlabs/skeleton';

	initializeStores();
	storePopup.set({ computePosition, autoUpdate, offset, shift, flip, arrow });

	const drawerStore = getDrawerStore();
	const popupFeatured: PopupSettings = {
		event: 'click',
		target: 'popupUser',
		placement: 'bottom',
	};

	function drawerOpen(): void {
		drawerStore.open();
	}
</script>

<Drawer position="left" width="w-1/2">
	<Navigation />
</Drawer>

<div class="card p-4 w-36 shadow-xl mr-24 mt-2 md:mr-0" data-popup="popupUser">
	<nav class="list-nav">
		<ul>
			<li>
				<a href="/">
					<span class="flex-auto">Profile</span>
				</a>
			</li>

			<hr />
			
			<li>
				<a href="/">
					<span class="flex-auto">Logout</span>
				</a>
			</li>
		</ul>
	</nav>
</div>

<AppShell>
	<svelte:fragment slot="header">
		<AppBar>
			<svelte:fragment slot="lead">
				<button class="btn btn-sm md:hidden" on:click={drawerOpen}>
					<IconMenu2 />
				</button>
				<h3 class="h3">{config.title}</h3>
			</svelte:fragment>

			<svelte:fragment slot="trail">
				<button class="flex flex-row items-center gap-2" use:popup={popupFeatured}>
					<img
						src="https://www.gravatar.com/avatar/715df10efbfe0d4a83a3b579bda20762?s=400"
						alt="Gravatar"
						class="rounded-full max-h-10 md:max-h-12"
					/>
					<p class="h6 font-bold md:h5">Username</p>
				</button>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>

	<svelte:fragment slot="sidebarLeft">
			<div class="hidden md:block bg-surface-100-800-token h-full w-24 p-2">
				<Navigation />
			</div>
	</svelte:fragment>
	
	<div class="p-4">
		<slot />
	</div>
</AppShell>