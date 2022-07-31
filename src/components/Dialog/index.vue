<template>
  <!-- 背景色 -->
  <div class="dialog-main">
    <div class="dialog" :style="{ width: width }" v-if="dialogShow">
      <div class="header" :style="{ background: titleBGC }">
        <div class="title">
          <!-- title具名插槽 -->
          <slot name="title">
            {{ title }}
          </slot>
        </div>
        <div class="off" @click.stop="dialogShowFn">&times;</div>
      </div>
      <div class="body">
        <!-- body匿名插槽 -->
        <slot></slot>
      </div>
      <div class="footer" :style="{ textAlign: footerDisplay }">
        <!-- 底部具名插槽 -->
        <slot name="footer"></slot>
      </div>
    </div>
    <div
      class="mask"
      :class="{ background: mask || offMask }"
      v-if="animation"
      @click.self="dialogShowFn"
    ></div>
  </div>
</template>

<script>
export default {
  props: {
    visible: { // dialog是否显示
      type: Boolean,
      default: false
    },
    title: { // title标题文本
      type: [String, Number]
    },
    titleBGC: { // title区域背景色
      type: String,
      default: '#fff'
    },
    width: { // dialog显示宽度
      type: String,
      default: '40%'
    },
    offMask: { // 关闭遮罩层
      type: Boolean,
      default: false
    },
    footerDisplay: { // 底部插槽显示模式
      type: String,
      default: 'right'
    }
  },
  created () { },
  data () {
    return {
      dialogShow: false,
      animation: false,
      mask: true
    }
  },
  methods: {
    dialogShowFn () {
      this.dialogShow = false
      this.$emit('update:visible', false)
    }
  },
  computed: {},
  watch: {
    visible: {
      handler (newVal) {
        if (newVal) {
          this.animation = true
          setTimeout(() => {
            this.mask = false
          }, 1)
          this.$emit('open')
        } else {
          this.$emit('close')
          this.mask = true
          setTimeout(() => {
            this.animation = false
          }, 330)
        }
        this.dialogShow = newVal
      }
    }
  },
  filters: {},
  components: {}
}
</script>

<style scoped lang='scss'>
.mask {
  position: fixed;
  left: 0;
  top: 0;
  background-color: rgba(0, 0, 0, 0.3);
  height: 100vh;
  width: 500vw;
  transition: 0.33s;
}
.dialog {
  color: #333;
  box-shadow: 1px 1px 2px 1px rgba(0, 0, 0, 0.1);
  z-index: 10;
  position: absolute;
  left: 50%;
  top: 0;
  transform: translate(-50%, 0);
  margin: 100px 0 100px;
  background-color: #fff;
  overflow: hidden;
  .header {
    padding: 10px;
    background-color: #66b1ff;
    display: flex;
    justify-content: space-between;
    // .title {
    // }
    .off {
      font-size: 20px;
      line-height: 16px;
      cursor: pointer;
    }
  }
  .body {
    padding: 10px;
  }
  .footer {
    padding: 0 10px 10px;
    // text-align: right;
  }
}

.background {
  background-color: rgba(0, 0, 0, 0);
}
</style>
