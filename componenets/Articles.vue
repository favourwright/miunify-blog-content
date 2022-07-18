<template>
<div
    v-intersection-observer="onIntersectionObserver"
    class="article">
    <div>
      Y:{{elem_y_cord}}
      Entering:{{entering_elem_y_cord}}
      <div>
        hey
      </div>
    </div>
    <div></div>
  </div>
</template>

<script setup>
import { vIntersectionObserver } from '@vueuse/components'
import { useWindowScroll } from '@vueuse/core'

const { y } = useWindowScroll()
const target_details = ref(null)
const is_visible = ref(false)
const elem_y_cord = ref(null)
const entering_elem_y_cord = ref(null)

function calculateIsVisible(top_offset, y_cord) {
  const value = top_offset-y_cord
  const entering = value > 0 ? true : false
  return { entering, value: Math.abs(value) }
}

watch(y, (new_y) => {
  if(is_visible.value){
    const { entering, value } = calculateIsVisible(target_details.value.target.offsetTop, new_y)
    elem_y_cord.value = value
    entering_elem_y_cord.value = entering
    // console.log(target_details.value.boundingClientRect.height-value);
  }
})

function onIntersectionObserver([el]) {
  target_details.value = el
  is_visible.value = el.isIntersecting
}
</script>

<style scoped>
.article{
  @apply h-screen flex;
}
.article > div{
  @apply relative
}
.article > div:nth-child(odd) {
  @apply w-3/5 bg-gray-300
}
.article > div:nth-child(odd) > div {
  @apply bg-rose-500 absolute bottom-0
  left-0 right-0
}
.article > div:nth-child(even) {
  @apply w-2/5
}
</style>