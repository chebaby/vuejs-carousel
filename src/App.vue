<template>
  <div>
    <carousel>
      <slide> <img src="./assets/1.png" width="100%"> </slide>
      <slide> <img src="./assets/2.jpg" width="100%"> </slide>
      <slide> <img src="./assets/3.jpg" width="100%"> </slide>
    </carousel>
  </div>
</template>





<script>

import Carousel from './components/carousel/Carousel'
import Slide from './components/carousel/Slide'

export default {
  name: 'app',
  components: {
    Carousel,
    Slide
  }
}

</script>


