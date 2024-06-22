<template>
    <div>
      <h1 class="text-4xl font-bold mb-4">{{ blog.title }}</h1>
      <img :src="blog.image.url" alt="blog image" class="mb-4">
      <div v-html="blog.content" class="prose"></div>
    </div>
  </template>
  
  <script>
  export default {
    async asyncData({ $axios, params }) {
      const { data } = await $axios.get(`/blog/${params.id}`, {
        headers: { 'X-API-KEY': process.env.apiKey }
      });
      return { blog: data };
    }
  }
  </script>