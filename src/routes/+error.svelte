<script lang="ts">
  import * as config from '$lib/config';
  import { page } from '$app/stores';
</script>

<svelte:head>
  <title>{config.title} - {$page.status}</title>
</svelte:head>

<div class="text-center pt-6 space-y-6">
  <h1 class="text-error-600 text-5xl">{$page.status}: {$page.error?.message}</h1>

  {#if $page.status === 404}
    <p class="text-lg">I'm not sure where you tried to go, but I'm sorry to say that you wont find that here.</p>
  {:else if $page.status === 500}
    <p class="text-lg">I'm sorry about that, I'm not sure what happened.</p>
  {:else}
    <p class="text-lg">I haven't seen this error yet so no custom message here.</p>
  {/if}
  <a href="/" class="text-primary-400 hover:text-primary-600">Go back Home</a>
</div>