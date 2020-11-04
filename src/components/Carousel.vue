<script>
export default {
  props: {
    dotsVisible: {
      type: Boolean,
    },
  },
  data() {
    return {
      index: 0,
      interval: null,
      slides: [],
      slideDirection: "",
    };
  },
  computed: {
    slidesLength() {
      return this.slides.length;
    },
  },
  mounted() {
    this.setInterval();
    this.slides = this.$children;
    this.slides.map((slide, index) => {
      slide.index = index;
    });
  },
  destroyed() {
    clearInterval(this.intervalo);
  },
  methods: {
    next() {
      this.index++;
      if (this.index >= this.slidesLength) {
        this.index = 0;
      }
      this.slideDirection = "slide-right";
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.slidesLength - 1;
      }
      this.slideDirection = "slide-left";
    },
    setInterval() {
      this.interval = setInterval(() => this.ramdomSlide(), 5000);
    },
    ramdomSlide() {
      if (this.index < this.slides.length - 1) this.index++;
      else this.index = 0;
      this.$emit("change", this.index);
    },
    checkSlide(event) {
      if (event.keyCode === 39) {
        this.next();
      } else if (event.keyCode === 37) {
        this.prev();
      } else {
        return;
      }
    },
    cliqueInDot(index) {
      this.$emit("change", index);
      this.index = index;
      clearInterval(this.interval);
      this.setInterval();
    },
  },
};
</script>

<template>
  <div class="shr-carousel" @keydown="checkSlide($event)" tabindex="0">
    <slot></slot>
    <div v-if="dotsVisible" class="shr-carousel__dots">
      <span
        v-for="(i, ind) in slides"
        :key="ind"
        class="shr-carousel__dots__dot"
        :class="{ 'shr-carousel__dots__dot--active': ind === index }"
        @click.prevent="cliqueInDot(ind)"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.shr-carousel {
  display: flex;
  flex-direction: column;
  outline: none;
  &__dots {
    display: flex;
    justify-content: center;
    padding-top: 10px;

    &__dot {
      cursor: pointer;
      height: 10px;
      width: 10px;
      background-color: #e0e0e0;
      border-radius: 100%;
      transition: all 0.2s ease;
      &:not(:last-of-type) {
        margin-right: 10px;
      }
      &:hover {
        transition: all 0.2s ease;
        transform: scale(1.1);
      }
      &--active {
        transform: scale(1.2);
        background-color: blue;
      }
    }
  }
}
</style>
