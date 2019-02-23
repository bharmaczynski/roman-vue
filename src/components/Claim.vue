<template>
	<div class="claimWrapper">
		<h1 class="claim">SPACER</h1>
		<p class="subclaim">
			Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam
		</p>
		<p class="subclaim">uis nostrud exercitation ullamco</p>
	</div>
</template>

<script>

export default {
	name: 'Claim',
}
	
</script>

<style lang="scss" scoped>
	.claimWrapper {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		text-align: center;
	}

	.claim {
		margin: 0;
		font-size: 50px;
	}

	.subclaim {
		margin: 25px 0 0 0;
		font-size: 13px;
	}
</style>