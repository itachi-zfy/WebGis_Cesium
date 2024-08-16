<script  lang="ts" setup>
import HelloWorld from './components/HelloWorld.vue'
import * as Cesium from 'cesium'
import PositionProperty from 'cesium/Source/DataSources/PositionProperty';
import { onMounted, version } from 'vue';
onMounted(()=>{
  console.log(22222,Cesium);
  Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJlYjIwNTQyMi1kNDc0LTQ3ZDItYjZhYy1iNGI5OTgxMjM0NmMiLCJpZCI6MjI5NjAxLCJpYXQiOjE3MjE0ODMxMjl9.2T_Xgk-UDIHjDq_aT8Dk9OoLJIuXJqPKw9rWYpfp-_k';
  
  const viewer = new Cesium.Viewer('cesiumContainer',{
    timeline:false,
    terrainProvider: Cesium.createWorldTerrain({
      requestWaterMask: true,
      requestVertexNormals: true,
    }),
})

var origin  = Cesium.Cartesian3.fromDegrees(114.399255, 30.539081, 10000);
var modelMatrix = Cesium.Transforms.eastNorthUpToFixedFrame(origin);
var model = viewer.scene.primitives.add(Cesium.Model.fromGltf({
  url:'http://192.168.3.65:8080/Apps/SampleData/models/CesiumAir/Cesium_Air.glb',
  modelMatrix: modelMatrix,
  scale:50
}))
viewer.camera.flyTo({
  destination:Cesium.Cartesian3.fromDegrees(114.399255, 30.539081, 11000),
})
let czml = [
  {
    id:"document",
    name:"CZML_Model",
    version:"1.0"
  },
  {
    id:"aircraft_model",
    name:"Cesium Air",
    position:{
      cartographicDegrees:[114.399255, 30.539081, 10000]
    },
    model:{
      gltf:"http://192.168.3.65:8080/Apps/SampleData/models/CesiumAir/Cesium_Air.glb",
      scale:2.0
    }
  }
]
var dataSourcesPromise = viewer.dataSources.add(Cesium.CzmlDataSource.load(czml));
dataSourcesPromise.then(function(dataSource){
  viewer.trackedEntity = dataSource.entities.getById('aircraft_model');
})
  console.log(111111,Cesium);
})
</script>

<template>
  <div id = "cesiumContainer" class="cesiumContainer">

  </div>

</template>


<style scoped>
.cesiumContainer {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  margin: 0;
  padding: 0;
}
</style>
