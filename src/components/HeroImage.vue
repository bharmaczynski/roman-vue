<template>
	<div class="heroImage"></div>
</template>

<script>
	export default {
		name: 'HeroImage',
	};
</script>

<style lang="scss" scoped>

	.heroImage {
		position: fixed;
		top: 0;
		z-index: -1;
		width: 100%;
		height: 100vh;
		background: url('../assets/heroimage.jpg') no-repeat;
		background-size: cover;
		background-position: 80% 0;
		&::after {
			content: '';
			position: absolute;
			top: 0;
			left: 0;
			z-index: 1;
			width: 100%;
			height: 100%;
			background: rgba(#000, .2);
		}
	}


</style>