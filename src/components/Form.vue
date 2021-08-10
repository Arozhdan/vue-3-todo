<template>
  <form class="max-w-2xl rounded py-8 px-6 bg-white fixed left-1/2 top-1/2 shadow" style='transform: translate(-50%, -50%);' @submit.prevent='addComment'>
    <div class="mb-5 relative">
      <input v-model='email' type="email" id="email" class="peer pt-8 border border-gray-200 focus:outline-none rounded-md focus:border-gray-500 focus:shadow-sm w-full p-3 h-16 placeholder-transparent" placeholder="name@example.com" autocomplete="off" />
      <label for="email" class="peer-placeholder-shown:opacity-100   opacity-75 peer-focus:opacity-75 peer-placeholder-shown:scale-100 scale-75 peer-focus:scale-75 peer-placeholder-shown:translate-y-0 -translate-y-3 peer-focus:-translate-y-3 peer-placeholder-shown:translate-x-0 translate-x-1 peer-focus:translate-x-1 absolute top-0 left-0 px-3 py-5 h-full pointer-events-none transform origin-left transition-all duration-100 ease-in-out">Email address</label>
    </div>
    <div class="mb-5 relative">
      <input v-model='name' type="text" id="password" class="peer pt-8 border border-gray-200 focus:outline-none rounded-md focus:border-gray-500 focus:shadow-sm w-full p-3 h-16 placeholder-transparent" placeholder="name" autocomplete="off" />
      <label for="password" class="peer-placeholder-shown:opacity-100   opacity-75 peer-focus:opacity-75 peer-placeholder-shown:scale-100 scale-75 peer-focus:scale-75 peer-placeholder-shown:translate-y-0 -translate-y-3 peer-focus:-translate-y-3 peer-placeholder-shown:translate-x-0 translate-x-1 peer-focus:translate-x-1 absolute top-0 left-0 px-3 py-5 h-full pointer-events-none transform origin-left transition-all duration-100 ease-in-out">Name</label>
    </div>
    <div class="mb-5 relative">
      <input v-model='postId' type="text" id="1" class="peer pt-8 border border-gray-200 focus:outline-none rounded-md focus:border-gray-500 focus:shadow-sm w-full p-3 h-16 placeholder-transparent" placeholder="post id" autocomplete="off" />
      <label for="1" class="peer-placeholder-shown:opacity-100   opacity-75 peer-focus:opacity-75 peer-placeholder-shown:scale-100 scale-75 peer-focus:scale-75 peer-placeholder-shown:translate-y-0 -translate-y-3 peer-focus:-translate-y-3 peer-placeholder-shown:translate-x-0 translate-x-1 peer-focus:translate-x-1 absolute top-0 left-0 px-3 py-5 h-full pointer-events-none transform origin-left transition-all duration-100 ease-in-out">Post Id</label>
    </div>
    <div class="mb-5 relative">
      <input v-model='body' type="text" id="2" class="peer pt-8 border border-gray-200 focus:outline-none rounded-md focus:border-gray-500 focus:shadow-sm w-full p-3 h-16 placeholder-transparent" placeholder="password" autocomplete="off" />
      <label for="2" class="peer-placeholder-shown:opacity-100   opacity-75 peer-focus:opacity-75 peer-placeholder-shown:scale-100 scale-75 peer-focus:scale-75 peer-placeholder-shown:translate-y-0 -translate-y-3 peer-focus:-translate-y-3 peer-placeholder-shown:translate-x-0 translate-x-1 peer-focus:translate-x-1 absolute top-0 left-0 px-3 py-5 h-full pointer-events-none transform origin-left transition-all duration-100 ease-in-out">body</label>
    </div>
    <button class="w-full bg-indigo-600 text-white p-3 rounded-md">Submit</button>
  </form>
</template>

<script lang='ts'>
  import { defineComponent } from 'vue'
  import axios from 'axios'
  import { IComment } from '../App.vue'

  export default defineComponent ( {
    name: 'Form',
    data:()=>({
      email:'',
      postId:'',
      body:'',
      name:''
    }),
    methods:{
      addComment(){
        const comment:IComment = {
          postId: +this.postId,
          id: Date.now(),
          name: this.name,
          email: this.email,
          body: this.body
        }
        axios.post('https://jsonplaceholder.typicode.com/comments', comment).then((response)=>{
          this.$emit('newComment', response.data)
        })
      }
    }
  })
</script>

