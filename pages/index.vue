<template>
  <div>
    <h1 class="text-4xl font-bold mb-8">Blog</h1>
    <div v-if="blogs.length">
      <ul class="space-y-4">
        <li v-for="blog in blogs" :key="blog.id" class="p-4 border rounded-lg shadow-sm">
          <h1><nuxt-link :to="'/blog/' + blog.id" class="text-2xl text-blue-600 hover:underline">
            {{ blog.title }}
          </nuxt-link></h1>

          <p class="mt-2 text-gray-600">{{ blog.summary }}</p>
          <p>{{ blog.content }}</p>
          var url = {{ blog.thumbnail.url }};
          

        </li>
      </ul>
    </div>
    <div v-else>
      <p>No blogs found</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blogs: []
    };
  },
  async fetch() {
    const { data } = await this.$axios.get('/blog', {
      headers: { 'X-MICROCMS-API-KEY': process.env.apiKey }
    });
    this.blogs = data.contents;
  }
}
</script>
