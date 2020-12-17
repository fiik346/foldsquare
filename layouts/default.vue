<template>
  <div>
    <a href="#" class="sr-only focus:not-sr-only focus:bg-gray-900 text-white">
      Skip to content
    </a>
    <nav class="bg-white shadow sticky top-0 lg:static">
      <div id="search" :class="search ? 'top-0' : '-top-full'">
        <div class="container search">
          <form class="flex">
            <input
              id="searchinput"
              type="search"
              autocomplete="off"
              name="q"
              class="w-full px-4 py-2 rounded-full bg-gray-200 focus:outline-none"
              placeholder="Search.."
            />
          </form>
          <div class="mt-4">
            <ul>
              <li>
                <a
                  class="block rounded hover:bg-gray-100 focus:bg-gray-200 py-2 px-4 font-serif"
                  href="/"
                  >Lorem Ipsum Dolor Sit Amet</a
                >
              </li>
              <li>
                <a
                  class="block rounded hover:bg-gray-100 focus:bg-gray-200 py-2 px-4 font-serif"
                  href="/"
                  >Lorem Ipsum Dolor Sit Amet</a
                >
              </li>
            </ul>
          </div>
          <button
            class="shadow bg-white p-2 absolute right-4 top-4 lg:right-8 lg:top-8 rounded-full"
            @click="searchF()"
          >
            <svg class="toggleIcon" viewBox="0 0 24 24">
              <path
                d="M19,6.41L17.59,5L12,10.59L6.41,5L5,6.41L10.59,12L5,17.59L6.41,19L12,13.41L17.59,19L19,17.59L13.41,12L19,6.41Z"
              />
            </svg>
          </button>
        </div>
        <div
          :class="search ? 'show' : ''"
          class="sbg"
          aria-label="Close Search Box"
          @click="searchF()"
        ></div>
      </div>
      <div class="container header">
        <button
          :aria-expanded="menu ? 'true' : 'false'"
          aria-controls="#menu"
          aria-label="Open Menu"
          class="-ml-1 p-1 focus:outline-none lg:hidden"
          @click="menuF()"
        >
          <svg
            class="toggleIcon hamburger"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="m3 5v2h18v-2h-18zm0 6v2h18v-2h-18zm0 6v2h10.775v-2h-10.775z"
            />
          </svg>
          <svg class="toggleIcon close" viewBox="0 0 24 24">
            <path
              d="M19,6.41L17.59,5L12,10.59L6.41,5L5,6.41L10.59,12L5,17.59L6.41,19L12,13.41L17.59,19L19,17.59L13.41,12L19,6.41Z"
            />
          </svg>
        </button>
        <div class="mx-auto lg:ml-0">
          <nuxt-link to="/" class="text-2xl font-serif font-bold"
            ><LazyLogo
          /></nuxt-link>
        </div>
        <div class="hidden lg:flex">
          <ul class="flex">
            <li v-for="(item, i) in sosmed" :key="i" class="px-2">
              <a
                :href="item.href"
                class="text-black uppercase font-bold text-sm hover:text-red-600"
                >{{ item.title }}</a
              >
            </li>
          </ul>
        </div>
        <label
          role="button"
          for="searchinput"
          class="-mr-1 p-1 focus:outline-none"
          aria-controls="#search"
          aria-label="Search Box Toggle"
          @click="searchF()"
        >
          <svg class="toggleIcon" viewBox="0 0 24 24">
            <path
              d="M9.5,3A6.5,6.5 0 0,1 16,9.5C16,11.11 15.41,12.59 14.44,13.73L14.71,14H15.5L20.5,19L19,20.5L14,15.5V14.71L13.73,14.44C12.59,15.41 11.11,16 9.5,16A6.5,6.5 0 0,1 3,9.5A6.5,6.5 0 0,1 9.5,3M9.5,5C7,5 5,7 5,9.5C5,12 7,14 9.5,14C12,14 14,12 14,9.5C14,7 12,5 9.5,5Z"
            />
          </svg>
        </label>
      </div>
    </nav>
    <nav
      id="menu"
      :aria-hidden="menu ? 'false' : 'true'"
      :class="menu ? 'left-0' : '-left-full'"
    >
      <ul
        class="container mx-auto flex flex-wrap lg:flex-nowrap lg:overflow-auto"
      >
        <li v-for="(item, i) in nav" :key="i" class="w-6/12 lg:w-max">
          <nuxt-link :to="item.to" class="nav-link">{{ item.title }}</nuxt-link>
        </li>
      </ul>
      <div class="container mx-auto mt-3 lg:hidden">
        <span class="text-white text-sm uppercase font-bold block px-3"
          >Connect With Us
          <i
            class="absolute inline-block animate-ping w-1.5 h-1.5 absolute rounded-full bg-red-700"
          ></i
        ></span>
        <ul class="flex mt-1 flex-wrap">
          <li v-for="(item, i) in sosmed" :key="i" class="w-6/12">
            <a
              :href="item.href"
              class="text-white text-sm uppercase font-bold block px-3 py-1 hover:bg-gray-900 focus:bg-gray-800"
              >{{ item.title }}</a
            >
          </li>
        </ul>
      </div>
    </nav>
    <Nuxt />
  </div>
</template>

<style lang="scss">
.toggleIcon {
  height: 24px;
  width: 24px;
  fill: #000;
}
[aria-expanded='true'] {
  .hamburger {
    display: none;
  }
}
[aria-expanded='false'] {
  .close {
    display: none;
  }
}
#menu {
  @apply fixed;
  @apply w-full;
  @apply bg-black;
  @apply transition-all;
  @apply top-16;
  @apply py-2;
  @apply lg:sticky;
  @apply lg:top-0 lg:py-0;
}
.header {
  @apply h-16;
  @apply mx-auto;
  @apply flex;
  @apply items-center;
  @apply px-3;
}
#search {
  @apply fixed;
  @apply z-20;
  @apply left-0;
  @apply w-full;
  @apply px-3;
  @apply h-full;
  @apply transition-all;
}
.search {
  @apply z-10 relative mt-4 mx-auto max-w-lg p-4 lg:p-8 bg-white rounded;
  max-height: calc(100vh - 4rem);
}
.sbg {
  @apply absolute;
  @apply h-full;
  @apply top-0;
  @apply left-0;
  @apply w-full;
}
.show.sbg {
  @apply transition;
  @apply delay-150;
  @apply bg-black;
  @apply z-0;
  @apply opacity-25;
}
.nav-link {
  @apply text-white text-sm uppercase font-bold block px-3 py-1 hover:bg-gray-900 focus:bg-gray-800 lg:bg-transparent lg:hover:bg-transparent lg:focus:bg-transparent lg:py-3 lg:hover:text-red-600;
}
</style>

<script>
export default {
  data() {
    return {
      menu: false,
      search: false,
      nav: [
        {
          title: 'Home',
          to: '/',
        },
        {
          title: 'Portal',
          to: '/portal',
        },
        {
          title: 'Life Style',
          to: '/life',
        },
      ],
      sosmed: [
        { title: 'Facebook', href: 'https://fb.com' },
        { title: 'Twitter', href: 'https://twitter.com' },
        { title: 'Github', href: 'https://github.com/fik346' },
      ],
    }
  },
  methods: {
    menuF() {
      this.menu = !this.menu
    },
    searchF() {
      this.search = !this.search
      this.menu = false
    },
  },
}
</script>
