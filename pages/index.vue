<template>
  <div class="container mx-auto px-3 py-4">
    <div v-if="posts" class="flex flex-row flex-wrap -m-3">
      <div class="w-12/12 lg:w-8/12 p-3">
        <div v-for="(item, i) in posts" :key="i" class="flex -m-2">
          <div class="w-4/12 p-1 lg:w-3/12">
            <picture v-if="item.featured_image">
              <source
                media="(max-width: 799px)"
                :srcset="`${item.featured_image}?resize=480,360`"
              />
              <source
                media="(min-width: 800px)"
                :srcset="`${item.featured_image}?resize=920,690`"
              />
              <img
                :src="`${item.featured_image}?resize=920,690`"
                :alt="item.title"
                class="w-full"
              />
            </picture>
            <picture v-else>
              <img
                src="https://images.unsplash.com/photo-1558000143-a78f8299c40b?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=750&q=80"
              />
            </picture>
          </div>
          <div class="flex flex-col justify-center p-1 w-8/12 lg:w-9/12 pb-2">
            <div>
              <h2 class="sm:text-xl lg:text-3xl font-serif">
                <nuxt-link
                  :to="`/read/${item.slug}`"
                  class="hover:text-red-600"
                  >{{ item.title }}</nuxt-link
                >
              </h2>
            </div>
            <div>
              <span
                v-for="(item, i) in item.categories"
                :key="i"
                class="uppercase text-sm text-red-600"
              >
                {{ item.name }}
              </span>
              <span class="text-sm italic text-gray-700">{{
                newDate(item.date)
              }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-else-if="error">{{ error.message }}</div>
    <div v-else>Loading...</div>
  </div>
</template>

<script>
const moment = require('moment')
export default {
  data() {
    return {
      posts: null,
      error: null,
    }
  },
  async fetch() {
    const item = await fetch(
      'https://public-api.wordpress.com/rest/v1.1/sites/foldsquare.wordpress.com/posts/'
    )
      .then((res) => res.json())
      .catch((err) => {
        this.error = err
      })
    this.posts = item.posts
    console.log(item.posts)
  },
  methods: {
    newDate(date) {
      const datenew = moment(date).locale('id').format('dddd, MMM YYYY')
      return datenew
    },
    itCat(item) {
      return item.name
    },
  },
}
</script>
