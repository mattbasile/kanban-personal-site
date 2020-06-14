<template>
  <div>
    <div v-for="(column, index) in columns" :key="index" class="h-24 border w-full my-2 mx-auto border-blue-500">
       <h2><span>{{column.emoji}}</span> {{column.title}}</h2>
    </div>
  </div>
</template>

<script>
export default {
  props:[ 'columns' ]
}
</script>