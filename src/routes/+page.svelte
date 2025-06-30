<script lang="ts">
	import { supabase } from '$lib/supabase';
	import { onMount } from 'svelte';

	let comments = [];

	onMount(async () => {
		const { data, error } = await supabase
			.from('comments')
			.select('*')
			.order('created_at', { ascending: false });

		if (error) {
			console.error(error);
		} else {
			comments = data;
		}
	});
</script>

<ul>
	{#each comments as comment}
		<li>{comment.content}</li>
	{/each}
</ul>
