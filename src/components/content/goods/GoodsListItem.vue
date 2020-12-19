<template>
<div class="goods-item">
<div>
  <img :src="goodsItem.show.image" alt="">
  <div>
    <p>{{goodsItem.title}}</p>
    <span class="price">{{goodsItem.price}</span>
    <span class="collect">{{goodsItem.cfav}}</span>
  </div>
</div>
</div>
</template>

<script>

export default {
name: "GoodsListItem",
  props:{
  goodsItem:{
    type:Object,
    default(){
      return {}
    }
  }
  }
}
</script>

<style scoped>

</style>
