<template>
  <div id="app">
    <header el="header" :style="{backgroundColor: headerColor}">
      <h1>{{ projectName }}</h1>      
      <h2>{{ projectIntroduce }}</h2>
    </header>    
    <div class="wrapper">
      <controller      
        :filterType="filterType"        
        :changeFilter="changeFilter"
        :changeSearch="changeSearch"
        :changeSort="changeSort"
        :doShuffle="doShuffle"
        :doAddItem="doAddItem"
      />
      <color-grid
        :gridItems="filteredItem"
      />
    </div>    
  </div>
</template>

<script>
import _ from 'lodash';

import Controller from './components/Controller'
import ColorGrid from './components/ColorGrid'

export default {
  name: 'app',
  data (){
    return {
      projectName: 'Vue-Filter',
      projectIntroduce: 'Search, filter and shuffle items',
      headerColor: '#f44336',
      filterType: [],
      search: '',
      gridItems: Array.apply(null, { length: 20 }).map((_, index) => {
        switch(index % 5){
          case 0: return {
            type: 'red',
            color: '#f44336'                    
          }; break;
          case 1: return {
            type: 'indigo',
            color: '#3F51B5'          
          }; break;
          case 2: return {
            type: 'lightblue',
            color: '#03A9F4'          
          }; break;
          case 3: return {
            type: 'green',
            color: '#4CAF50'          
          }; break;
          case 4: return {
            type: 'orange',
            color: '#FF9800'         
          }; break;
        }
      }),
    }
  },
  computed: {
    filteredItem(){      
      let filteredItem = this.gridItems;
      if(this.filterType.length) filteredItem = this.gridItems.filter(data => this.filterType.indexOf(data.type) != -1);
      if(this.search) filteredItem = filteredItem.filter(data => data.type.search(this.search) != -1 || data.color.search(this.search) != -1);      
      return filteredItem;
    }
  },
  methods: {
    changeFilter(filter){                  
      const filterTypeIdx= this.filterType.indexOf(filter.type);
      filterTypeIdx == -1 ? this.filterType.push(filter.type) : this.filterType.splice(filterTypeIdx, 1);      
      // header color change
      this.headerColor = filter.color;
    },
    changeSearch(e){
      this.search = e.target.value;
    },
    changeSort(sort){
      this.sort = sort;
    },
    randomIndex() {
      return Math.floor(Math.random() * this.gridItems.length); 
    }, 
    doShuffle() {
      this.gridItems = _.shuffle(this.gridItems);
    },
    doAddItem() {     
      this.gridItems.splice(this.randomIndex(), 0, _.cloneDeep(this.gridItems[this.randomIndex()]));
    }
  },
  components: {
    Controller,
    ColorGrid
  }     
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto');

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-weight: 300;
}
#app {
  width: 100vw;
  height: 100vh;
  overflow-x: hidden;
  overflow-y: scroll;
  font-family: 'Roboto', sans-serif;
  background-color: #FAFAFA;
}
header {
  position: relative;  
  padding: 1.5rem;  
  width: 100vw;  
  color: white;  
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
  transition: all 0.3s;
}
header > h1{    
  margin-bottom: 0.3rem;
  font-size: 2.5rem;
}
header > h2{   
  font-size: 1.25rem;
}
.wrapper{
  padding: 1rem;
}
</style>
