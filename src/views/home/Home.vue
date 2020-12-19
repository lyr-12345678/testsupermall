<template>
  <div id="home">
  <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
  <scroll class="content" ref="scroll"
          :probe-type="3"
          @scroll="contentClick"
          @pullingUp="loadMore"
          :pull-up-load="true">
  <home-swiper :banners="banners"/>
  <recommend-view :recommends="recommends"/>
  <feature-view />
  <tab-control class="tab-control" :titles="['流行','新款','精选']"/>
  <goods-list :goods="showGoods" @tabClick="tabClick(index)" />
    <ul>
      <li>分类1</li>
      <li>分类2</li>
      <li>分类3</li>
      <li>分类4</li>
      <li>分类5</li>
      <li>分类6</li>
      <li>分类7</li>
      <li>分类8</li>
      <li>分类9</li>
      <li>分类10</li>
      <li>分类11</li>
      <li>分类12</li>
      <li>分类13</li>
      <li>分类14</li>
      <li>分类15</li>
      <li>分类16</li>
      <li>分类17</li>
      <li>分类18</li>
      <li>分类19</li>
      <li>分类20</li>
      <li>分类21</li>
      <li>分类22</li>
      <li>分类23</li>
      <li>分类24</li>
      <li>分类25</li>
      <li>分类26</li>
      <li>分类27</li>
      <li>分类28</li>
      <li>分类29</li>
      <li>分类30</li>
      <li>分类31</li>
      <li>分类32</li>
      <li>分类33</li>
      <li>分类34</li>
      <li>分类35</li>
      <li>分类36</li>
      <li>分类37</li>
      <li>分类38</li>
      <li>分类39</li>
      <li>分类40</li>
      <li>分类41</li>
      <li>分类42</li>
      <li>分类43</li>
      <li>分类44</li>
      <li>分类45</li>
      <li>分类46</li>
      <li>分类47</li>
      <li>分类48</li>
      <li>分类49</li>
      <li>分类50</li>
    </ul>
   </scroll >
  <back-top @click.native="backTopClick" v-show="isShowBackTop "/>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'
import Scroll from 'components/common/scroll/Scroll'

import TabControl from 'components/content/tabcontrol/TabControl'
import GoodsList from 'components/content/goods/GoodsList'


import HomeSwiper from './childComp/HomeSwiper'
import RecommendView from './childComp/RecommendView'
import FeatureView from './childComp/FeatureView'


import {getHomeMultidata,getHomeGoods} from 'network/home'
import BackTop from 'components/content/backTop/BackTop'


export default {
  name: "Home",
  components:{
    NavBar,
    Scroll,
    TabControl,
    GoodsList,
    HomeSwiper,
    RecommendView,
    FeatureView,
    BackTop

  },
  data(){
    return{
    banners:[],
    recommends:[],
      goods:{
      'pop':{page:0,list:[]},
      'news':{page:0,list:[]},
      'sell':{page:0,list:[]}
      },
      currentType:'pop',
      isShowBackTop:false
    }
  },
  created() {
    // 请求多个数据
 this.getHomeMultidata()
    // 请求多个数据
    // this.getHomeGoods('pop')
    // this.getHomeGoods('news')
    // this.getHomeGoods('sell')
  },
  computed:{
    showGoods(){
      return this.goods[this.currentType].list
    }
  },
  methods:{
    tabClick(index){
      switch (index){
        case 0:
          this.currentType='pop'
          break
        case 1:
          this.currentType='news'
          break
        case 2:
          this.currentType='sell'
          break
      }
    },
    backTopClick(){
      this.$refs.scroll.scroll.scrollTo(0,0,500)
    },
    contentClick(position){
     this.isShowBackTop=(-position.y)>50
    },
    loadMore(){
      // this.getHomeGoods(this.currentType)
      this.$refs.scroll.scroll.refresh()

    },
    getHomeMultidata(){
      // 请求多个数据
      getHomeMultidata().then(res=>{
        this.banners=res.data.banner.list
        this.recommends=res.data.recommend.list

      })
    },
    getHomeGoods(type){
      // 请求商品数据
      const page=this.goods[type].page+1
      getHomeGoods(type,page).then(res=>{

        this.goods[type].list.push(...res.data.list)
        this.goods[type].page+=1
        this.$refs.scroll.scroll.finishPullUp()
      })
    }
  }


}
</script>

<style scoped>
#home{
  padding-top: 44px;
  height: 100vh;
}
.home-nav{
background-color: #ff5777;
  color: #fff;
  position: fixed;

  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}
.tab-control{
  position: sticky;
  top: 44px;
}
.content{
 overflow: hidden;
  position: absolute;
  top: 5px;
  bottom: 49px;
  left: 0;
  right: 0;

}
</style>
