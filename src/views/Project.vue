<template>
	<div class="project" v-if="project" :style="cssVars">
		<h1>{{ project.title }}</h1>
		<span>{{ project.description }}</span>
		<div class="icons">
			<img v-for="icon in project.icons" :key="icon" :src="getIcon(icon)" :title="icon" />
		</div>
		<div class="part1">
			<Carousel v-if="project.images.length > 0" :project="project" class="images"></Carousel>
			<div class="list">
				<h2>Technologies Used</h2>
				<ul>
					<li v-for="item in project.technologies" :key="item.name">
						<a v-if="item.url" :href="item.url" target="_blank">{{ item.name }}</a>
						<a v-else>{{ item.name }}</a>
						<p v-html="item.explanation"></p>
					</li>
				</ul>
			</div>
		</div>
		<div v-if="project.description_long" class="description">
			<h2>Description</h2>
			<p v-html="project.description_long"></p>
		</div>
	</div>
	<div v-else>
		not project
	</div>
</template>

<script lang="ts">
	import { defineComponent } from "vue";
	import { useRoute } from "vue-router";
	import Carousel from "@/components/Carousel.vue";
	import projects from "@/assets/projects.json";

	export default defineComponent({
		components: {
			Carousel,
		},
		setup() {
			const route = useRoute();
			const project = projects.find((p) => p.id == route.params.project);
			if (project) {
				project.technologies.forEach((t) => {
					t.explanation = t.explanation.replaceAll(/\[([^\]]+)\]\(([^\)]+)\)/g, '<a href="$2" target="_blank">$1</a>');
				});
				project.description_long = project.description_long.replaceAll(
					/\[([^\]]+)\]\(([^\)]+)\)/g,
					'<a href="$2" target="_blank">$1</a>'
				);
			}

			const cssVars = {
				"--projectColor": project?.color,
			};

			const getIcon = function(icon: string) {
				try {
					return require(`@/assets/icons/${icon}.svg`);
				} catch (e) {
					return require(`@/assets/icons/default.svg`);
				}
			};

			return {
				project,
				cssVars,
				getIcon,
			};
		},
	});
</script>

<style>
	@media only screen and (max-width: 900px) {
		.part1 {
			flex-direction: column-reverse;
			align-items: center;
		}
		div.images {
			margin-right: 0;
		}
	}
	.icons {
		margin-top: auto;
		white-space: nowrap;
	}

	.icons > img {
		display: inline-block;
		height: 2.5em;
		width: auto;
		margin: 5px;
	}
	.part1 {
		display: flex;
		margin-top: 1em;
		justify-content: center;
	}
	.images {
		min-width: 300px;
		max-width: 700px;
		flex: 1 3;
		margin-right: 1em;
	}
	.list {
		flex: 1 1;
		max-width: 700px;
		text-align-last: left;
	}
	.project a[href] {
		color: rgb(var(--projectColor));
	}
	li > a {
		font-size: 1.1em;
		font-weight: bold;
	}
	li > p {
		margin-top: 0;
	}
	h2 + p {
		font-size: 1.1em;
		max-width: 1000px;
		margin: 0 auto;
	}
</style>
