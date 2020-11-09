<script>
export default {
  name: "Carousel",
  props: {
    dotsVisible: {
      type: Boolean,
      required: false,
    },
    automatic: {
      type: Boolean,
      required: false,
    },
    timer: {
      type: Number,
      required: false,
      default: () => 3000,
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
      if (this.automatic) {
        this.interval = setInterval(() => this.sequenceSlide(), this.timer);
      }
    },
    sequenceSlide() {
      if (this.index < this.slides.length - 1) this.index++;
      else this.index = 0;
      this.$emit("change", this.index);
    },
    checkSlide(event) {
      if (event.keyCode === 39) {
        this.next();
      } else if (event.keyCode === 37) {
        this.prev();
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
  <div class="shr-carousel" tabindex="0" @keydown="checkSlide($event)">
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
  justify-content: center;
  flex-direction: column;
  outline: none;
  width: 500px;
  &__dots {
    display: flex;
    justify-content: center;
    padding-top: 10px;

    &__dot {
      width: 10px;
      height: 10px;
      cursor: pointer;
      background-color: blueviolet;
      opacity: 0.6;
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
        background-color: blanchedalmond;
        opacity: 1;
        transform: scale(1.2);
      }
    }
  }
}
</style>
