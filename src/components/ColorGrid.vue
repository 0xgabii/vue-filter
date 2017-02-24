<template>
  <transition-group tag="div" class="color-grid" name="color-grid">
    <div 
      class="color-box" 
      v-for="item in gridItems"
      :key="item"
      :style="{backgroundColor: item.color}">
      <div class="text-box">
        <span class="type">{{item.type}}</span>
        <span class="color">{{item.color}}</span>
      </div>        
    </div>
  </transition-group>    
</template>

<script>
export default {
  name:'colorgrid',
  props:['gridItems']
}
</script>

<style scoped>
  /* transition-group CSS */
  .color-grid-enter,
  .color-grid-leave-to{
    opacity: 0;
    transform: scale(0.5);
  }
  .color-grid-leave-active {
    position: absolute;
  }
  /* template CSS */
  .color-grid{    
    position: relative;    
  }
  .color-box{
    display: inline-block;    
    margin: 1rem;
    width: calc(20% - 2rem);
    height: 8.5rem;    
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
    transition: all 0.75s;
  }
  .text-box{
    position: relative;
    width: 100%;
    height: 100%;
  }
  .text-box > span{
    display: block;
    position: absolute;
    color: white;    
  }
  .type{
    left: 5%;
    top: 8%;
    margin-bottom: 0.5rem;
    font-size: 1.25rem; 
    text-transform: capitalize;    
  }
  .color{
    right: 5%;
    bottom: 6%;
    font-size: 1.3rem;
    text-transform: uppercase;    
  }
</style>