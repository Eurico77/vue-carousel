<script>
export default {
  name: 'CarouselSlide',
  props: {
    imageUrl: {
      type: String,
      required: true,
      default: '',
    },
    title: {
      type: String,
      required: true,
      default: '',
    },
    subTitle: {
      type: String,
      required: true,
      default: '',
    },
  },
  data() {
    return {
      index: 0,
    }
  },
  computed: {
    visible() {
      return this.index === this.$parent.index
    },
    dir() {
      return this.$parent.slideDirection
    },
    customImage() {
      return this.$slots.image
    },
  },
}
</script>

<template>
  <div class="shr-slide">
    <div v-if="visible" class="shr-slide--shr-slide-content">
      <slot></slot>
      <template v-if="customImage">
        <slot name="image"></slot>
      </template>
      <img v-else :src="imageUrl" :alt="title" />
      <h1 class="shr-slide__title shr-text-weight-medium">{{ title }}</h1>
      <p class="shr-slide__subtitle shr-text-subtitle1">{{ subTitle }}</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>



</style>
