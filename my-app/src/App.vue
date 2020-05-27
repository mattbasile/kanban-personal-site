<template>
  <section class="bg-blue-100">
    <nav class="flex px-8 h-20 justify-between items-center">
      <p class="text-2xl font-black text-blue-900">MB</p>
      <div class='flex items-center'>
        <p class="mr-4 font-semibold text-blue-900">Product and Engineering</p>
        <img class="rounded-full" src='./assets/Matts_pro.png' alt="Profile Image of Matt Basile"/>
      </div>
    </nav>
    <board></board>
  </section>
</template>

<script>
import Board from './components/Board.vue'
import cards from "./assets/info.json";

export default {
  name: 'App',
  components: {
    Board
  },
  data:function(){
    return{
      rowss:cards.cards,
    }
  }
}
</script>

<style>
  @import 'https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css';
  @import './styles/main.css';
</style>
