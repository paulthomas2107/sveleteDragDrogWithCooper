<script lang="ts">
	import { dndzone } from 'svelte-dnd-action';
	import { handle_promise } from 'svelte/internal';
	let items = [
		{
			id: 1,
			title: 'Blog Post 1'
		}
	];

	const handleConsider = (evt: any) => {
		console.log('consider');
	};

	const handleFinalize = (evt: any) => {
		console.log('finalize');
	};
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<section use:dndzone={{ items: items }} on:consider={handleConsider} on:finalize={handleFinalize}>
		{#each items as item (item.id)}
			<div class="card card-hover w-96 my-4">
				<header class="card-header">
					<h4>{item.title}</h4>
				</header>
			</div>
		{/each}
	</section>
</div>
