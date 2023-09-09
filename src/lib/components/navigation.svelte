<script lang="ts">
  import { IconHome2 } from '@tabler/icons-svelte';
  import { getDrawerStore } from '@skeletonlabs/skeleton';
  import { page } from '$app/stores';

  const drawerStore = getDrawerStore();

  $: classesActive = (href: string) => (href === $page.url.pathname ? 'bg-primary-900' : '');

  function drawerClose(): void {
    drawerStore.close();
  }
</script>

<nav class="list-nav">
  <ul>
    <li>
      <a href="/" class="{classesActive('/')} flex flex-col" on:click={drawerClose}>
        <IconHome2 />
        Home
      </a>
    </li>
  </ul>
</nav>