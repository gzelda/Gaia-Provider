<template>
  <div class="block">
         <svg id="isvg" >

<defs>

<marker id="idArrow"

         viewBox="0 0 20 20" refX="0" refY="10"

         markerUnits="strokeWidth" markerWidth="3" markerHeight="10"

         orient="auto">

         <path d="M 0 0 L 20 10 L 0 20 z" fill="purple" stroke="black"/>

      </marker>

</defs>

  <path d="M 50 450 l 0 -350"  stroke="blue"  stroke-width="3" fill="none" marker-end="url(#idArrow)" />

  

</svg>
  </div>
</template>

<script>
import Velocity from 'velocity-animate'
export default {
  name: 'diagram',
  props: ['user'],
  data () {
    return {
       
    }
  },
  methods: {
    
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
