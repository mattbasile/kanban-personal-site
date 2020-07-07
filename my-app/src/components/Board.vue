<template>
<section>
  <div class="flex flex-wrap justify-between w-4/5 mx-auto items-center">
    <div class="flex flex-wrap items-center justify-between w-full">
      <h1 class="text-5xl font-semibold">Matt’s Board</h1>
      <div class="flex flex-wrap items-baseline lg:ml-4 mb-4 md:mb-0">
        <p class="font-hairline text-xl mr-4">Filter by:</p>
        <button v-for="(item, index) in filterButtons" :key="index" :name="item" @click="setActiveFilter($event)" :class="[activeFilter === item ? 'selected' : '', 'mx-2 mt-2 px-4 rounded font-medium']">
          {{item}}
        </button>
      </div>
    </div>
    <!-- List View v Board View toggle -->
    <!-- <div class="flex font-bold text-2xl">
      <p @click="selectedBoardView=true" :class="[selectedBoardView ? 'underline' : '', 'mr-2 cursor-pointer']">Board</p>
      <p @click="selectedBoardView=false" :class="[!selectedBoardView ? 'underline' : '', 'cursor-pointer']">List</p>
    </div> -->
  </div>
   <div class="flex w-4/5 mx-auto flex-wrap mt-6" v-if="selectedBoardView">
     <div v-for="(column, index) in columns" :key="index" class="h-auto w-full lg:w-1/4 lg:px-1 my-4">
        <h2 class="font-black text-xl"><span>{{column.emoji}}</span> {{column.title}}</h2>
        <div v-for="(card, index) in column.cards" 
        :key="index" 
        :class="[card.tags[0] === 'product' ? 'border-purple-200' : card.tags[0] === 'code' ? 'border-green-200' : card.tags[0] === 'contact' ? 'border-orange-200' : card.tags[0] === 'teaching' ? 'border-blue-200' : 'border-red-200']"
        class="bg-white border-l-8 w-full rounded my-4 cursor-pointer hover:shadow-xl">
          <div @click="setModalContent(card)" class="p-2 flex">
            <div class="w-3/4 lg:w-full">
              <p class="font-semibold mb-2 text-lg">{{card.title}}</p>
              <p class="text-sm hidden lg:block">{{truncateText(card.short_blurb)}}</p>
              <div class="flex flex-wrap lg:justify-between items-center mt-2">
                <div class="flex items-center mt-1">
                  <div v-if="card.company === 'Matt Basile'" style="font-size: 6px;" class="bg-blue-800 flex h-4 items-center justify-center rounded-full text-white w-4">
                    MB
                  </div>
                  <div v-else-if="card.company === 'Trivia Now!'" class="bg-indigo-500 flex font-semibold h-4 items-center justify-center rounded-full text-white w-4">
                    !
                  </div>
                  <img v-else-if="card.company === 'Monax'" :src="Monax_Logo" class="flex h-4 w-4 items-center justify-center rounded-full text-blue-800 "/>
                  <img v-else-if="card.company === 'Lambda School'" :src="Lambda_Logo" class="flex h-4 w-4 items-center justify-center rounded-full text-blue-800 "/>
                  <img v-else-if="card.company === 'European Watch Co.'" :src="EWC_Logo" class="flex h-4 w-4 items-center justify-center rounded-full text-blue-800 "/>
                  <img v-else-if="card.company === 'America on Tech'" :src="AOT_Logo" class="border-gray-200 border flex h-4 w-4 items-center justify-center rounded-full text-blue-800 "/>
                  <img v-else :src="NBA_Logo" class="border-gray-200 border flex h-4 w-4 items-center justify-center rounded-full text-blue-800 "/>
                  <p class="ml-1 text-xs font-semibold text-blue-800">{{card.company}}</p>
                </div>
                <div class="flex items-baseline lg:ml-0 ml-2 mt-1 text-gray-500 text-xs">
                  <i class="far fa-calendar-alt"></i>
                  <p class="ml-1">{{card.dates}}</p>
                </div>
              </div>
            </div>
             <p class="flex items-center justify-end lg:hidden w-1/4 underline text-blue-900 font-semibold">
                See More
              </p>
          </div>
        </div>
     </div>
   </div>
  <list class="w-4/5 mx-auto" v-else v-bind:columns="columns"></list>
  <modal v-if="toggleModal" v-bind:content="selectedModal" v-bind:closeModal="closeModal"></modal>
</section>
</template>

<script>
import columns from "../assets/info.json";
import List from "./List";
import Modal from "./Modal"
export default {
  components: {
    List,
    Modal
  },
  data: function() {
    return {
        filterButtons:['Contact', 'Code', 'Product', 'Teaching'],
        activeFilter: '',
        selectedBoardView: true,
        columns: columns.columns,
        Monax_Logo: require('@/assets/Monax.png'),
        Lambda_Logo: require('@/assets/Lambda.png'),
        EWC_Logo: require('@/assets/EWC.png'),
        AOT_Logo: require('@/assets/AOT.png'),
        NBA_Logo: require('@/assets/NBA.png'),
        toggleModal: false,
        selectedModal: '',
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
    },
    truncateText(blurb) {
      if (blurb.length > 150) {
        return blurb.substr(0, 150) + '...';
      }else{
        return blurb;
      }
    },
    setModalContent(card){
      console.log(card);
      this.toggleModal = true;
      this.selectedModal = card;
    },
    closeModal(){
      this.toggleModal = false;
      this.selectedModal = '';
    }
  }
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