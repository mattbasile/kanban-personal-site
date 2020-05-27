<template>
  <div class="flex justify-between w-4/5 mx-auto items-center">
    <div class="flex items-center">
      <h1 class="text-5xl font-semibold">Matt’s Board</h1>
      <div class="flex ml-4">
        <p class="font-hairline text-xl mr-4">Filter by:</p>
        <button v-for="(item, index) in filterButtons" :key="index" :name="item" @click="setActiveFilter($event)" :class="[activeFilter === item ? 'selected' : '', 'mx-2 px-4 rounded font-medium']">
          {{item}}
        </button>
      </div>
    </div>
    <div class="flex font-bold text-2xl">
      <p @click="selectedBoardView=true" :class="[selectedBoardView ? 'underline' : '', 'mr-2 cursor-pointer']">Board</p>
      <p @click="selectedBoardView=false" :class="[!selectedBoardView ? 'underline' : '', 'cursor-pointer']">List</p>
    </div>
  </div>
</template>

<script>
export default {
data: function() {
  return {
      filterButtons:['Contact', 'Code', 'Product', 'Teaching'],
      activeFilter: '',
      selectedBoardView: true,
    }
  },
methods: {
  setActiveFilter(e){
    let click_target = e.target.name;
    if(click_target=== this.activeFilter ){
      this.activeFilter = '';
    }else{
      this.activeFilter = click_target;
    }
  }
},
}
</script>
<style scoped>
  button[name='Contact']{
    background: #FEEBC8;
    color: #DD6B20;
  }
  button[name='Contact'].selected{
    color: #FEEBC8;
    background: #DD6B20;
  }
  button[name='Code']{
    background: #C6F6D5;
    color: #38A169;
  }
  button[name='Code'].selected{
    color: #C6F6D5;
    background: #38A169;
  }
  button[name='Product']{
    background: #E9D8FD;
    color: #805AD5;
  }
  button[name='Product'].selected{
    color: #E9D8FD;
    background: #805AD5;
  }
  button[name='Teaching']{
    background: #BEE3F8;
    color: #3182CE;
  }
  button[name='Teaching'].selected{
    color: #BEE3F8;
    background: #3182CE;
  }
  .selected{
    font-weight: 900;
  }
</style>