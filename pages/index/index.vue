<template>
  <view>
    <!-- 自定义导航栏 -->
    <nav-bar>
      <text slot="left" class="font-md ml-3">首页</text>
      <template slot="right">
        <view
          class="flex align-center justify-center bg-icon rounded-circle mr-3"
          style="width: 60rpx; height: 60rpx"
        >
          <text class="iconfont icon-zengjia"></text>
        </view>
        <view
          class="flex align-center justify-center bg-icon rounded-circle mr-3"
          style="width: 60rpx; height: 60rpx"
        >
          <text class="iconfont icon-gengduo"></text>
        </view>
      </template>
    </nav-bar>
    <view class="px-3 py-2">
      <view class="position-relative">
        <view
          class="flex align-center justify-center text-light-muted"
          style="
            width: 70rpx;
            height: 70rpx;
            position: absolute;
            top: 0;
            left: 0;
          "
        >
          <text class="iconfont icon-sousuo"></text>
        </view>
        <!-- <uni-search-bar :radius="20"  placeholder="搜索网盘文件" @confirm="search" cancelButton="none"></uni-search-bar> -->
        <input
          style="height: 70rpx; padding-left: 70rpx"
          type="text"
          class="bg-light font-md rounded-circle"
          placeholder="搜索网盘文件"
        />
      </view>
    </view>
    <view v-for="(item, index) in list" :key="index">
      <fList :item="item" :index="index" @select="select"></fList>
    </view>
  </view>
</template>

<script>
import navBar from "@/components/common/nav-bar.vue";
import fList from "@/components/common/f-list.vue";
// import uniSearchBar from '@/components/uni-search-bar/uni-search-bar.vue';
export default {
  components: {
    navBar,
    fList,
    // uniSearchBar
  },
  data() {
    return {
      title: "Hello",
      list: [
        {
          type: "dir",
          name: "我的笔记",
          create_time: "2020-10-21 08:00",
          checked: false,
        },
        {
          type: "image",
          name: "风景.jpg",
          create_time: "2020-10-21 08:00",
          checked: false,
        },
        {
          type: "video",
          name: "uniapp实战教程.mp4",
          create_time: "2020-10-21 08:00",
          checked: false,
        },
        {
          type: "text",
          name: "记事本.txt",
          create_time: "2020-10-21 08:00",
          checked: false,
        },
        {
          type: "none",
          name: "压缩包.rar",
          create_time: "2020-10-21 08:00",
          checked: false,
        },
      ],
    };
  },
  onLoad() {
    uni.request({
      url: "http://localhost:7001/list",
      method: "GET",
      success: (res) => {
        console.log(res.data);
      },
    });
  },
  methods: {
    select(e) {
      this.list[e.index].checked = e.value;
    },
  },
};
</script>

<style>
</style>
