<template>
  <section :id="key" class="comp-compare"
    :style="{
      height: heightLimit ? height + 'px' : 'auto'
    }">
    <img class="bottom-image"
      :src="bottomImage" alt=""
      @load="handleImageLoad()">
    <div class="box-top-layer"
      :style="{
        width: coverWidth + 'px'
      }">
      <img class="top-image"
        :src="coverImage" alt=""
        :style="{
          width: width + 'px',
          clipPath
        }">
      <svg class="fake-handler"
        :width="coverWidth"
        :height="height"
        v-html="seperatorPath"></svg>
      <div class="real-handler"
        draggable="true"
        @drag="handleDrag"
        :style="{
          right: seperator === 'slash' ? slashDivX / 2 + 'px' : 0
        }">&nbsp;</div>
    </div>
  </section>
</template>

<script>
let compX = 0

export default {
  props: {
    bottomImage: {
      type: String,
      required: true
    },
    coverImage: {
      type: String,
      required: true
    },
    heightLimit: {
      type: Number,
      required: false,
      default: 0
    },
    seperator: { // slash | vertical
      type: String,
      required: false,
      default: 'slash'
    },
    position: {
      type: Number,
      requried: false,
      default: 0.5
    },
    seperatorColor: {
      type: String,
      required: false,
      default: '#fff'
    },
    key: {
      type: String,
      required: false,
      default: 'compare-comp'
    }
  },
  data () {
    return {
      width: 0,
      height: 0,
      coverWidth: 0
    }
  },
  computed: {
    slashDivX () { // 倾斜分隔的横向间距距离，单位px
      if (this.seperator === 'slash') {
        return this.height * 0.2
      } else {
        return 0
      }
    },
    clipPath () {
      return `path('M0 0 L${this.coverWidth} 0 L${this.coverWidth - this.slashDivX} ${this.height} L0 ${this.height} Z')`
    },
    seperatorPath () {
      return `<path d="M${this.coverWidth} 0 L${this.coverWidth - this.slashDivX} ${this.height}" fill="transparent" stroke="${this.seperatorColor}" stroke-width="2"/><circle cx="${this.coverWidth - this.slashDivX / 2}" cy="${this.height / 2}" r="2" stroke="${this.seperatorColor !== 'transparent' ? this.seperatorColor : '#fff'}" fill="transparent" stroke-width="5"/>`
    }
  },

  methods: {
    handleDrag (e) {
      // console.log('drag', e)
      const x = e.clientX || e.x
      const y = e.clientY || e.y
      if (x === 0 && y === 0) {
        return
      }
      const attempX = x - compX
      if (attempX > this.width) {
        this.coverWidth = this.width + this.slashDivX / 2
      } else if (attempX < 0) {
        this.coverWidth = 2 + this.slashDivX / 2
      } else {
        this.coverWidth = attempX + this.slashDivX / 2
      }
    },
    handleImageLoad () {
      // console.log('image loaded')
      const { width, height, left } = document.querySelector(`#${this.key}`).getBoundingClientRect()
      compX = left
      this.width = width
      if (this.heightLimit) {
        this.height = this.heightLimit
      } else {
        this.height = height
      }
      this.coverWidth = this.width * this.position + this.slashDivX / 2
    }
  }
}
</script>

<style scoped>
.comp-compare {
  position: relative;
  overflow: hidden;
}
img {
  width: 100%;
  height: 100%;
  vertical-align: top;
  pointer-events: none;
}
.bottom-image {
  object-fit: cover;
}
.box-top-layer {
  position: absolute;
  left: 0;
  top: 0;
  /* right: 0; */
  width: 80%;
  bottom: 0;
  z-index: 1;
}
.top-image {
  object-fit: cover;
}
.fake-handler {
  position: absolute;
  left: 0;
  top: 0;
  z-index: 1;
  pointer-events: none;
}
.real-handler {
  position: absolute;
  top: 0;
  bottom: 0;
  z-index: 2;
  width: 4px;
  height: 100%;
  background: transparent;
  /* background: red; */
  cursor: ew-resize;
}
</style>
