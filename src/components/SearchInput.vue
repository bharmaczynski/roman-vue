<template>
	<input 
		id="search" 
		name="search" 
		:class="{ dark }"
		:value="value" 
		@input="handleChange"
	/>
</template>

<script>
	export default {
		name: 'SearchInput',
		props: {
			value: {
				type: String,
				required: true,
			},
			dark: {
				type: Boolean,
				default: false,
			}
		},
		methods: {
			handleChange(e) {
				this.$emit('input', e.target.value);
			}
		}
	};
</script>
 
<style lang="scss" scoped>
	input {
		margin-top: 50px;
		display: flex;
		flex-direction: column;
		width: 300px;
		height: 30px;
		border: 0;
		background: none;
		border-bottom: 1px solid #fff;
		text-align: center;
		font-size: 18px;
		font-weight: 300;
		color: #fff;
		transition: box-shadow .5s ease;
		&:focus {
			outline: none;
			box-shadow: 0 10px 20px -8px rgba(#fff, .4);
		}

		@media (min-width: 1024px) {
			font-weight: 400;
		}
	}

	.dark {
		color: #1e3d4a;
		border-bottom-color: #1e3d4a;
		&:focus {
			box-shadow: 0 10px 20px -8px rgba(#1e3d4a, .2);
		}
	}
</style>