<style scoped lang="scss">
  $blue: #49c8fd;
  $s-width: 700px;
  $s-height: 396px;
  @mixin slideSize ($s-width, $s-height) {
    width: $s-width;
    height: $s-height;
  }
  .slide {
    position: relative;
    overflow: hidden;
    @include slideSize($s-width, $s-height);
    img {
      @include slideSize($s-width, $s-height);
    }
    .img-box {
      a{
        float: left;
        position: absolute;
      }
      .title {
        position: absolute;
        // padding: 0 15px;
        text-indent: 15px;
        width: $s-width;
        bottom: 0px;
        $height: 52px;
        height: $height;
        line-height: $height;
        background: linear-gradient(to top, rgba(0,0,0,0.6), transparent);
        font: {
          size: 21px;
          family: 'Microsoft YaHei';
          weight: bold;
        }
        color: #fff;
        &:hover {
          color: $blue;
        }
      }
    }
    
    .switch-bar {
      padding: 15px;
      position: absolute;
      right: 0;
      bottom: 5px;
      .switch-btn {
        $rect: 10px;
        width: $rect;
        height: $rect;
        float: left;
        margin-right: 10px;
        border-radius: $rect/2;
        background-color: #f3eae9;
        cursor: pointer;
      }
      .cur {
        width: 25px;
        background-color: #ff6041;
      }
    }
    $pn-btn-width: 34px;
    $pn-btn-height: 47px;
    $pn-btn-top: 147px;
    [name=prev-btn], [name=next-btn] {
      width: $pn-btn-width;
      height: $pn-btn-height;
      position: absolute;
      top: $s-height/2 - $pn-btn-height/2;
      z-index: 2;
      background: url("http://image.gamersky.com/webimg15/slide-btn.png") no-repeat;
      cursor: pointer;
      opacity: 0;
    }
    &:hover {
      [name=prev-btn], [name=next-btn]{
        transition: opacity 0.5s;
        opacity: 1;
      }
    }
    [name=prev-btn] {
      left: 0;
      border-radius: 0 5px 5px 0;
      &:hover {
        background-position-y: -47px;
      }
    }
    [name=next-btn] {
      right: 0;
      background-position-x: -34px;
      border-radius: 5px 0 0 5px;
      &:hover {
        background-position: -34px -47px;
      }
    }
  }
  #prev {
    left: -$s-width;
  }
  #next {
    left: $s-width;
  }
</style>

<template>
  <div class="slide" v-if="slideNews.length" @mouseenter="clearInv" @mouseleave="runInv">
    <div class="img-box">
      <a target="_blank" id="prev"
      :href="slideNews[prevIndex].href" 
      :style="">
        <img 
        :src="slideNews[prevIndex].src"  
        :alt="slideNews[prevIndex].title">
        <div class="title"> {{slideNews[prevIndex].title}} </div>
      </a>
      <a target="_blank" id="now"
      :href="slideNews[nowIndex].href" 
      :style="nowImgStyle">
        <img 
        :src="slideNews[nowIndex].src"  
        :alt="slideNews[nowIndex].title">
        <div class="title"> {{slideNews[nowIndex].title}} </div>
      </a>
      <a target="_blank" id="next"
      :href="slideNews[nextIndex].href" 
      :style="" >
        <img 
        :src="slideNews[nextIndex].src"  
        :alt="slideNews[nextIndex].title">
        <div class="title"> {{slideNews[nextIndex].title}} </div>
      </a>
    </div>
    <div class="switch-bar">
      <span class="switch-btn" v-for="(item, index) of slideNews" :class="{cur: index === nowIndex}" @click="goto(index)"></span>
    </div>
    <span name="prev-btn" @click="goto(prevIndex, 'right')"></span>
    <span name="next-btn" @click="goto(nextIndex, 'left')"></span>
  </div>
</template>

<script>
export default {
  props: {
    slideNews: {
      type: Array,
      default: []
    },
    inv: {
      type: Number,
      default: 2
    }
  },
  data () {
    return {
      nowIndex: 0,
      showLeft: false,
      showRight: false,
      duration: 0.3, // 左右移动的动画时间 (s)
      nowImgStyle: {
        display: 'block'
      }
    }
  },
  computed: {
    prevIndex () {
      if (this.nowIndex === 0) {
        return this.slideNews.length - 1
      } else {
        return this.nowIndex - 1
      }
    },
    nextIndex () {
      if (this.nowIndex === this.slideNews.length - 1) {
        return 0
      } else {
        return this.nowIndex + 1
      }
    }
  },
  methods: {
    goto (index, position) {
      let oldIndex = this.nowIndex
      this.nowIndex = index
      if (!position) {
        if (index > oldIndex) position = 'left'
        else position = 'right'
      }
      // window.alert(position)
      this.nowImgStyle.transitionDuration = this.duration + 's'
      // if (position === 'left') {
      //   this.nowImgStyle.transform = 'translateX(-700px)'
      // }
      // if (position === 'right') {
      //   this.nowImgStyle.transform = 'translateX(700px)'
      // }
      setTimeout(() => {
        this.nowImgStyle.transform = 'translateX(-700px)'
        console.dir(this.nowImgStyle.transform)
      }, this.duration * 1000)
    }
  /*  runInv () {
      this.invId = setInterval(() => {
        this.goto(this.nextIndex)
      }, this.inv * 1000)
    }, */
   /* clearInv () {
      clearInterval(this.invId)
    } */
  },
  mounted () {
    this.runInv()
  }
}
</script>
