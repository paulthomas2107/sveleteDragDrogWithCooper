<script lang="ts">
	import { flip } from 'svelte/animate';
	import { dndzone } from 'svelte-dnd-action';

	const flipDurationMs = 100;

	interface ListItem {
		id: number;
		title: string;
		description: string;
		tags: string[];
	}

	let items: ListItem[] = [
		{
			id: 1,
			title: 'Blog Post 1',
			description: 'Blog Post 1 Description',
			tags: ['CooperCodes']
		},
		{
			id: 2,
			title: 'Blog Post 2',
			description: 'Blog Post 2 Description',
			tags: ['Development']
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
	<section
		use:dndzone={{ items: items, flipDurationMs: flipDurationMs, dropTargetStyle: {} }}
		on:consider={handleConsider}
		on:finalize={handleFinalize}
	>
		{#each items as item (item.id)}
			<div class="card card-hover w-96 my-4" animate:flip={{ duration: flipDurationMs }}>
				<header class="card-header">
					<h4>{item.title}</h4>
				</header>
				<section class="p-4">
					{item.description}
				</section>
				<footer class="card-footer inline-block">
					{#each item.tags as tag}
						<span class="chip variant-filled-secondary">{tag}</span>
					{/each}
				</footer>
			</div>
		{/each}
	</section>
</div>
