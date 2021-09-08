<template>
	<p class="header">
		This is a selection of projects I have completed over the last few years. There is a strong survivorship bias here as many
		more projects never saw the light of day, due to changing requirements and priorities.<br />
		If I ever get the chance to get one of them to a presentable state, I will add it here.
	</p>
	<div class="body">
		<Card v-for="project in projects.filter((p) => p.id)" :key="project.id" :project="project" />
	</div>
</template>

<script lang="ts">
	import { defineComponent } from "vue";
	import projects from "@/assets/projects.json";
	import Card from "@/components/Card.vue";

	export default defineComponent({
		components: {
			Card,
		},
		setup() {
			return { projects };
		},
	});
</script>

<style>
	@media only screen and (max-width: 450px) {
		div.body {
			grid-template-columns: minmax(290px, 1fr);
		}
	}
	.body {
		padding: 0 1rem;
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
		grid-gap: 1rem;
		padding: clamp(0px, 0.1vw, 5px);
	}
	.header {
		font-size: clamp(1.1rem, 1.1vw, 1.5rem);
		padding: clamp(0px, 0.1vw, 5px);
	}
</style>
