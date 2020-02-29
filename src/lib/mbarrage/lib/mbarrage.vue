<template>
  <div id="mbarrage">
      <div class="mbarrage-bullet bulletActive" :class="{scrollPause:!isScroll,scrollRestart:isScroll}" v-for="(item,index) of list" :key="index">{{item.msg}}</div>
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
          isScroll: true,
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
                this.isScroll = false
            },2000)
            setTimeout(() => {
                // let list = document.getElementsByClassName('active')
                // this.isShow = true

                // for(let item of list) {
                //     console.log(item)
                // }
                this.isScroll = true
            },6000)
            setTimeout(() => {
                // this.isShow = false
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
      },
      $addBullet(item){
        // 使用v-for来生成dom的话，有个问题，无法为每条弹幕设置初始位置
        // 后续可能还是要用手动插入dom的形式来
        console.log(item)
      },
      $pauseScroll(){
        this.isScroll = false
      },
      $startScroll(){
        this.isScroll = true
      },
      $clearBarrageList(){
        // 暂时没有头绪
        // 或者到时候，还是分成  正在发送的弹幕池，待发送的弹幕池？
      },
      $resetCanvas() {
        
      },

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
.bulletActive{
    
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
.scrollPause{
    animation-play-state: paused;
}
.scrollRestart{
    animation-play-state: running;

}
</style>
