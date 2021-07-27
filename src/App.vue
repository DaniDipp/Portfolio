<template>
	<Header />
	<router-view />
</template>

<script lang="ts">
	import { defineComponent } from "vue";
	import Header from "@/components/Header.vue"; // @ is an alias to /src

	export default defineComponent({
		name: "Home",
		components: {
			Header,
		},
	});
</script>

<style>
	:root {
		--background: 25, 34, 43;
		--foreground: 217, 226, 216;
		--highlight: 15, 189, 230;
		background-color: rgb(var(--background));
		color: rgb(var(--foreground));
	}

	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
	}

	a,
	a:visited,
	a:hover {
		color: inherit;
		text-decoration: inherit;
	}
</style>
