<template>
  <div class="controller">    
    <div class="filter-group">
      <button 
        v-for="filter in filters"
        @click="changeFilter(filter)"        
        :class="{active: filterType.indexOf(filter.type) != -1}"
        :style="{backgroundColor: filter.color}">
        {{ filter.type }}
      </button>
    </div>    
    <div class="search-group">
      <input 
        type="text" 
        @input="changeSearch"
        placeholder="Search something...">
    </div>
    <button @click="doShuffle">shuffle</button>
    <button @click="doAddItem">addItem</button>
  </div>
</template>

<script>
export default {
  name: 'filter',
  props: [
    'sort',
    'filterType',
    'changeFilter',
    'changeSearch',
    'changeSort',
    'doShuffle',
    'doAddItem'
  ],
  data () {
    return {
      filters: [
        {
          type: 'red',
          color: '#f44336'                    
        },
        {
          type: 'indigo',
          color: '#3F51B5'          
        },
        {
          type: 'lightblue',
          color: '#03A9F4'
        },
        {
          type: 'green',
          color: '#4CAF50'
        },
        {
          type: 'orange',
          color: '#FF9800'
        },
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .controller{
    display: flex;    
    align-items: center;
    padding: 0.5rem 1rem 1.5rem 1rem;
    margin-bottom: 0.5rem;
    border-bottom: 2.5px solid #dadada;
  }
  .controller > div{
    margin-right: 1.5rem;
  }
  .filter-group{
    display: flex;    
  }
  .filter-group > button{
    padding: 0.7rem 1.8rem;   
    margin: 0 0.15rem;
    border: none;     
    outline: none;
    color: white;    
    text-transform: capitalize;  
    border-radius: 2rem;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24); 
    transition: all 0.3s;
  }
  .filter-group > button:hover{
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  }
  .filter-group > button.active{    
    background-color: rgba(0,0,0,0.5) !important;
  }
  .search-group > input{    
    padding: 0.5rem 0.75rem;
    background-color: transparent;
    font-size: 1.25rem;
    border:none;
    border-bottom: 2.5px solid #dadada;
  }
  .search-group ~ button{
    padding: 0.7rem 1.8rem; 
    margin-right: 0.3rem;
    outline: none;
    border: none;
    border-radius: 0.3rem;
    color: white;        
    transition: all 0.3s;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24); 
  }
  .search-group ~ button:hover{
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  }
  .search-group ~ button:nth-of-type(1){
    background-color: #9c27b0;
  }
  .search-group ~ button:nth-of-type(2){
    background-color: #673ab7;
  }
</style>
