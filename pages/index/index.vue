<template>
  <view>
    <!-- 自定义导航栏 -->
    <nav-bar>
      <template v-if="checkCount === 0">
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
      </template>
      <template v-else>
        <view
          slot="left"
          class="font-md ml-3 text-primary"
          @click="handleCheckAll(false)"
          >取消</view
        >
        <text class="font-md font-weight-bold">已选中{{ checkCount }}</text>
        <view
          slot="right"
          class="font-md mr-3 text-primary"
          @click="handleCheckAll(true)"
          >全选</view
        >
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
    <view v-if="checkCount > 0">
      <view style="height: 115rpx"></view>
      <view
        style="height: 115rpx"
        class="flex align-stretch bg-primary text-white fixed-bottom"
      >
        <view
          class="flex-1 flex flex-column align-center justify-center"
          style="line-height: 1.5"
          v-for="(item, index) in actions"
          :key="index"
          hover-class="bg-hover-primary"
          @click="handleBottomEvent(item)"
        >
          <text class="iconfont" :class="item.icon"></text>
          {{ item.name }}
        </view>
      </view>
    </view>
    <fDialog ref="dialog">是否删除选中的文件</fDialog>
  </view>
</template>

<script>
import navBar from "@/components/common/nav-bar.vue";
import fList from "@/components/common/f-list.vue";
import fDialog from "@/components/common/f-dialog.vue";
// import uniSearchBar from '@/components/uni-search-bar/uni-search-bar.vue';
export default {
  components: {
    navBar,
    fList,
    fDialog,
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
    handleCheckAll(checked) {
      this.list.forEach((item) => {
        item.checked = checked;
      });
    },
    handleBottomEvent(item) {
      switch (item.name) {
        case "删除":
          this.$refs.dialog.open((close) => {
            close();
            console.log("删除文件");
            console.log(this.checkList);
		  });
		  break;
		default:
			break;
      }
    },
  },
  computed: {
    checkList() {
      return this.list.filter((item) => item.checked);
    },
    checkCount() {
      return this.checkList.length;
    },
    actions() {
      if (this.checkCount > 1) {
        return [
          {
            icon: "icon-xiazai",
            name: "下载",
          },
          {
            icon: "icon-shanchu",
            name: "删除",
          },
        ];
      }
      return [
        {
          icon: "icon-xiazai",
          name: "下载",
        },
        {
          icon: "icon-fenxiang-1",
          name: "分享",
        },
        {
          icon: "icon-shanchu",
          name: "删除",
        },
        {
          icon: "icon-chongmingming",
          name: "重命名",
        },
      ];
    },
  },
};
</script>

<style>
</style>
