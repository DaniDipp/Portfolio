<template>
	<div class="head">
		<img alt="Logo" src="@/assets/logo.png" />
		<div>
			<h1>Daniel Dippold</h1>
			<span>Software developer and community builder</span>
		</div>
	</div>
	<p>I develop and host fun stuff for my friends and online community members.</p>
</template>

<script lang="ts">
	import { defineComponent } from "vue";

	export default defineComponent({
		name: "Home",
		components: {},
	});
</script>

<style scoped>
	@media only screen and (max-width: 600px) {
		div img {
			height: 7em;
			margin-right: 0;
		}
		.head {
			flex-direction: column;
		}
	}
	img {
		height: 10em;
		border-radius: 20%;
		margin-right: 4em;
	}

	h1 {
		font-size: 3em;
		margin: 0.4em 0;
	}

	span,
	p {
		font-size: 1.2em;
	}

	.head {
		display: flex;
		justify-content: center;
		align-items: center;
		margin-bottom: 2em;
	}
</style>
