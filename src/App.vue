<template>
    <div :class="[{ flexStart: step === 1}, 'wrapper']">
    	<transition name="slide">
    		<img src="./assets/logo.svg" class="logo" v-if="step === 1">
    	</transition>
    	<transition name="fade">
	    	<HeroImage v-if="step === 0"/>
	    </transition>
    	<Claim v-if="step === 0"/>
    	<SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    	<div class="results" v-if="results && !loading && step === 1">
			<Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)" />
    	</div>
    	<div class="loader" v-if="step === 1 && loading" />
    	<Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
  	</div>
</template>


<script>
/* eslint-disable */
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';
export default {
  	name: 'App',
  	components : {
  		HeroImage,
  		Claim,
  		SearchInput,
  		Item,
  		Modal,
  	},
	data() {
	  	return {
	  		loading: false,
	  		step: 0,
	  		searchValue: '',
	  		results: [],
	  		modalOpen: false,
	  		modalItem: null,
	  	};
	},
  	methods: {
  		// eslint-disable-next-line
  		handleModalOpen(item) {
  			this.modalOpen = true;
  			this.modalItem = item;
  		},
		handleInput: debounce(function() {
			this.loading = true;
			console.log(this.searchValue);
			axios.get(`${API}?q=${this.searchValue}&media_type=image`)
			.then((response) => {
				this.results = response.data.collection.items;
				this.loading = false;
				this.step = 1;
			})
			.catch((error) => {
				console.log(error);
			})
		}, 500),
	},
};
</script>

<style lang="scss">

	@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');
	
	* {
	    box-sizing: border-box;
	    -webkit-font-smoothing: antialiased;
	    -moz-osx-font-smoothing: grayscale;
	}

	body {
	    margin: 0;
	    padding: 0;
	    font-family: 'Montserrat', sans-serif;
	}

	.fade-enter-active, .fade-leave-active {
		transition: opacity .3s ease;
	}

	.fade-enter, .fade-leave-to {
		opacity: 0;
	}

	.slide-enter-active, .slide-leave-active {
		transition: transform .3s ease, opacity .3s ease;
	}

	.slide-enter, .slide-leave-to {
		opacity: 0;
		transform: translateY(-50px);
	}

	.wrapper {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		position: relative;
		width: 100%;
		min-height: 100vh;
		margin: 0;
		padding: 30px;

		&.flexStart {
			justify-content: flex-start;
		}
		
	}

	.logo {
		position: absolute;
		top: 40px;
	}

	.results {
		margin-top: 50px;
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 20px;

		@media (min-width: 768px) {
			width: 90%;
			grid-template-columns: 1fr 1fr 1fr;
		}
	}

	.loader {
		margin-top: 80px;
		display: inline-block;
		width: 64px;
		height: 64px;
	}
	.loader:after {
		content: " ";
		display: block;
		width: 46px;
		height: 46px;
		margin: 1px;
		border-radius: 50%;
		border: 5px solid #000;
		border-color: #000 transparent #000 transparent;
		animation: loading 1.2s linear infinite;
	}
	@keyframes loading {
	  0% {
	    transform: rotate(0deg);
	  }
	  100% {
	    transform: rotate(360deg);
	  }
	}

</style>
