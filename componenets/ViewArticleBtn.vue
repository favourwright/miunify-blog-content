<template>
<button>
  <a :class="{'effect':true, 'auto-play':auto_play}" :href="link">
    <slot></slot>
    <span class="bg"></span>
  </a>
</button>
</template>

<script setup>
const props = defineProps({
  auto_play: {
    type: Boolean,
    default: false
  },
  link: {
    type: String,
    default: '/'
  }
})
</script>

<style scoped>
button {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  /* background: #eee; */
}

.effect {
  color: #222;
  text-decoration: none;
  font-family: sans-serif;
  font-size: 24px;
  position: relative;
  padding: 10px 50px 10px 20px;
  transition: all 0.3s;
  transform: scale(1);
}

.effect .bg {
  background: #222;
  width: 30px;
  height: 2px;
  position: absolute;
  right: 0;
  top: 50%;
  margin-top: -1px;
  z-index: -1;
  transition: all 0.3s;
}

.effect:hover {
  padding-right: 20px;
  color: #fff;
}
.effect.auto-play{
  padding-right: 20px;
  color: #fff;
}

.effect:hover .bg {
  height: 100%;
  width: 100%;
  transform: translate(0, -50%);
}
.effect.auto-play .bg {
  height: 100%;
  width: 100%;
  transform: translate(0, -50%);
}

.effect .bg:before, .effect .bg:after {
  content: '';
  height: 2px;
  width: 10px;
  background: #222;
  position: absolute;
  right: -2px;      
  transition: all 0.3s;
}

.effect .bg:before {
  bottom: 3px;
  transform: rotate(45deg);
}
.effect .bg:after{
  top: 3px;
  transform: rotate(-45deg);
}

.effect:hover .bg:before,
.effect:hover .bg:after{
  right: 0;
}
.effect.auto-play .bg:before,
.effect.auto-play .bg:after{
  right: 0;
}

.effect:hover .bg:before{
  bottom: 6px;
}
.effect.auto-play .bg:before{
  bottom: 6px;
}

.effect:hover .bg:after{
  top: 6px;
}
.effect.auto-play .bg:after{
  top: 6px;
}
</style>