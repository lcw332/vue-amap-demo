<template>
  <div class="app-container">
    <!-- 顶部搜索框 -->
    <van-search
      v-model="searchValue"
      :placeholder="searchPh"
      @search="onSearch()"
    />
    <!-- 地图组件 -->
    <amap
      :is-hotspot="false"
      :show-indoor-map="false"
      :center="centerPoint"
      :zoom="zoomLevel"
      map-style="amap://styles/whitesmoke"
    >
    </amap>
    <!-- 从底部上来的弹出层 -->
    <van-popup
      v-model="isSearchReusltPopShow"
      :position="popPosition"
      :overlay="overlay"
      :closeable="true"
      :style="{ height: '40%' }"
    >
      <!-- 展示搜索结果 -->
      <van-list
        v-model="loading"
        :finished="finished"
        finished-text="没有更多了"
      >
        <!-- 里面使用单元格组件 -->
        <van-cell
          v-for="item in fakeData"
          :key="item.title"
          :title="item.title"
          :label="item.desc"
        ></van-cell>
      </van-list>
    </van-popup>
  </div>
</template>
<script>
import { loadPlugins } from "@amap/amap-vue";

export default {
  name: "GetLocationInfo",
  data() {
    return {
      // 是否没有新的结果集
      finished: false,
      // 结果集
      loading: false,
      // 是否展示弹出层
      isSearchReusltPopShow: true,
      // 弹出层位置
      popPosition: "bottom",
      // 是否暂时遮罩层
      overlay: false,
      searchValue: "",
      searchPh: "请输入地址",
      centerPoint: [116.473778, 39.990661],
      zoomLevel: 13,
      // 假数据
      fakeData: [
        {
          title: "北京大学",
          desc: "颐和园路5号",
        },
        {
          title: "北京大学医学部",
          desc: "学院路38号",
        },
        {
          title: "北京大学",
          desc: "颐和园路5号",
        },
        {
          title: "北京大学医学部",
          desc: "学院路38号",
        },
        {
          title: "北京大学",
          desc: "颐和园路5号",
        },
        {
          title: "北京大学医学部",
          desc: "学院路38号",
        },
      ],
    };
  },
  async mounted() {
    // 加载组件
    await loadPlugins(["Amap.AutoComplete", "Amap.PlaceSearch"]);
  },
  methods: {
    // 搜索方法
    onSearch(){

    }
  },
};
</script>
<style>
.app-container {
  width: 100%;
  height: 500px;
}
</style>