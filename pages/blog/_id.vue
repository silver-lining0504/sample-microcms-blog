<template>
  <div>
    <h1 class="text-4xl font-bold mb-8">Blog Detail</h1>
    <div v-if="blog">
      <h2 class="text-2xl text-blue-600">{{ blog.title }}</h2>
      <div v-html="convertPToBr(blog.content)"></div>
    </div>
    <div v-else>
      <p v-if="error">Error loading blog: {{ error.message }}</p>
      <p v-else>Loading...</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blog: null,
      error: null,
    };
  },
  methods: {
    convertPToBr(content) {
      return content.replace(/<\/p>/g, '<br>').replace(/<p>/g, '');
    }
  },
  async fetch() {
    const blogId = this.$route.params.id;
    console.log('Fetching blog ID:', blogId);

    try {
      const { data } = await this.$axios.get(`/blog/${blogId}`, {
        headers: { 'X-MICROCMS-API-KEY': process.env.apiKey }
      });
      console.log('Fetched blog data:', data);
      this.blog = data;
    } catch (error) {
      console.error('Error fetching blog:', error);
      this.error = error;
    }
  }
}
</script>

<style>
/* You can add custom styles here if needed */
</style>
