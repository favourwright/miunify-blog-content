<template>
  <main class="min-h-screen bg-gray-100">
    <section>
      <header
        class="flex justify-between items-center px-[4%] xl:px-[10%]
        h-[60px] md:h-[90px] bg-neutral-700 md:bg-white/80 md:fixed top-0 left-0 right-0 transition-all duration-300
        backdrop-blur-lg z-40">
        <div
          class="tracking-[.3em] hover:tracking-[.36em] select-none
          transition-all duration-300 font-black text-xl
          text-white md:text-amber-900">
          MIUNIFY.
        </div>
        <nav>
          <ul class="hidden md:flex leading-tight gap-2 text-sm font-medium text-gray-300">
            <li class="px-6 text-gray-700">BLOG</li>
            <li class="px-6">ABOUT</li>
            <li class="px-6">CONTACT</li>
          </ul>
        </nav>
      </header>
      <div id="landing" class="h-screen px-[4%] xl:px-[10%] flex flex-col justify-center">
        <h1 
          class="text-[20vw] md:text-[120px] font-extrabold
          tracking-wide text-neutral-700 text-right select-none">
          Mi<span class="text-neutral-100 text-outline">unify</span>.
        </h1>
        <p class="text-amber-900 font-light text-3xl text-right">
          A collection of blog posts about consistency & stuff.
        </p> 
      </div>
    </section>
    <section class="articles px-[4%] xl:px-[10%] flex flex-col gap-10">
      <Article
        title="Writing A Novel with A Heart"
        description="Far far away, behind the word mountains, far from the countries Vokalia and Consonantia, there live the blind texts. Separated they live in Bookmarksgrove right at the coast of the Semantics, a large language ocean."
        bg="ximage_1.jpg.pagespeed.ic.MUxtZlUbLa.webp" />
      <Article
        title="The Only Way To Learn Is To Learn"
        description="Far far away, behind the word mountains, far from the countries Vokalia and Consonantia, there live the blind texts. Separated they live in Bookmarksgrove right at the coast of the Semantics, a large language ocean."
        bg="ximage_3.jpg.pagespeed.ic.dNvGCQOnGy.webp" />
      <Article
        title="The Only Way To Learn Is To Learn"
        description="Far far away, behind the word mountains, far from the countries Vokalia and Consonantia, there live the blind texts. Separated they live in Bookmarksgrove right at the coast of the Semantics, a large language ocean."
        bg="ximage_4.jpg.pagespeed.ic.x3WQ0kfx8W.webp" />
      <!-- <ContentList path="/blog" v-slot="{ list }">
        <div v-for="article in list" :key="article._path">
          {{article.title}}
          <h2>{{ article.title }}</h2>
          <p>{{ article.description }}</p>
        </div>
      </ContentList> -->
    </section>
  </main>
</template>

<script setup>
import Article from '@/componenets/Article'
</script>

<style>
.text-outline{
  text-shadow:
    -1px -1px 0 rgb(120, 53, 15),
    1px -1px 0 rgb(120, 53, 15),
    -1px 1px 0 rgb(120, 53, 15),
    1px 1px 0 rgb(120, 53, 15);
}
</style>
