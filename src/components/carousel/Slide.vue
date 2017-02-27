<template>
	<transition :name="animation">
		<div v-show="visible">
		<slot></slot>
	</div>
	</transition>
</template>


<script>
	
	export default {
		name: 'slide',

		data () {
			return {
				position: 0
			}
		},

		computed: {
			animation () {return 'slide-' + this.$parent.direction},
			visible () { return this.position === this.$parent.position }
		}
	}

</script>

<style>
	.slide-toRight-enter-active {
		animation: slideInToRight .5s;
	}

	.slide-toRight-leave-active {
		animation: slideOutToRight .5s;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		width: 100%;
	}

	@keyframes slideInToRight {
		from { transform: translateX(100%); }
		to{ transform: translateX(0); }
	}

	@keyframes slideOutToRight {
		from{ transform: translateX(0); }
		to{ transform: translateX(-100%); }
	}

	.slide-toLeft-enter-active {
		animation: slideInToLeft .5s;
	}

	.slide-toLeft-leave-active {
		animation: slideOutToLeft .5s;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		width: 100%;
	}
	
	@keyframes slideInToLeft {
		from { transform: translateX(-100%); }
		to{ transform: translateX(0); }
	}

	@keyframes slideOutToLeft {
		from{ transform: translateX(0); }
		to{ transform: translateX(100%); }
	}
</style>