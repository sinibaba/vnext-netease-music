<template>
  <div class="player-progress slider-hover-button">
    <ElSlider
      v-model="progress"
      :min="0"
      :max="duration"
      :show-tooltip="false"
      class="hover-button"
      @input="changeSlider"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmit, watch } from 'vue'
import { ElSlider } from 'element-plus'

const props = defineProps({
  currentTime: {
    type: Number,
    required: true,
  },
  duration: {
    type: Number,
    required: true,
  },
})

const emits = defineEmit(['update:currentTime'])

const progress = ref(0)
// const ssslider = ref<any>(null)
const changeSlider = (s: any) => {
  // nextTick(() => {
  //   console.log('1111', s)
  // })

  // console.log(ssslider.value.barStyle)

  emits('update:currentTime', progress.value)
}

watch(() => props.currentTime, (newv, oldv) => {
  // console.log('22222', newv, oldv)
  progress.value = props.currentTime
})

// setInterval(() => {
//   console.log(1)
//   slider.value = slider.value + 1
// }, 1000)

// watchEffect(() => {
//   // slider.value = Math.round(props.currentTime / props.duration * 100)
// })
</script>

<style lang="scss" scoped>
@include b(player-progress) {
  position: absolute;
  top: -13px;
  left: 0;
  width: 100%;
  padding: 10px 0;
}
</style>
