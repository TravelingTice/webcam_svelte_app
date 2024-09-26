<script lang="ts">
	import { onMount } from 'svelte'
	let video: HTMLVideoElement
	let isSepia = false
	let error = ''

	onMount(async () => {
		video = document.querySelector('#webcam')!
		try {
			const stream = await navigator.mediaDevices.getUserMedia({ video: true })
			video.srcObject = stream
			video.play()
		} catch (err: any) {
			error = 'Error accessing webcam: ' + err.message
		}
	})
</script>

{#if error}
	<p>{error}</p>
{:else}
	<div class="flex flex-col gap-4 items-center justify-center h-screen">
		<video id="webcam" autoplay playsinline class="rounded-lg shadow {isSepia ? 'sepia' : ''}"
		></video>
		<button
			on:click={() => (isSepia = !isSepia)}
			class=" p-3 rounded-lg font-bold uppercase text-sm bg-amber-100 shadow"
			>Turn {isSepia ? 'off' : 'on'} Sepia mode</button
		>
	</div>
{/if}
