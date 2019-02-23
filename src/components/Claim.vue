<template>
	<div class="claimWrapper">
		<h1 class="claim">SPACER</h1>
		<p class="subclaim">
			Begin your journey through our amazing galaxy, and discover places you never even heard of.
		</p>
		<p class="subclaim">Type anything space-related to start.</p>
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
		color: #fff;
	}

	.claim {
		margin: 0;
		font-size: 50px;

		@media (min-width: 768px) {
			font-size: 80px;
		}

		@media (min-width: 1024) {
			font-size: 100px;
		}
	}

	.subclaim {
		max-width: 500px;	
		margin: 25px 0 0 0;
		font-size: 13px;
		font-weight: 400px;
		line-height: 1.3;
		@media (min-width: 768px) {
			font-size: 17px;
			letter-spacing: 1px;
		}
	}
</style>