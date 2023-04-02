<script lang="ts">
	import { dndzone } from 'svelte-dnd-action';

	interface ListItem {
		id: number;
		title: string;
		description: string;
	}

	let items: ListItem[] = [
		{
			id: 1,
			title: 'Blog Post 1',
			description: 'Blog Post 1 Description'
		},
		{
			id: 2,
			title: 'Blog Post 2',
			description: 'Blog Post 2 Description'
		}
	];

	const handleConsider = (evt: CustomEvent<DndEvent<ListItem>>) => {
		console.log('consider');
		items = evt.detail.items;
	};

	const handleFinalize = (evt: CustomEvent<DndEvent<ListItem>>) => {
		console.log('finalize');
		items = evt.detail.items;
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
