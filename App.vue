<script setup lang="ts">
import * as Cesium from "cesium"
import { onMounted } from 'vue'
onMounted(()=>{
  console.log(22222,Cesium);
  Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJlYjIwNTQyMi1kNDc0LTQ3ZDItYjZhYy1iNGI5OTgxMjM0NmMiLCJpZCI6MjI5NjAxLCJpYXQiOjE3MjE0ODMxMjl9.2T_Xgk-UDIHjDq_aT8Dk9OoLJIuXJqPKw9rWYpfp-_k';
  const viewer = new Cesium.Viewer('cesiumContainer',{
    timeline: false,
    // imageryProvider: new Cesium.ArcGisMapServerImageryProvider({
    //       url: "http://map.geoq.cn/ArcGIS/rest/services/ChinaOnlineStreetPurplishBlue/MapServer",
    //       //url: "https://services.arcgisonline.com/arcgis/rest/services/World_Imagery/MapServer",
    //     }),
  //   terrainProvider: new Cesium.CesiumTerrainProvider({
  //   url: 'https://assets.agi.com/stk-terrain/v1/tilesets/world/tiles', // 地形数据的URL
  //   requestVertexNormals: true // 如果地形数据包含法线信息，可以设置为true
  // }),
})

const terrainProvider = new Cesium.CesiumTerrainProvider({
  url:Cesium.IonResource.fromAssetId(3356),
  requestWaterMask:true,//请求水体效果所需要的海岸线数据
  requestVertexNormals:true,//请求地形照明数据
})
viewer.terrainProvider = terrainProvider 

})

</script>

<template>
  <div id = "cesiumContainer" class="cesium-container">
    
  </div>
</template>

<style scoped>
  .cesium-container {
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0;
    background-color: aqua;
  }
</style>
