<template>
  <div class="shr-slide">
    <div class="visible" v-if="visible">
      <slot></slot>
      <img :src="imageUrl" :alt="title" class="image">
      <h1>{{title}}</h1>
      <p>{{subTitle}}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imageUrl: {
      type: String,
    },
    title: {
      type: String,
    },
    subTitle: {
      type: String,
    },
  },
  data() {
    return {
      index: 0,
    };
  },
  computed: {
    visible() {
      return this.index === this.$parent.index;
    },
    dir() {
      console.log(this.$parent.slideDirection);
      return this.$parent.slideDirection;
    },
  },
};
</script>

<style lang="scss" scoped>

.shr-slide {

  &image {
  height: 70vh;
}

}

</style>
