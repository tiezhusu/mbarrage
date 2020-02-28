<template>
  <div id="mbarrage">
      <div class="mbarrage-bullet bullet-active" :class=[{active:isScroll},{pause:isShow}] v-for="(item,index) of list" :key="index">{{item.msg}}</div>
      <!-- <div class="mbarrage-bullet">这是一条测试用弹幕</div> -->
  </div>
</template>

<script>

export default {
  name: 'App',
  props: {
    barrageList: {
      type: Array,
      default() {
        return []
      }
    },
    bulletBorder:{
      type: Boolean,
      default: false,
    },
    bulletAvatar:{
      type: Boolean,
      default: false,
    },
    bulletNickname: {
      type: Boolean,
      default: false,
    },
    bulletFontSize: {
      type: Number,
      default: 28,
    },
    bulletFontStyle: {
      type: String,
      default: 'Arial'
    },
    scrollSpeed: {
      type: Number,
      default: 1
    }
  },
  data() {
      return {
          list: [],
          isScroll: false,
          isShow: false,
          number: 1,
      }
  },
  methods:{
      init(){
          for (let i = 0; i < 10; i++) {
              this.list.push({
                msg: `填充弹幕1信息`
            })
          }
          
          
            setTimeout(() => {
                this.isScroll = true
            },2000)
            setTimeout(() => {
                // let list = document.getElementsByClassName('active')
                this.isShow = true

                // for(let item of list) {
                //     console.log(item)
                // }
                // this.isScroll = false
            },6000)
            setTimeout(() => {
                this.isShow = false
            },10000)
      },
      initbullet(){
          let bullet = document.createElement('div');
          bullet.className = 'mbarrage-bullet'
          bullet.innerText = '这是一条弹幕，测试transition'
          let barrage = document.getElementById('mbarrage')
          barrage.addEventListener('animationend',function(){
              console.log('动画播放完毕')
          })
          barrage.appendChild(bullet)

          setTimeout(() => {
              let Bullet = document.getElementsByClassName('mbarrage-bullet')
              Bullet[0].className = 'mbarrage-bullet bullet-active'
          },2000)
      }
  },
  mounted() {
      this.init()
        // this.initbullet()
  }
}
</script>

<style>
#mbarrage {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
.mbarrage-bullet{
    position: absolute; /* 重要样式 */
    left:100%;  /* 重要样式 */
    top:0;      /* 重要样式 */
    white-space: nowrap;
    /* user-select: none; */
}
.active{
    
    transform: translateX(-1000px);
    will-change:transform;   /* 重要样式 */
    /* transition:transform 7s linear; 重要样式 */
    animation: move 7s linear;
}

@keyframes move {
    0% {
        transform: translateX(0);
    }
    100% {
        transform: translateX(-1000px)
    }

    
}
.pause{
    animation-play-state:paused;
}
</style>
