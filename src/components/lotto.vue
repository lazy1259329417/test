<template>
  <div class="total">
    <span v-for="(item, index) in imgs" :key="index"><img :src="item" alt="" /></span>
    <span @click="Begin()"><img src="../img/9.png" alt="" /></span>
  </div>
</template>

<script>
export default {
    data() {
        return {
            flag: 1,
            imgs: [
                require("../img/1.png"),
                require("../img/2.png"),
                require("../img/3.png"),
                require("../img/4.png"),
                require("../img/5.png"),
                require("../img/6.png"),
                require("../img/7.png"),
                require("../img/8.png")
            ],
            imgs1: [
                require("../img/1.png"),
                require("../img/2.png"),
                require("../img/3.png"),
                require("../img/4.png"),
                require("../img/5.png"),
                require("../img/6.png"),
                require("../img/7.png"),
                require("../img/8.png")
            ],//用来每走过的前一格置为白板
            imgs2: [
                [require("../img/1.1.png"),'随时用上温热的干毛巾电热烘干毛巾架'],
                [require("../img/2.1.png"),'10元满减红包'],
                [require("../img/3.1.png"),'2积分'],
                [require("../img/4.1.png"),'春暖花开随身出行胖喵焖烧罐'],
                [require("../img/5.1.png"),'5元满减红包'],
                [require("../img/6.1.png"),'开箱即用移动方便可折叠多层置物架'],
                [require("../img/7.1.png"),'3元直减红包'],
                [require("../img/8.1.png"),'全场满99减10']
            ]//用来当停止时改变img的src属性值（即抽中的为深色格）
        }
    },
    methods: {
        Begin(){
            if(this.flag === 0){return}//当flag=0时（即九宫格还在转动，不能再次点击）
            let index = 0
            let stop = 0
            let num = 40 + Math.floor(Math.random() * 20)//取随机数
            for (let i = 0; i < this.imgs.length; i++) {
                 this.imgs[i] = this.imgs1[i];
            }//当点击抽奖按钮时九宫格为空（还未中奖）
            let turn = setInterval(()=>{
                this.flag = 0//开始转动时，flag=0（即不能再点击）
                if (index===0) {
                    this.imgs[this.imgs.length-1] = this.imgs1[this.imgs.length-1]
                }//九宫格的最后一格（即第一格的前一格）为白
                this.imgs[index] = this.imgs2[index][0]//当前格为深色（即抽中）
                this.imgs[index-1] = this.imgs1[index-1]//每走过一格的前一格置为白
                index++
                if (index>this.imgs.length-1) {
                    index=0
                }//index为数组最大下标时置0
                stop++
                if (stop===num) {
                    clearInterval(turn)
                    this.flag = 1//停止时flag=1，可再次点击抽奖按钮
                    setTimeout(()=>{
                      alert('恭喜你获得大奖：'+this.imgs2[index-1][1])
                    })
                }
            },60)
        }
    },
};
</script>

<style>
img {
  width: 100px;
  height: 100px;
}
span {
  width: 100px;
  height: 100px;
  margin: 5px;
}

.row {
  float: left;
}
span:nth-child(4) {
  position: absolute;
  top: 110px;
  right: 0;
}
span:nth-child(5) {
  position: absolute;
  top: 220px;
  right: 0;
}

span:nth-child(6) {
  position: absolute;
  top: 220px;
  right: 110px;
}
span:nth-child(7) {
  position: absolute;
  top: 220px;
  left: 0;
}
span:nth-child(8) {
  position: absolute;
  top: 110px;
  left: 0;
}
span:nth-child(9) {
  background: rgb(255, 148, 61);
  position: absolute;
  top: 110px;
  right: 110px;
}
.total {
  width: 330px;
  height: 330px;
  position: relative;
  left: 50%;
  transform: translate(-50%, 30%);
}
</style>