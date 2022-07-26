<template>
  <div class="max-w-3xl mx-auto min-h-screen my-12 prose prose-gray dark:prose-invert">

    <div v-if="post">
      <h1 class="text-2xl font-semibold mb-6">{{ post.title }}</h1>
        <div class="flex">
          <span>{{ post.dateHuman }}</span>
          <span class="flex-grow"></span>
          <span class="">
            <span v-for="(tag, i) in post.tags" :key="i" class="ml-1 text-slate-500 text-sm">#{{ tag }}</span>
          </span>
        </div>
        <img :src="post.cover_image" alt="blog photographs" class=""/>
      <!-- <nuxt-content :document="post" /> -->
      <ContentDoc
        :path="$route.params.slug ? `/blog/${$route.params.slug[0]}` : '/blog'"
      >
        <template #not-found>
          <h2>Blog slug ({{ $route.params.slug }}) not found</h2>
        </template>
      </ContentDoc>
      <div class="mt-8">
        <nuxt-link to="/" class="hover:underline">Back to blog</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script setup>
const route=useRoute()
console.log('router', route.path, route.params)
const { data: post } = await useAsyncData('post', () => {
  // return queryContent(route.params.slug[0]).find()
  return queryContent().where({ _path: route.path }).findOne();
})
console.log('post',post)

  // export default {
  //   async setup({ $content, params }) {
  //     // const projects = useProjectsStore()
  //     const route=useRoute()
  //     console.log(route.params)
  //     const article = await $content(route.params.slug[0]).fetch()
  //     console.log(article)
  //     // const project = projects.projects.find((project) => project.id === route.params.id)

  //     // console.log(project);
  //     // return { project }
  //   },
  //   async asyncData({ $content, params }) {
  //     console.log($content, params)

  //     // return { article }
  //   }
  // }

// console.log($route.params)
// const { data: post } = await useAsyncData('blog-post', () => {
//   return queryContent('/blog')
//     // .sortBy("publishOn", "desc")
//     .find()
// })
// console.log(blogs)
// export default {
//   data() {
//     return {
//       post: null,
//     }
//   },
//   async fetch() {
//     this.post = (
//       await this.$content()
//         .where({ slug: this.$route.params.slug })
//         .limit(1)
//         .fetch()
//     )?.[0]
//   },
// }
</script>