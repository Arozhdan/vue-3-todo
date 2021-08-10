<template>
  <Table @delete-comment='deleteComment' :comments='comments'/>
  <Form v-if='formIsVisible' @new-comment='newComment' />
  <button @click='formIsVisible=!formIsVisible' class='w-12 h-12 bg-purple-300 rounded-full shadow text-white fixed right-4 bottom-4 hover:shadow-2xl hover:bg-purple-400 transition duration-300  '>x</button>
</template>

<script lang="ts">
  import { defineComponent, ref } from 'vue'
  import Table from '@/components/Table.vue'
  import Form from '@/components/Form.vue'
  import axios from 'axios'

  export interface IComment {
    postId: number;
    id: number;
    name: string;
    email: string;
    body: string;
  }
  export default defineComponent({
    name: 'App',
    components: {Table, Form},
    data:()=>({
      formIsVisible:false
    }),
    setup() {
      const comments = ref<IComment[]>([])
      const err = ref('')
      axios.get<IComment[]>('https://jsonplaceholder.typicode.com/comments?_limit=10').then(response => comments.value = response.data).catch(e => err.value = e)

      const deleteComment = (id:number) => {
        axios.delete(`https://jsonplaceholder.typicode.com/comments/${id}`).then( ()=>{
            comments.value = comments.value.filter((el:IComment)=> el.id !== id)
          }
        ).catch(e=> err.value = e)
      }
      const newComment = (comment:IComment) => {
        comments.value.unshift(comment)
      }

      return { comments, deleteComment,newComment ,err }
    }

  })
</script>

