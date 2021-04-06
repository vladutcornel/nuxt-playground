<template>
  <div class="container">
    <h2>keen-slider</h2>

    <div id="slider" class="slider">
      <div ref="slider" class="slider-inner keen-slider">
        <div class="keen-slider__slide">
          <img
            width="385"
            height="256"
            src="https://i2.wp.com/www.cabral.ro/wp-content/uploads/2020/09/Bitdefender-Box-3-of-10.jpg?fit=820%2C547&ssl=1"
          />
        </div>
        <div class="keen-slider__slide">
          <img
            width="385"
            height="256"
            src="https://i0.wp.com/www.cabral.ro/wp-content/uploads/2020/11/libraria-Strand-2.jpg?fit=820%2C547&ssl=1"
          />
        </div>
        <div class="keen-slider__slide">
          <img
            width="385"
            height="256"
            src="https://i1.wp.com/www.cabral.ro/wp-content/uploads/2020/11/Dragoste-si-alte-droguri.jpg?fit=820%2C461&ssl=1"
          />
        </div>
        <div class="keen-slider__slide">
          <img
            width="385"
            height="256"
            src="https://i0.wp.com/www.cabral.ro/wp-content/uploads/2020/11/1250-GSA_1.jpeg?fit=820%2C615&ssl=1"
          />
        </div>
        <div class="keen-slider__slide">
          <img
            width="385"
            height="256"
            src="https://i1.wp.com/www.cabral.ro/wp-content/uploads/2020/12/Hip-hop.jpg?fit=820%2C461&ssl=1"
          />
        </div>
      </div>
      <a
        class="slider-control-prev"
        href="#slider"
        role="button"
        @click="slider.prev()"
      >
        <span class="slider-control-prev-icon" aria-hidden="true" />
        <span class="visually-hidden">Previous</span>
      </a>
      <a
        class="slider-control-next"
        href="#slider"
        role="button"
        @click="slider.next()"
      >
        <span class="slider-control-next-icon" aria-hidden="true" />
        <span class="visually-hidden">Next</span>
      </a>
      <div class="slider-indicators">
        <button
          v-for="(slide, idx) in dotHelper"
          :key="idx"
          class="dot"
          :class="{ active: current === idx }"
          @click="slider.moveToSlideRelative(idx)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import KeenSlider from "keen-slider";

export default {
  name: "Keen",

  data: () => ({
    current: 1,
    slider: null,
  }),
  computed: {
    dotHelper() {
      return this.slider ? [...Array(this.slider.details().size).keys()] : [];
    },
  },
  mounted() {
    this.slider = this.keenSlider();
  },
  beforeDestroy() {
    if (this.slider) this.slider.destroy();
  },
  methods: {
    keenSlider() {
      return new KeenSlider(this.$refs.slider, {
        initial: this.current,
        slidesPerView: 2,
        mode: "free-snap",
        spacing: 15,
        centered: true,
        loop: true,
        slideChanged: (s) => {
          this.current = s.details().relativeSlide;
        },
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~keen-slider/keen-slider.scss";
//@import "~/assets/scss/app-component.scss";
$carousel-control-width: 10rem;
$carousel-control-icon-width: 10rem;
$carousel-control-color: #666;
$carousel-control-opacity: 0.69;

.slider {
  position: relative;
}
.slider-control-prev,
.slider-control-next {
  position: absolute;
  top: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: translateY(-50%);
  width: $carousel-control-width;
  color: $carousel-control-color;
  opacity: $carousel-control-opacity;
  //@include transition($carousel-control-transition);
}
.slider-control-prev {
  left: 0;
}
.slider-control-next {
  right: 0;
}
.slider-control-prev-icon,
.slider-control-next-icon {
  display: inline-block;
  width: $carousel-control-icon-width;
  height: $carousel-control-icon-width;
  background: 50% / 100% 100% no-repeat;
}
.slider-control-prev-icon {
  //background-image: escape-svg($carousel-control-prev-icon-bg);
  background: #3b8070;
}
.slider-control-next-icon {
  //background-image: escape-svg($carousel-control-next-icon-bg);
  background: #3b8070;
}
.slider-indicators {
  display: flex;
  justify-content: center;
  padding: 10px 0;
  > * {
    border: none;
    width: 10px;
    height: 10px;
    background: #c5c5c5;
    border-radius: 50%;
    margin: 0 5px;
    padding: 5px;
    cursor: pointer;
    &.active {
      background: #000;
    }
  }
}
</style>
