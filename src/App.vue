<template>
  <div id="app">
    <Menu @periodeData="updateData" @kindData="updateKindData" id="nav" />
    <div id="menuButton" v-on:click="menu"><ArrowRightCircleIcon id="menuIcon"></ArrowRightCircleIcon></div>
    <Content id="content" :periode="periode" :kind="kind"/>
  </div>
</template>

<script>
import Content from './components/Content'
import Menu from './components/Menu'
import { ArrowRightCircleIcon } from 'vue-feather-icons'

export default {
  name: 'App',
  components: {
    Content,
    Menu,
    ArrowRightCircleIcon
  },
  data: function () {
    return {
      baseClass: 'v-icon',
      periode: "",
      kind: ""
    }
  },
  methods: {
    menu: function(){
      var nav = document.getElementById("nav");
      var button = document.getElementById("menuButton");
      var icon = document.getElementById("menuIcon");
      if (nav.style.left !== "0px"){
        nav.style.left = "0px";
        button.style.left = "300px"
        icon.style.transform = "rotate(180deg)";
      }else{
        nav.style.left = "-360px";
        button.style.left = "5px";
        icon.style.transform = "rotate(0deg)";
      }
    },
    updateData(variabel){
      this.periode = variabel;
    },
    updateKindData(variabel2){
      this.kind = variabel2;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
#nav{
  height: 100%;
  width: 360px;
  position: fixed;
  z-index: 1;
  top: 0px;
  background-color: #eaeaea;
  overflow-x: hidden;
  left: -360px;
  transition: all 0.2s ease;
  box-shadow: 1px 0 10px 0 #a29d9d;
}
#menuButton{
  position: fixed;
  left:5px;
  bottom:5px;
  z-index: 100;
  transition: all 0.2s ease;
  width: 20px;
}
#menuIcon:hover{
  filter: invert(100%); 
  transition: all 0.2s ease;
  cursor: pointer;
}
#content{
  margin-left: 0px;
  background-color: white;
  top: 0px;
  left: 0px;
  transition: all 0.2s ease;
}
</style>
