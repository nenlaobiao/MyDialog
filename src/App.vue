<template>
  <div class="container">
    <button @click="dialogShow = true">
      {{ dialogShow ? "点击隐藏" : "点击显示" }}
    </button>
    <Dialog
      :visible.sync="dialogShow"
      title="Dialog标题"
      titleBGC="#ddd"
      width="400px"
      @close="close"
      @open="open"
      :offMask="false"
    >
      <template slot="title"> 666777 </template>
      Dialog 的内容
      <template slot="footer">
        <button @click="dialogShow = false">取消</button>
        <button>确认</button>
      </template>
    </Dialog>
  </div>
</template>

<script>
import Dialog from '@/components/Dialog'
export default {
  created () { },
  data () {
    return {
      dialogShow: false
    }
  },
  methods: {
    close () {
      console.log('关闭了Dialog')
    },
    open () {
      console.log('打开了Dialog')
    }
  },
  computed: {},
  watch: {},
  filters: {},
  components: { Dialog }
}
</script>

<style scoped lang='scss'>
.container {
  color: skyblue;
}
</style>
