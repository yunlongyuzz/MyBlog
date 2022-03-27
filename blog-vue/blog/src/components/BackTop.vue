<template>
  <div class="rightside" :style="isShow">

    <div :class="'rightside-config-hide ' + isOut">
      <i :class="'iconfont rightside-icon ' + icon" @click="check" />
      <i :class="'iconfont rightside-icon ' + flower" @click="Flowercheck" />
      <i :class="'iconfont rightside-icon ' + rain" @click="Raincheck" />
    </div>


    <div class="setting-container" @click="show">
      <i class="iconfont iconshezhi setting" />
    </div>

    <!--返回顶部 -->
    <i @click="backTop" class="iconfont rightside-icon iconziyuanldpi" />
  </div>
</template>

<script>

import "../assets/css/flower/iconfont.css";
import "../assets/css/BanFlower/iconfont.css";
import "../assets/css/rain/iconfont.css";
import {Rain} from "../../public/stastic/js/rain.js";

export default {
  mounted() {
    window.addEventListener("scroll", this.scrollToTop);
  },
  destroyed() {
    window.removeEventListener("scroll", this.scrollToTop);
  },
  data: function() {
    return {
      isShow: "",
      isOut: "rightside-out",
      icon: "iconyueliang",
      flower: "icon-weixinhua",
      rain: "icon-weixinxiayu",
      ban: "icon-ai47"
    };
  },
  methods: {
    // 回到顶部方法
    backTop() {
      window.scrollTo({
        behavior: "smooth",
        top: 0
      });
    },
    // 为了计算距离顶部的高度，当高度大于100显示回顶部图标，小于100则隐藏
    scrollToTop() {
      const that = this;
      let scrollTop =
        window.pageYOffset ||
        document.documentElement.scrollTop ||
        document.body.scrollTop;
      that.scrollTop = scrollTop;
      if (that.scrollTop > 20) {
        that.isShow = "opacity: 1;transform: translateX(-38px);";
      } else {
        that.isShow = "";
      }
    },
    show() {
      const flag = this.isOut == "rightside-out";
      this.isOut = flag ? "rightside-in" : "rightside-out";
    },
    check() {
      const flag = this.icon == "iconyueliang";
      this.icon = flag ? "icontaiyang" : "iconyueliang";
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },
    Flowercheck() {
      const flag = this.flower == "icon-weixinhua";
      this.flower = flag ? "icon-ai47" : "icon-weixinhua";
      this.rain = flag ? "icon-ai47" : "icon-weixinxiayu";

      if (this.flower == "icon-ai47"){
        import("../../public/stastic/js/sakura-small.js");
      }else {
        location.reload();
      }
    },
    Raincheck() {
      const flag = this.rain == "icon-weixinxiayu";
      this.rain = flag ? "icon-ai47" : "icon-weixinxiayu";
      this.flower = flag ? "icon-ai47" : "icon-weixinhua";

      if (this.rain == "icon-ai47"){

        Rain({speed:[2,40],hasBounce:false,wind_direction:340,gravity:0.05,maxNum:80,numLevel:5,drop_chance:0.4,cloud:true});

      }else {
        location.reload();
      }

    }

    },
};
</script>


<style scoped>
.rightside {
  z-index: 4;
  position: fixed;
  right: -38px;
  bottom: 85px;
  transition: all 0.5s;
}
.rightside-config-hide {
  transform: translate(35px, 0);
}
.rightside-out {
  animation: rightsideOut 0.3s;
}
.rightside-in {
  transform: translate(0, 0) !important;
  animation: rightsideIn 0.3s;
}
.rightside-icon,
.setting-container {
  display: block;
  margin-bottom: 2px;
  width: 30px;
  height: 30px;
  background-color: #49b1f5;
  color: #fff;
  text-align: center;
  font-size: 16px;
  line-height: 30px;
  cursor: pointer;
}
.rightside-icon:hover,
.setting-container:hover {
  background-color: #ff7242;
}
.setting-container i {
  display: block;
  animation: turn-around 2s linear infinite;
}
@keyframes turn-around {
  0% {
    transform: rotate(0);
  }
  100% {
    transform: rotate(360deg);
  }
}
@keyframes rightsideOut {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(30px, 0);
  }
}
@keyframes rightsideIn {
  0% {
    transform: translate(30px, 0);
  }
  100% {
    transform: translate(0, 0);
  }
}
</style>
