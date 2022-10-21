<script lang="ts">
import { reactive } from 'vue'
export default {

  setup() {
    let foodList: Array<string> = ['日式咖喱', '泰式咖喱', '印度咖喱', '韩式鱼饼', '巧克力蛋糕', 'pizza', '炒年糕', '夜市大排档', '厚多士', '日式寿司', '墨西哥taco', '潮汕粥', '紫菜包饭', '港式滑蛋饭', '奶油烩饭', '天上飞的食物', '带五种颜色的食物', '盒马（仅限新品）', 'OLE打折的食物', '让朋友随机发表情包', '大众点评页面推荐第一个', '自助餐', '煎三文鱼', '东北大饭包', '流沙包', '7-11便利店']

    const state = reactive({money:0,food: "", inChoose: false, pick:0});

    function choose() {
      if( state.inChoose) {
        state.inChoose = false;
        clearInterval(state.pick);
      } else {
        state.pick = setInterval(changeState,50);
        state.inChoose = true;
      }
      
    }

    function changeState() {
      state.money = Math.floor(Math.random() * 300 + 50)
      state.food = foodList[Math.floor(Math.random() * foodList.length)]
    }

    return {
      state,
      choose,
    }

  }
}
</script>

<template>
  <div class="container">
    <div class="wrapper">今天的钱 {{ state.money}}</div>
    <div class="wrapper">今天吃{{state.food}}</div>
    <button id="float" @click="choose">{{state.inChoose?"停！":"抽奖"}}</button>
  </div>

</template>

<style scoped>
.container {
  display: flex;
  justify-content: space-around;
  max-height: 100vh;
  min-height: 100vh;
  min-width: 100vw;

}

.container .wrapper {
  border: 1px;
  border-style: dashed;
  width: 50%;
  border-color: white;
  text-align: center;
}

#float {
  position: absolute;
  bottom: 20vh;
  z-index: 100;
}

@media screen and (max-width: 1080px) {
  .container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  max-height: 100vh;
  min-height: 100vh;
  min-width: 100vw;

}

.container .wrapper {
  width: 100%;
  border-color: white;
  text-align: center;

}

#float {
  position: absolute;
  bottom: 1vh;
  z-index: 100;
}
  
}
</style>
