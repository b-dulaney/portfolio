<script lang="ts">
    import { onMount } from "svelte";
    import { fade } from "svelte/transition";
    import { paths } from './shape.js';
	let show = false;
	const colors = Array(65).fill("#F2F1EC")

	onMount(() => {
		show = true
	})

	function handleMouseOver(i: number) {
		colors[i] = "#bef264"
	}

	function handleMouseOut(i: number){
		setTimeout(()=> colors[i] = "#F2F1EC", 250)
	}
	
</script>

{#if show}
	<svg
	class="-top-48 right-0 sm:-top-24 sm:right-10 md:right-24 xl:right-1/4 xl:-top-40 absolute overflow-visible w-[300px] h-[300px] md:w-[400px] md:h-[400px] lg:w-[500px] lg:h-[500px] xl:w-[600px] xl:h-[600px] z-0"
	version="1.1"
	id="shapes"
	xmlns="http://www.w3.org/2000/svg"
	xmlns:xlink="http://www.w3.org/1999/xlink"
	x="0px"
	y="0px"
	viewBox="0 5 100 100"
	xml:space="preserve"
	stroke-width="0.5"
	>
	<g>
        {#each paths as path, i (path)}
            <!-- svelte-ignore a11y-mouse-events-have-key-events -->
            <path in:fade|global={{duration: 500, delay: i*10}} d={path}
			 	on:mouseover={() => handleMouseOver(i)}
				role="presentation"
			  	on:mouseout={() => handleMouseOut(i)}
			   	fill={colors[i]}
				stroke={colors[i]}/>
        {/each}
	</g>
	</svg>
{/if}
