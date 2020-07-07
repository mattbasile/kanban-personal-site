<template>
  <div class="w-screen h-screen z-10 absolute top-0 flex items-center justify-center">
    <div class="w-4/5 p-12 bg-white mx-auto rounded-lg h-full fixed" style="height: calc(100% - 15%)">
      <div class="flex justify-between w-full">
        <p class="text-4xl font-semibold text-blue-main">{{content.title}}</p>
        <span @click="closeModal" class="font-black text-gray-500 text-5xl cursor-pointer hover:text-red-800" style="transform: rotate(45deg);">+</span>
      </div>
      
    </div>
  </div>
</template>

<script>
export default {
  props: {
    content: Object,
    closeModal: Function,
  }
}
</script>
