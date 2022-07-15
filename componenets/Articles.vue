<template>
 <div>{{is_intersecting}}</div>
</template>

<script setup>
let observer = reactive(null)
let is_intersecting = ref(false)
onMounted(() => {
  let options = {
    root: null,
    rootMargin: '0px',
    threshold: 1.0
  }
  let callback = (entries, observer) => {
    entries.forEach(entry => {
      // Each entry describes an intersection change for one observed
      // target element:
      //   entry.boundingClientRect
      //   entry.intersectionRatio
      //   entry.intersectionRect
      // entry.isIntersecting
      is_intersecting.value = entry.isIntersecting
      //   entry.rootBounds
      //   entry.target
      //   entry.time
    });
  };

  observer = new IntersectionObserver(callback, options);
  let target = document.querySelector('#landing');
  observer.observe(target);
})

onUnmounted(() => {
  observer.disconnect()
})
</script>

<style>

</style>