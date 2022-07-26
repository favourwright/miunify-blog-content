<template>
<div
    v-intersection-observer="onIntersectionObserver"
    class="article">
    <div>
      <div :style="`background-image:url(images/${bg})`"></div>
    </div>
    <div>
      <div>
        <h2 class="title">
          {{ title }}
          <a :href="link"></a>
        </h2>
        <p class="description">{{ description }}</p>
        <MoreBtn :link="link" :auto_play="auto_play">LEARN MORE</MoreBtn>
      </div>
    </div>
  </div>
</template>

<script setup>
import { vIntersectionObserver } from '@vueuse/components'
import { useWindowScroll } from '@vueuse/core'
import MoreBtn from '@/componenets/ViewArticleBtn'


const props = defineProps({
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  },
  bg: {
    type: String,
    default: 'ximage_1.jpg.pagespeed.ic.MUxtZlUbLa.webp'
  },
  link: {
    type: String,
    default: '/'
  }
})
let { y } = useWindowScroll()
let target_details = ref(null)
let target_height = ref(null)
let is_visible = ref(false)
let elem_y_cord = ref(null)
let entering_elem_y_cord = ref(null)
const percentage_shown = computed(()=>(((target_height.value-elem_y_cord.value)/target_height.value)*100).toFixed(1))
const img_percentage_to_use = computed(()=>is_visible.value?100+(percentage_shown.value/10)+"%":'100%')
const txt_percentage_to_use = computed(()=>is_visible.value?((percentage_shown.value)*-1)+'px':'0')
const auto_play = ref(false)

function onIntersectionObserver([el]) {
  target_details.value = el
  target_height.value = el.boundingClientRect.height
  is_visible.value = el.isIntersecting
}
function calculateIsVisible(top_offset, y_cord) {
  const value = top_offset-y_cord
  // negative value means element has reached above the screen
  const entering = value > 0 ? true : false
  return { entering, value: Math.abs(value) }
}

watch(y, (new_y) => {
  if(is_visible.value){
    const { entering, value } = calculateIsVisible(target_details.value.target.offsetTop, new_y)
    elem_y_cord.value = value
    entering_elem_y_cord.value = entering
  }
})
watch(percentage_shown, (new_percentage) => {
  auto_play.value = new_percentage > 60 ? true : false
})
</script>

<style scoped>
.article{
  @apply min-h-screen flex flex-col md:flex-row gap-10
  border-4 md:border-none border-neutral-700/20 relative;
}
.article:last-of-type {
  @apply mb-10 md:mb-20
}
.article > div{
  @apply relative;
  min-height: calc(100vh/1.5);
}
.article > div:nth-child(odd) {
  @apply md:w-3/5;
}
.article > div:nth-child(odd) > div {
  @apply absolute bottom-0 left-0 right-0
  bg-no-repeat bg-cover bg-center
  transition-all duration-200;
  height: v-bind(img_percentage_to_use);
}
.article > div:nth-child(even) {
  @apply md:w-2/5;
}
:global(.articles > .article:nth-child(even)) {
  @apply md:flex-row-reverse
}
.article > div:nth-child(even) > div{
  @apply mt-10 transition-all duration-100
  flex flex-col;
  transform: translateY(v-bind(txt_percentage_to_use));
}
/* prevent transform on mobile screens */
@media (max-width: 768px) {
  .article > div > div{
    transform: translateY(0);
  }
}
.article > div > div > .meta{
  @apply text-base text-gray-400 font-medium
}
.article > div > div > .title{
  @apply text-6xl md:text-8xl text-neutral-700 mb-8 relative
  underline decoration-neutral-500 hover:decoration-amber-900
  decoration-4 md:decoration-8 underline-offset-4 transition-all duration-300
  cursor-pointer bg-white/10 backdrop-blur-sm md:bg-transparent px-3;
}
.article > div > div > .title > a{
  @apply absolute top-0 right-0 bottom-0 left-0
}
.article > div > div > .description{
  @apply text-lg text-gray-500 mb-6 px-3
}
.article button{
  @apply self-start md:self-end mx-3;
}
:global(.articles > .article:nth-child(even) button) {
  @apply md:self-start
}
</style>