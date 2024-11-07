<template>
  <div class="pr-5">
    <Drawer />
  </div>
  <div class="container mx-auto max-w-4xl space-y-6 px-4 mb-20">
    <div class="mb-10">
      <NuxtLink :to="`/categories/${post.category}`">
        <span>
          <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24">
            <path fill="currentColor" d="m6.921 12.5l5.793 5.792L12 19l-7-7l7-7l.714.708L6.92 11.5H19v1z"></path>
          </svg>
        </span>
        <span class="text-xs tinos-regular">{{post.categoryTitle}}</span>
      </NuxtLink>
    </div>
    

    <ContentSlot>
      <h1 class="text-6xl font-bold road-rage-regular">{{ post.title }}</h1>
      <p class="text-3xl font-bold grenze text-neutral-300">{{ post.description }}</p>
    </ContentSlot>


    <ContentDoc v-slot="{ doc }">
      <article class="text-xl grenze">
        <ContentRenderer :value="doc" />
      </article>
    </ContentDoc>

    <div v-if="post.imagegallery && post.showgaller !=='false'">
      <ImageGallery />
    </div>
  </div>
</template>

<script setup>
import { useAsyncData, useRoute } from 'nuxt/app'

const route = useRoute()
const { data: post, error } = await useAsyncData('page', () =>
  queryContent(route.path.replace(/\/$/, '')).findOne()
)

// Handle loading or error states as needed
if (error.value) {
  console.error('Error fetching post:', error.value)
}
</script>
