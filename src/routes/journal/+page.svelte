<script lang="ts">
	import Link from '../../components/link.svelte';
	import type { PageProps } from './$types';
	let { data }: PageProps = $props();

	// Sort the posts by date, descending
	data.posts.sort((a, b) => {
		if (a.date > b.date) return -1;
		if (a.date < b.date) return 1;
		return 0;
	});
</script>

<!-- Header -->
<div class="px-4 md:px-0">
	<div class="my-8 w-full md:w-1/2">
		<h1 class="font- font-mono text-4xl font-[900] text-blue-300 md:text-6xl">Journal.</h1>
		<p class="my-5 py-2 text-gray-200 italic">
			Here you can find my journal where I write all kinds of tech-related things. Some of them are
			about my projects, some are about my thoughts, and some are about my experiences. I hope you
			enjoy!
		</p>
	</div>

	<div class="w-full md:w-2/3">
		{#if data.posts.length === 0}
			<h2 class="py-8 text-4xl font-semibold text-gray-300 italic opacity-30 md:text-6xl">404</h2>
			<p class="w-full text-gray-300 md:w-2/3">
				Uh oh! There are no posts to show. Check back later for more content! If you think this is a
				mistake or have any interesting ideas, please let me know by sending me an
				<Link href="mailto:hhargreaves2006@gmail.com" text="email" />.
			</p>
		{/if}

		{#each data.posts as post}
			<div class="group my-5 rounded-sm border-l-4 border-blue-300 px-4">
				<a href={post.path} class="group relative inline-block no-underline">
					<h2 class="text-xl">
						<span class="relative z-10 text-gray-300">{post.title}</span>
						<span
							class="absolute -bottom-1 left-0 h-[3px] w-0 bg-blue-300 transition-all duration-300 group-hover:w-full"
						></span>
					</h2>
					<p class="text-sm text-gray-400">{post.description}</p>
				</a>
			</div>
		{/each}
	</div>
</div>
