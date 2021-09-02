<template>
	<div>
		<div class="container">
			<!-- Full-width images with number and caption text -->
			<div
				v-for="(image, index) in project.images"
				:key="image.name"
				:style="[slide == index ? 'display: block' : 'display: none']"
				class="mySlides fade"
			>
				<div class="numbertext">{{ index + 1 }} / {{ project.images.length }}</div>
				<img :src="getImage(project.id, image.file)" style="width:100%" />
				<div class="text">{{ image.caption }}</div>
			</div>

			<!-- Next and previous buttons -->
			<a class="arrow prev" @click="prev">&#10094;</a>
			<a class="arrow next" @click="next">&#10095;</a>
		</div>
		<br />

		<!-- The dots/circles -->
		<div style="text-align:center">
			<span
				v-for="(image, index) in project.images"
				:key="image.name"
				@click="slide = index"
				class="dot"
				:class="slide == index ? 'active' : ''"
			></span>
		</div>
	</div>
</template>

<script lang="ts">
	import { defineComponent, ref } from "vue";

	export default defineComponent({
		props: {
			project: {
				required: true,
				type: Object,
			},
		},
		setup(props) {
			const slide = ref(0);

			function next() {
				slide.value++;
				if (slide.value >= props.project.images.length) slide.value = 0;
			}
			function prev() {
				slide.value--;
				if (slide.value < 0) slide.value = props.project.images.length - 1;
			}

			function getImage(projectId: string, file: string) {
				try {
					return require(`@/assets/img/${projectId}/${file}`);
				} catch (e) {
					return require("@/assets/img/default.png");
				}
			}

			return {
				slide,
				prev,
				next,
				getImage,
			};
		},
	});
</script>

<style scoped>
	* {
		box-sizing: border-box;
		--gradient: rgba(var(--background), 0.75) 0%, rgba(var(--background), 1) 100%;
	}
	.container {
		position: relative;
	}

	.arrow {
		cursor: pointer;
		position: absolute;
		top: 50%;
		width: auto;
		margin-top: -22px;
		padding: 16px;
		color: rgb(var(--foreground));
		font-weight: bold;
		font-size: 18px;
		transition: 0.2s ease;
		user-select: none;
	}

	.prev {
		left: 0;
	}

	.next {
		right: 0;
	}

	.prev:hover {
		background: linear-gradient(270deg, var(--gradient));
	}

	.next:hover {
		background: linear-gradient(90deg, var(--gradient));
	}

	.text {
		color: rgb(var(--foreground));
		background: linear-gradient(180deg, var(--gradient));
		font-size: 1.2em;
		padding: 0.3em;
		position: absolute;
		width: 100%;
		bottom: 0;
		text-align: center;
	}

	/* Number text (1/3 etc) */
	.numbertext {
		color: var(--foreground);
		background-color: rgba(var(--background), 0.75);
		font-size: 1em;
		padding: 0.25em 0.5em;
		margin: 0.25em 0.5em;
		border-radius: 0.5em;
		position: absolute;
		top: 0;
	}

	/* The dots/bullets/indicators */
	.dot {
		cursor: pointer;
		height: 15px;
		width: 15px;
		margin: 0 2px;
		background-color: rgb(var(--foreground));
		border-radius: 50%;
		display: inline-block;
		transition: background-color 0.2s ease;
	}

	.active,
	.dot:hover {
		background-color: rgb(var(--projectColor));
	}
	.dot:hover {
		opacity: 0.8;
	}

	.fade {
		animation-name: fade;
		animation-duration: 0.5s;
	}

	@keyframes fade {
		from {
			opacity: 0.4;
		}
		to {
			opacity: 1;
		}
	}
</style>
