<template>
  <div class="slider">
    <transition v-on:before-enter="beforeEnter" v-on:after-leave="afterLeave" name="change">
      <div v-show="isShow" class="slider__content">{{ content }}</div>
    </transition>
    <div class="slider__arrows">
      <div class="slider__arrow slider__arrow_left" @click="change('left')">left</div>
      <div class="slider__arrow slider__arrow_right" @click="change('right')">right</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Slider",
  data() {
    return {
      isShow: false,
      status: null,
      content: null,
      pointer: 0,
      slides: [
        { title: "Slider-1" },
        { title: "Slider-2" },
        { title: "Slider-3" }
      ]
    };
  },
  mounted() {
    this.isShow = true;
    this.content = this.slides[this.pointer].title;
  },
  methods: {
    beforeEnter() {},
    afterLeave() {
      this.isShow = true;
      console.log("this.pointer", this.pointer);
      this.content = this.slides[this.pointer].title;
    },
    change(dir) {
      if (!isShow) {
        this.isShow = false;
        switch (dir) {
          case "left":
            this.pointer--;
            break;
          case "right":
            this.pointer++;
            break;
        }
        if (this.pointer < 0) {
          this.pointer = this.slides.length - 1;
        } else if (this.pointer > this.slides.length - 1) {
          this.pointer = 0;
        }
      }
    }
  }
};
</script>

<style>
.slider__content {
  background: #ccc;
  width: 1200px;
  height: 600px;
  position: relative;
}

.slider__arrows {
  position: absolute;
}
.change-enter {
  opacity: 0;
}

.change-enter-to {
  opacity: 1;
  transition: all 1s ease;
}

.change-leave {
  opacity: 1;
}

.change-leave-to {
  opacity: 0;
  transition: all 1s ease;
}
</style>