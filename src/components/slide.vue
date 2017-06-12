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
    @include slideSize($s-width, $s-height);
    img {
      @include slideSize($s-width, $s-height);
    }
    ul {
      li {
        list-style: none;
        .title {
          position: absolute;
          padding: 0 15px;
          width: auto;
          bottom: 0px;
          $height: 52px;
          height: $height;
          line-height: $height;
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
    }
    .switch-bar {
      padding: 15px;
      position: absolute;
      right: 0;
      bottom: 5px;
      .switch-btn {
        transition: width 0.3s;
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
</style>

<template>
  <div class="slide" v-if="slideNews.length" @mouseenter="clearInv" @mouseleave="runInv">
    <ul>
      <li>
        <a :href="slideNews[nowIndex].href" target="_blank">
          <transitoion name="slide-trans">
            <img v-if="isShow" :src="slideNews[nowIndex].src" alt="">
            <div v-if="isShow" class="title"> {{slideNews[nowIndex].title}} </div>
          </transitoion>
          <transitoion name="slide-trans-old">
            <img v-if="!isShow" :src="slideNews[nowIndex].src" alt="">
            <div v-if="!isShow" class="title"> {{slideNews[nowIndex].title}} </div>
          </transitoion>
        </a>
      </li>
    </ul>
    <div class="switch-bar">
      <span class="switch-btn" v-for="(item, index) of slideNews" :class="{cur: index === nowIndex}" @click="goto(index)"></span>
    </div>
    <span name="prev-btn" @click="goto(prevIndex)"></span>
    <span name="next-btn" @click="goto(nextIndex)"></span>
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
      isShow: true
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
    goto (index) {
      this.nowIndex = index
    },
    runInv () {
      this.invId = setInterval(() => {
        this.goto(this.nextIndex)
      }, this.inv * 1000)
    },
    clearInv () {
      clearInterval(this.invId)
    }
  },
  mounted () {
    this.runInv()
  }
}
</script>
