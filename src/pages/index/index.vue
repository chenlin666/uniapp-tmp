<template>
  <view class="content">
    <image class="logo" src="/static/logo.png"></image>
    <canvas
      style="width: 300px; height: 200px"
      canvas-id="firstCanvas"
      id="firstCanvas"
    ></canvas>
    <button type=""></button>
  </view>
</template>

<script>
import { Game } from "@eva/eva.js";
import { RendererSystem } from "@eva/plugin-renderer";

export default {
  data() {
    return {
      title: "Hello",
    };
  },
  onLoad() {},
  methods: {},
  onReady: function (e) {
    var context = uni.createCanvasContext("firstCanvas");

    const query = uni.createSelectorQuery().in(this);
    query
      .select("#firstCanvas")
      .fields({
        node: true,
        size: true,
      })
      .exec((data) => {
        console.log(data);
      });

    console.log(context);
    // 创建渲染系统
    const rendererSystem = new RendererSystem({
      canvas: context, // 可选，自动生成 canvas 挂在 game.canvas 上
      width: 750,
      height: 1000,
      transparent: false,
      resolution: window.devicePixelRatio / 2, // 可选, 如果是2倍图设计 可以除以2
      enableScroll: true, // 允许页面滚动
      renderType: 0, // 0:自动判断，1: WebGL，2:Canvas，建议android6.1 ios9 以下使用Canvas，需业务判断。
    });
    console.log(rendererSystem);
    // // 创建游戏对象
    const game = new Game({
      frameRate: 60, // 可选，游戏帧率，默认60
      autoStart: true, // 可选，自动开始
      systems: [rendererSystem],
    });
  },
};
</script>

<style lang="scss"></style>
