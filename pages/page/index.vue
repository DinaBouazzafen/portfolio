<template>
  <div>
    <div class="pr-5">
      <Drawer />
    </div>
    <main class="mx-auto max-w-4xl space-y-6 px-4 mb-20">
      <div class="text-7xl font-bold roboto-black">
        Hi, I am Dina!
      </div>

      <div class="text-xl grenze">
        As a student of Graphic Design: Media and Information Design, and a recent graduate with a Bachelor's degree in Multimedia and Creative Technologies, my journey has focused on blending art and technology. I'm passionate about crafting dynamic visual experiences through graphic, motion, and interactive design, always exploring new ways to push creative boundaries and bring ideas to life.
      </div>

      <!-- Categories displayed as masonry layout -->
      <div class="masonry mt-10">
        <div 
          class="masonry-item" 
          v-for="category in categories" 
          :key="category.slug"
        >
          <!-- Link to the specific category page -->
          <NuxtLink :to="`/categories/${category.slug}`" class="block">
            <!-- Category thumbnail -->
            <div class="masonry-image">
              <NuxtImg
                :src="category.thumbnail"
                alt="Category thumbnail"
                class="w-full h-64 object-cover rounded-md mb-4"
                :width="750"
                :height="550"
              />
            </div>
            <!-- Category title and description -->
            <div class="masonry-item-text p-4">
              <h2 class="text-3xl font-semibold mb-2 road-rage-regular">{{ category.title }}</h2>
              <p v-if="category.description" class="text-gray-300 line-clamp-3 text-xl grenze">{{ category.description }}</p>
            </div>
          </NuxtLink>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
const categories = [
  {
    title: 'Mixed Media',
    slug: 'mixed-media',
    description: 'Explore works that blend various artistic mediums.',
    thumbnail: '/img/ptsdex_ffhh-copy.png',
  },
  {
    title: 'Graphic Design',
    slug: 'graphic-design',
    description: 'Showcasing innovative graphic design projects.',
    thumbnail: '/img/screenshot-2024-08-26-at-18.22.28.png',
  },
  {
    title: 'Motion',
    slug: 'motion',
    description: 'Dynamic motion design projects that push the boundaries.',
    thumbnail: '/img/daydream.png',
  },
  {
    title: 'Random Works',
    slug: 'random-works',
    description: 'A collection of miscellaneous creative projects.',
    thumbnail: '/img/3d-eyes.png',
  }
];
</script>

