<style scoped lang="scss">
  $blue: #49c8fd;
  @mixin slideSize {
    width: 700px;
    height: 396px;
  }
  .slide {
    position: relative;
    @include slideSize;
    img {
      @include slideSize;
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
</style>

<template>
  <div class="slide">
    <ul>
      <li>
        <a :href="slides[nowIndex].href" target="_blank">
          <img :src="slides[nowIndex].src" alt="">
          <div class="title"> {{slides[nowIndex].title}} </div>
        </a>
      </li>
    </ul>
    <div class="switch-bar">
      <span class="switch-btn" v-for="(item, index) of slides" :class="{cur: index === nowIndex}" @click="goto(index)">
      </span>
    </div>
  </div>  
</template>

<script>
export default {
  props: ['slides'],
  data () {
    return {
      nowIndex: 0
    }
  },
  methods: {
    goto (index) {
      this.nowIndex = index
    }
  }
  /* ,mounted () {
    window.console.log(this.slides)
  } */
}
</script>
