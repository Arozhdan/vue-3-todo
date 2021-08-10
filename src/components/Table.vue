<template>
  <table class='rounded-t-lg m-5 w-5/6 mx-auto bg-gray-800 text-gray-200' v-if='comments && comments.length'>
    <tr class='text-left border-b border-gray-300'>
      <th class='px-4 py-3'>Name</th>
      <th class='px-4 py-3'>Email</th>
      <th class='px-4 py-3'>Body</th>
      <th class='px-4 py-3'>Phone</th>
    </tr>
    <tr v-for='comment in comments' :key='comment.id + Date.now()' class='bg-gray-700 border-b border-gray-600'>
      <td class='px-4 py-3'>{{ comment.name }}</td>
      <td class='px-4 py-3'>{{ comment.email }}</td>
      <td class='px-4 py-3'>{{ comment.body }}</td>
      <td class='px-4 py-3'><button class='px-4 py-2 rounded bg-purple-900' @click="$emit('deleteComment', comment.id )">Delete</button></td>
    </tr>
  </table>
</template>
<script lang='ts'>

  import { defineComponent, PropType } from 'vue'
  import { IComment } from '@/App.vue'
export default defineComponent({
  props:{
    comments:{
      type:Array as PropType<IComment[]>
    }
  }
})
</script>