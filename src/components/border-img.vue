<template>
  <view>
    <img class="border-img" @click="handleSrcChange" :src="src" alt="">
  </view>
</template>

<script>
export default {
  props: {
    src: String
  },
  methods: {
    handleSrcChange () {
      this.$emit('srcChange',this.src)
    }
  }
}
</script>

<style>
  .border-img {
    border-radius: 50%;
  }
</style>