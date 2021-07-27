<template>
	<nav>
		<router-link to="/">Profile</router-link> | <router-link to="/projects">Projects</router-link> |
		<router-link to="/about">About</router-link>
	</nav>
</template>

<script>
	export default {};
</script>

<style scoped>
	nav {
		padding: 30px;
		font-size: 20px;
	}

	nav a {
		font-weight: bold;
		text-decoration: none;
		font-size: 16px;
		color: rgb(var(--highlight));
	}

	nav a:hover {
		text-decoration: underline;
	}

	nav a.router-link-exact-active {
		font-size: 20px;
	}
</style>
