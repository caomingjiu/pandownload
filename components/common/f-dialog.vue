<template>
  <uni-popup ref="dialog">
    <view style="width: 600rpx" class="bg-white rounded">
      <view
        class="flex align-center justify-center font-weight-bold border-bottom border-light-secondary"
        style="height: 100rpx"
      >
        {{ title }}
      </view>
      <view class="flex align-center justify-center p-3"><slot></slot></view>
      <view
        class="flex border-top border-light-secondary"
        style="height: 100rpx"
      >
        <view
          class="flex-1 text-muted flex align-center justify-center"
          @tap="cancel"
          >{{ cancelText }}</view
        >
        <view
          class="flex-1 text-main flex align-center justify-center"
          @tap="confirm"
          >{{ confirmText }}</view
        >
      </view>
    </view>
  </uni-popup>
</template>

<script>
import uniPopup from "../uni-ui/uni-popup/uni-popup";
export default {
  components: {
    uniPopup,
  },
  //父组件可以传递弹出层的图标，确定和取消区域的文字，不传就是用默认值
  props: {
    title: {
      type: String,
      default: "提示",
    },
    cancelText: {
      type: String,
      default: "取消",
    },
    confirmText: {
      type: String,
      default: "确定",
    },
  },
  data() {
    return {
      //是否需要回调函数，默认不需要
      callback: false,
    };
  },
  methods: {
    open(callback = false) {
      this.callback = callback;
      this.$refs.dialog.open();
    },
    cancel() {
      //向父组件传递cancel时间，同时关闭对话框
      this.$emit("cancel");
      this.$refs.dialog.close();
    },
    confirm() {
      //如果选哟回调，表示暂时不关闭，则当前对象的cancel传递
      if (typeof this.callback === "function") {
        this.callback(() => {
          this.cancel();
        });
      } else {
        //向父组件传递confirm事件
        this.$emit("confirm");
        this.cancel();
      }
    },
  },
};
</script>

<style>
</style>
