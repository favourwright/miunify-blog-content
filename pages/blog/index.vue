<template>
  <main class="min-h-screen bg-gray-100">
    <section>
      <header
        class="flex justify-between items-center px-[10%]
        h-[90px] bg-white/80 fixed top-0 left-0 right-0
        backdrop-blur-lg">
        <div
          class="tracking-[.3em] hover:tracking-[.36em] select-none
          transition-all duration-300 font-black text-xl">
          MIUNIFY.
        </div>
        <nav>
          <ul class="flex leading-tight gap-2 text-sm font-medium text-gray-300">
            <li class="px-6 text-gray-700">BLOG</li>
            <li class="px-6">ABOUT</li>
            <li class="px-6">CONTACT</li>
          </ul>
        </nav>
      </header>
      <div id="landing" class="h-screen px-[10%] flex flex-col justify-center">
        <h1 
          class="text-outline text-[120px] font-extrabold
          tracking-wide text-gray-700 text-right select-none">
          Mi<span class="text-gray-100">unify</span>.
        </h1>
        <p class="text-gray-400 font-light text-3xl text-right">
          A collection of blog posts about consistency & stuff.
        </p> 
      </div>
    </section>
    <section class="articles px-[10%]">
      <Articles />
      <ContentList path="/blog" v-slot="{ list }">
        <div v-for="article in list" :key="article._path">
          {{article.title}}
          <!-- <h2>{{ article.title }}</h2> -->
          <!-- <p>{{ article.description }}</p> -->
        </div>
      </ContentList>
    </section>
  </main>
</template>

<script setup>
import Articles from '../../componenets/Articles'
</script>

<style>
#landing::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: -1;
  background:red;

}
.text-outline{
  text-shadow:
    -1px -1px 0 rgb(55, 65, 81),
    1px -1px 0 rgb(55, 65, 81),
    -1px 1px 0 rgb(55, 65, 81),
    1px 1px 0 rgb(55, 65, 81);
}
</style>
