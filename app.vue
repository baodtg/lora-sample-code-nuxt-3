<script setup lang="ts">
let player: any = undefined;
onMounted(() => {
	player = window.BeLivePlayerWidget.initialize({
		showId: "b5ed4b45-9d2f-4f92-aabd-992fb189c0ff",
	});
	player.on(window.BeLivePlayerWidget.PlayerEventType.READY, () => {
		console.log("Player Widget Ready");
	});
	player.on(window.BeLivePlayerWidget.PlayerEventType.MINIMIZED, () => {
		console.log("Player Widget MINIMIZED");
	});

	player.on(window.BeLivePlayerWidget.PlayerEventType.UNMINIMIZED, () => {
		console.log("Player Widget UNMINIMIZED");
	});
	player.on(window.BeLivePlayerWidget.PlayerEventType.CLOSE, () => {
		console.log("Player Widget CLOSE");
	});
});

onBeforeUnmount(() => {
	player?.removeAllListeners();
});

function close() {
	player?.close();
}
function minimize() {
	player?.minimize();
}
function unminimize() {
	player?.unminimize();
}
function watchLive() {
	player?.open();
}
</script>

<template>
	<div id="home">
		<div class="alert alert-danger" role="alert">
			We are restricting iframe from using our script. To make this sample code
			work
			<a href="/" target="_blank" class="alert-link">click here</a>
			to open this page in another browser tab and try to click "Watch Live"
			again
		</div>
		<div class="d-flex flex-column align-items-center justify-content-center">
			<img class="mx-auto" alt="Vue logo" src="/nuxt-logo.svg" width="100px" />
			<h1>Demo LORA Widget!</h1>
			<div class="d-flex justify-content-center mt-5">
				<button
					@click="watchLive"
					id="watch-button"
					class="btn btn-primary mx-2"
				>
					Watch Live
				</button>
				<button @click="close" id="close-button" class="btn btn-primary mx-2">
					Close Widget
				</button>
				<button
					@click="minimize"
					id="minimize-button"
					class="btn btn-primary mx-2"
				>
					Minimize
				</button>
				<button
					@click="unminimize"
					id="unminimize-button"
					class="btn btn-primary mx-2"
				>
					Unminimize
				</button>
			</div>
		</div>
	</div>
</template>

<style>
body {
	min-height: 100vh;
}
#app {
	text-align: center;
}
</style>
