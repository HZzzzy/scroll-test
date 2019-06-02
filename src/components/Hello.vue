<template>
  <div>
    <cube-popup type="dialog" :ref="refName" :zIndex="99"
      :maskClosable="closeable"  @mask-click.stop="popHide"
      position="center">
      <div class="pop">
        <ul>
          <li><router-link :to="{name: 'HelloWorld'}">编辑</router-link></li>
          <li @click="clickHandler">删除</li>
        </ul>
      </div>
    </cube-popup>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  name: 'hello',
  props: {
    content: {
      type: String,
      default: 'Hello',
    },
    closeable: {
      type: Boolean,
      default: true,
    },
    refName: {
      type: String,
      default: 'mypop',
    },
    itemId: {
      type: String,
    },
  },
  methods: {
    clickHandler(e) {
      e.preventDefault();
      this.$createToast({
        txt: this.itemId,
        time: 2000,
      }).show();
    },
    popHide() {
      debugger;
      this.test = '';
    },
  },
};
</script>
<style>
.pop {
  background: white;
  width: 4rem;
  text-align: center;
}
</style>
