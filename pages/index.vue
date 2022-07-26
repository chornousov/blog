<template>
  <div
    class="max-w-3xl max-w-5xlmin-h-screen flex justify-center mx-auto mt-4"
  >
    <main class="w-full">
      <h1 class="text-2xl font-semibold mb-6">My awesome blog</h1>
      <!-- <section class="space-y-4 divide-y">
        <article v-for="post of posts" :key="post.slug" class="pt-4">
          <h2 class="text-lg mb-2 text-blue-700 hover:text-blue-800">
            <nuxt-link :to="`/blog/${post.slug}`">
              {{ post.title }}
            </nuxt-link>
          </h2>
          <span>
            {{ post.description }}
          </span>
        </article>
      </section> -->

      <article 
        v-for="blog in blogs" :key="blog.slug + blog.createdAt"
        class="pb-4"
      >
        <h2 class="text-lg mb-2 text-blue-700 hover:text-blue-800">
          <nuxt-link :to="`${blog._path}`">{{ blog.title }}</nuxt-link>          
        </h2>
        <div>
          <div class="flex">
            <span>{{ blog.dateHuman }}</span>
            <span class="flex-grow"></span>
            <span class="">
              <span v-for="(tag, i) in blog.tags" :key="i" class="ml-1 text-slate-500 text-sm">#{{ tag }}</span>
            </span>
          </div>
        </div>
        <img :src="blog.cover_image" alt="blog photographs" class=""/>
        <p>{{ blog.description.substring(0, 150) }}...</p>
        <button>
          <nuxt-link :to="`${blog._path}`" class="hover:underline">Read More</nuxt-link>
        </button>
      </article>
    </main>
  </div>
</template>

<script setup>
console.log('start')
const { data: blogs } = await useAsyncData('blog-posts', () => {
  return queryContent('/blog')
    .sort({date: -1})
    .find()
})
console.log(blogs)
console.log('finish')
</script>