<template>
  <van-form @submit="onSubmit">
    <van-field
      v-model="username"
      name="起点-经纬度"
      label="起点-经纬度"
      placeholder="经纬度"
      :rules="[{ required: true, message: '请填写用户名' }]"
    >
      <template #button>
        <van-button size="small" type="primary">定位</van-button>
      </template>
    </van-field>
    <van-field
      v-model="password"
      name="终点-经纬度"
      label="终点-经纬度"
      placeholder="经纬度"
      :rules="[{ required: true, message: '请填写密码' }]"
    >
      <template #button>
        <van-button size="small" type="primary">定位</van-button>
      </template>
    </van-field>
    <!-- 地图详情 -->
    <div style="width: 100%; height: 400px">
      <amap
        cache-key="map"
        ref="map"
        view-mode="3D"
        map-style="amap://styles/whitesmoke"
        async
        :zoom.sync="zoom"
        :center.sync="center"
        :pitch.sync="pitch"
        :rotation.sync="rotation"
        :show-indoor-map="false"
        is-hotspot
        @hotspotclick="onHotspotClick"
      >
        <amap-marker
          :position="position"
          :label="{
            content: '起点',
            direction: 'bottom',
          }"
        />
      </amap>
    </div>
    <div style="margin: 16px">
      <van-button round block type="info" native-type="submit">提交</van-button>
    </div>
  </van-form>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data() {
    return {
      username: "",
      password: "",
      center: [116.473778, 39.990661],
      position: [116.473778, 39.990661],
      zoom: 9,
      pitch: 45,
      rotation: 15,
    };
  },
  methods: {
    onSubmit(values) {
      console.log("submit", values);
    },
    onHotspotClick(e) {
      if (e && e.lnglat) {
        this.center = [e.lnglat.lng, e.lnglat.lat];
      }
    },
    // 获取定位信息
    onSubGetOptions(){

    }
  },
};
</script>
