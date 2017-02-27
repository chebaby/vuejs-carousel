<template>
	<div class="carousel">

		<slot></slot>

		<button type="button" 
				class="carousel__nav carousel__next" 
				@click.prevent="next">Next
		</button>
		<button type="button" 
				class="carousel__nav carousel__prev" 
				@click.prevent="prev">Prev
		</button>

		<div class="carousel__pagination">
			<button v-for="item in slidesCount" 
					@click="jumpTo(item-1)" 
					:class="{active: item - 1 == position}">				
			</button>
		</div>

	</div>
</template>



<script>

	export default {

		name: 'carousel',
		// the state
		data () {

			return {
				position: 0,
				slides: [],
				direction: '' // direction of the slide animation
			}
		},

		// when the carousel is created
		mounted () {
			// children/slides in the carousel
			this.slides = this.$children

			// foreach children/slide in the carousel assign the position/index
			this.slides.forEach((slide, index) => {
				slide.position = index
			})
		},

		methods: {
			next () {
				this.position += 1
				// 
				this.direction = 'toRight'
				// Generate loop:
				// If the carousel reach the last slide
				// Return the first slide position/index
				if(this.position >= this.slidesCount) {
					this.position = 0
				}
			},

			prev () {
				this.position -= 1
				this.direction = 'toLeft'
				// Generate loop:
				// If the slide position is less than 0
				// Return the last slide position/index
				if(this.position < 0) {
					this.position = this.slidesCount - 1
				}
			},

			jumpTo (position) {
				this.direction = position > this.position ? 'toRight' : 'toLeft'
				this.position = position

			}
		},

		computed: {
			// Retrun the number of slides in the carousel
			slidesCount () {
				return this.slides.length
			}
		}
	}

</script>

<style>
	.carousel{
		position:relative;
		overflow: hidden;
	}

	.carousel__nav{
		position: absolute;
		top: 50%;
	}

	.carousel__nav.carousel__next{
		right: 0;
	}

	.carousel__nav.carousel__prev{
		left: 0;
	}

	.carousel__pagination{
		position: absolute;
	    bottom: 15px;
	    left: 0;
	    right: 0;
	    text-align: center;
	}

	.carousel__pagination button{
		margin-right: 5px;
	    height: 15px;
	    width: 15px;
	    border-radius: 50%;
	    background-color: black;
	    opacity: 0.5;
	    cursor: pointer;
	}

	.carousel__pagination button.active{
		background-color: white;
		opacity: 1;
	}
</style>