<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import { user } from '$lib/stores';
	import Metrics from '$lib/components/workspace/Metrics.svelte';

	// Check if user has metrics access based on role
	$: hasMetricsAccess =
		$user?.role === 'admin' || $user?.role === 'analyst' || $user?.role === 'global_analyst';

	onMount(async () => {
		// Redirect to home if user doesn't have metrics access
		if (!hasMetricsAccess) {
			await goto('/');
		}
	});
</script>

{#if hasMetricsAccess}
	<Metrics />
{/if}
