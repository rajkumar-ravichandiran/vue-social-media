<template>
	<header>
		<img alt="Vue logo" class="logo" src="./assets/logo.svg" width="60" height="60" />
	</header>
	<main>
		<SocialMediaFeed />
	</main>
</template>

<script>
	import SocialMediaFeed from './components/SocialMediaFeed.vue'

	export default {
		name: 'App',
		components: {
			SocialMediaFeed
		}
	}
</script>
