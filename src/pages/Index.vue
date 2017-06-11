<template>
  <div class="index-wrap">
    <div class="index-left">
      <div class="index-left-block">
        <h2>全部产品</h2>
        <template v-for="product in productList">
          <h3>{{ product.title }}</h3>
          <ul>
            <li v-for="item of product.list">
              <a :href="item.url" :class="{'hot': item.hot,'faq':true}">{{ item.name }}</a>
              <!--<span class="hot-tag" v-if="item.hot">HOT</span>-->
            </li>
          </ul>
          <div v-if="!product.last" class="hr"></div>
        </template>
      </div>
      <div class="index-left-block lastest-news">
        <h2>最新消息</h2>
        <ul>
          <li v-for="news in newsList">
            <a :href="news.url" class="new-item">{{ news.title }}</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="index-right">
      <slide :slides="slides"></slide>
      <div class="index-board-list">
        <div
          class="index-board-item" 
          v-for="(item, index) in boardList"
          :class="[{'line-last': index % 2},
          'index-board-' + item.id]"
        >
          <div class="index-board-item-inner">
            <h2>{{item.title}}</h2>
            <p>{{item.description}}</p>
            <div class="index-board-button">
              <a href="" class="button">立即购买</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Slide from '../components/slide.vue'
export default {
  components: {
    Slide
  },
  // 创建完毕之后
  created: function () {
    this.$http.post('api/getNewsList')
    .then((data) => {
      this.newsList = data.data
    }, (err) => {
      console.log(err)
    })
  },
  data () {
    return {
      slides: [
        {
          title: '《星战前线2》新实机演示 后续DLC全免费',
          href: 'http://www.gamersky.com/news/201706/914531.shtml',
          src: 'http://image.gamersky.com/gameshd/2017/20170611_wyc_246_5.jpg'
        },
        {
          title: 'EA新作《逃出生天》公布 兄弟合作逃狱',
          href: 'http://www.gamersky.com/news/201706/914498.shtml',
          src: 'http://image.gamersky.com/gameshd/2017/20170611_wyc_246_3.jpg'
        },
        {
          title: '《极品飞车20》实机演示 劲爆飙车场面',
          href: 'http://www.gamersky.com/news/201706/914500.shtml',
          src: 'http://image.gamersky.com/gameshd/2017/20170611_wyc_246_2.jpg'
        },
        {
          title: 'BF1俄国DLC宣传片 冰天雪地残酷大战',
          href: 'http://www.gamersky.com/news/201706/914536.shtml',
          src: 'http://image.gamersky.com/gameshd/2017/20170611_wyc_246_1.jpg'
        }
      ],
      productList: {
        pc: {
          title: 'pc产品',
          list: [
            {
              name: '数据统计',
              url: ''
            },
            {
              name: '数据预测',
              url: ''
            },
            {
              name: '数据分析',
              url: ''
            },
            {
              name: '流量分析',
              url: '',
              hot: true
            }
          ]
        },
        app: {
          title: '手机app类',
          last: true,
          list: [
            {
              name: '91助手',
              url: ''
            },
            {
              name: '产品助手',
              url: ''
            },
            {
              name: '智能地图',
              url: ''
            },
            {
              name: '团队语音',
              url: ''
            }
          ]
        }
      },
      newsList: [],
      boardList: [
        {
          title: '开放产品',
          description: '开放产品是一款开放产品',
          id: 'car',
          toKey: 'analysis',
          saleout: false
        },
        {
          title: '品牌营销',
          description: '品牌营销帮助你的产品更好地找到定位',
          id: 'earth',
          toKey: 'count',
          saleout: false
        },
        {
          title: '使命必达',
          description: '使命必达快速迭代永远保持最前端的速度',
          id: 'loud',
          toKey: 'forecast',
          saleout: true
        },
        {
          title: '勇攀高峰',
          description: '帮你勇闯高峰，到达事业的顶峰',
          id: 'hill',
          toKey: 'publish',
          saleout: false
        }
      ]
    }
  }
}
</script>

<style scoped>
.index-wrap {
  width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}
.index-left {
  float: left;
  width: 300px;
  text-align: left;
}
.index-right {
  float: left;
  width: 900px;
}
.index-left-block {
  margin: 15px;
  background: #fff;
  box-shadow: 0 0 1px #ddd;
}
.index-left-block .hr {
  margin-bottom: 20px;
}
.index-left-block h2 {
  background: #4fc08d;
  color: #fff;
  padding: 10px 15px;
  margin-bottom: 20px;
}
.index-left-block h3 {
  padding: 0 15px 5px 15px;
  font-weight: bold;
  color: #222;
}
.index-left-block ul {
  padding: 10px 15px;
}
.index-left-block li {
  padding: 5px;
}
.index-board-list {
  overflow: hidden;
}
.index-board-item {
  float: left;
  width: 400px;
  background: #fff;
  box-shadow: 0 0 1px #ddd;
  padding: 20px;
  margin-right: 20px;
  margin-bottom: 20px;
}
.index-board-item-inner {
  min-height: 125px;
  padding-left: 120px;
}
.index-board-car .index-board-item-inner{
  background: url(../assets/images/car.png) no-repeat;
}
.index-board-loud .index-board-item-inner{
  background: url(../assets/images/earth.png) no-repeat;
}
.index-board-earth .index-board-item-inner{
  background: url(../assets/images/hill.png) no-repeat;
}
.index-board-hill .index-board-item-inner{
  background: url(../assets/images/loud.png) no-repeat;
}
.index-board-item h2 {
  font-size: 18px;
  font-weight: bold;
  color: #000;
  margin-bottom: 15px;
}
.line-last {
  margin-right: 0;
}
.index-board-button {
  margin-top: 20px;
}
.lastest-news {
  min-height: 512px;
}
.hot-tag {
  background: red;
  color: #fff;
}
.new-item {
  display: inline-block;
  width: 230px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.hot {
  color: #d9502d;
}
</style>
