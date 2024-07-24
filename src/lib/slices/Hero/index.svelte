<script lang="ts">
	import { onMount } from 'svelte';
	import gsap from 'gsap';

	import Bounded from '$lib/components/Bounded.svelte';
	import ButtonLink from '$lib/components/ButtonLink.svelte';
	import TriangleGrid from '$lib/components/TriangleGrid.svelte';
	import type { Content } from '@prismicio/client';
	import { PrismicImage, PrismicLink, PrismicRichText, PrismicText } from '@prismicio/svelte';

	export let slice: Content.HeroSlice;

	onMount(() => {
		const tl = gsap.timeline({ defaults: { ease: 'power2.inOut' } });
		tl.fromTo('.hero__heading', { scale: 0.5 }, { scale: 1, opacity: 1, duration: 1.4 });
	});
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<div class="relative text-center">
		<TriangleGrid />
		{#if slice.primary.heading}
			<h1
				class="hero__heading mx-auto max-w-3xl text-balance text-5xl font-medium opacity-0 md:text-7xl"
			>
				<PrismicText field={slice.primary.heading} />
			</h1>
		{/if}
		{#if slice.primary.body}
			<p class="mx-auto mt-6 max-w-md text-balance text-gray-300">
				<PrismicRichText field={slice.primary.body} />
			</p>
		{/if}
		{#if slice.primary.button_link}
			<ButtonLink class="mt-8" field={slice.primary.button_link}
				>{slice.primary.button_label}</ButtonLink
			>
		{/if}
		{#if slice.primary.image}
			<div class="glass-container mt-16 w-fit">
				<div
					class="absolute left-1/3 top-0 -z-10 h-2/3 w-2/3 bg-violet-700/50 mix-blend-screen blur-[120px] filter"
				/>
				<div
					class="absolute left-0 top-1/3 -z-10 h-2/3 w-2/3 bg-orange-600/50 mix-blend-screen blur-[120px] filter"
				/>
				<PrismicImage class="rounded-lg" field={slice.primary.image} />
			</div>
		{/if}
	</div>
</Bounded>
