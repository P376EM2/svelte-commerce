<script>
import { fly } from 'svelte/transition'
import { page } from '$app/stores'
import { ProductCard, DummyProductCard } from '$lib/components'

export let data
let product_image_dimension = $page.data.store?.product_image_dimension || '3x4'
</script>

<!-- Trending products -->

{#if data.home?.trending?.length > 0}
	<div in:fly="{{ y: 20, duration: 700 }}">
		<h2 class="p-3 py-5 text-center sm:px-10 md:py-10 uppercase">
			TRENDING ON {$page.data.store?.websiteName}
		</h2>

		<ul
			class="px-3 sm:px-10 grid w-full items-start gap-3 lg:gap-6
				{product_image_dimension == '16x9'
				? 'grid-cols-1 md:grid-cols-2 lg:flex lg:flex-wrap lg:justify-between'
				: 'grid-cols-2 sm:flex sm:flex-wrap sm:justify-between'}">
			{#each data.home?.trending as p}
				<li>
					<ProductCard product="{p}" />
				</li>
			{/each}

			{#each { length: 8 } as _}
				<li class="hidden sm:block">
					<DummyProductCard />
				</li>
			{/each}
		</ul>
	</div>
{/if}
