<template>
	<router-link :to="`/projects/${project.id}`">
		<div class="card" :style="cssVars">
			<img :src="iconSrc" :alt="`${project.title} Image`" />
			<div class="content">
				<h1>{{ project.title }}</h1>
				<p>{{ project.description }}</p>
				<div class="ellipses">
					<div class="icons">
						<img v-for="icon in project.icons" :key="icon" :src="getIcon(icon)" :title="icon" />
					</div>
				</div>
			</div>
		</div>
	</router-link>
</template>

<script lang="ts">
	import { defineComponent } from "vue";
	export default defineComponent({
		props: {
			project: {
				required: true,
				type: Object,
			},
		},
		setup({ project }) {
			let iconSrc: string;

			try {
				iconSrc = require(`../assets/img/${project.id}/icon.png`);
			} catch (e) {
				try {
					iconSrc = require(`../assets/img/${project.id}/icon.gif`);
				} catch (e) {
					iconSrc = require("../assets/img/default.png");
				}
			}

			const cssVars = {
				"--projectColor": project.color,
			};

			const getIcon = function(icon: string) {
				try {
					return require(`@/assets/icons/${icon}.svg`);
				} catch (e) {
					return require(`@/assets/icons/default.svg`);
				}
			};

			return {
				iconSrc,
				cssVars,
				getIcon,
			};
		},
	});
</script>

<style scoped>
	.card {
		display: flex;
		padding: 0 0.1em;
		border: 1px solid black;
		box-shadow: 0 0 10px rgb(var(--projectColor));
		border-radius: 20px;
		height: 100%;
	}
	.card:hover {
		box-shadow: 0 0 15px rgb(var(--projectColor));
	}
	.card > img {
		margin: auto clamp(0.2em, calc(0.2em + 2vw), 0.5em) auto calc(0.1em + 1vw);
		width: clamp(70px, 5vw, 8em);
		height: auto;
		border-radius: 50%;
		border: 4px solid rgb(var(--projectColor));
	}
	.content {
		flex: 1;
		width: 67.5vw;
	}
	h1 {
		font-size: clamp(1.5em, 5vw, 1.8em);
	}
	.ellipses {
		color: rgba(0, 0, 0, 0);
		margin-top: auto;
	}
	.icons {
		overflow: hidden;
		white-space: nowrap;
	}

	.icons > img {
		display: inline-block;
		height: calc(2vw + 1.2em);
		max-height: 2.5em;
		width: auto;
		margin: 5px;
	}
</style>
