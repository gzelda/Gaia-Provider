<template>
  <div class="block">
    
    <transition name="" appear
                  @before-enter="handleBeforeEnter"
                  @enter="handleEnter"
                  @after-enter="handleAfterEnter"
                  @before-leave="handleBeforeLeave"
                  @leave="handleLeave"
                  @after-leave="handleAfterLeave"
                  :css="false">
        <div class="circle" v-if="show"></div>
    </transition>
    <div class="sensors">
        <div v-for="(sensor,index) in sensors" :key="index" class="sensor">
            <div class="circle"></div>
        </div>
    </div>
    <div class="gaia">
        <div class="gaiaCircle"></div>
    </div>

    <div class="evm">
        <div class="evmCircle"></div>
    </div>
  </div>
</template>

<script>
import Velocity from 'velocity-animate'
export default {
  name: 'diagram',
  props: ['user'],
  data () {
    return {
        show:false,
        sensors:[1, 2, 3, 4, 5, 6, 7]
    }
  },
  methods: {
    hide(){
      this.show = !this.show
    },
    handleBeforeEnter: function (el) {
        el.style.opacity = 0;
        console.log('方块显示动画即将执行');
    },
    handleEnter: function (el, done) {
      Velocity(el, 'stop');
      Velocity(el, {
        backgroundColor: '#ffffff',
        opacity: 1,
        translateX: 260,
        translateY: 100
      }, {
        duration: 1000,
        complete: done
      });
      console.log('方块显示动画执行中...');
    },
    handleAfterEnter: function (el) {
      console.log('方块显示动画结束');
    },
    handleBeforeLeave: function (el) {
      console.log('方块隐藏动画即将执行');
    },
    handleLeave: function (el, done) {
      Velocity(el, 'stop');
      Velocity(el, {
        backgroundColor: '#ffffff',
        opacity: 0,
        translateX: 0
      }, {
        duration: 1000,
        complete: done
      });
      console.log('方块隐藏动画执行中...');
    },
    handleAfterLeave: function (el) {
      console.log('方块隐藏动画结束');
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.block{
            display: flex;
            padding: 20px 20px 20px 20px;
            height: 100%;
        }
.circle {
			background: #ffffff;
			height: 20px;
			width: 20px;			
			border-radius: 10px;
        }

.gaiaCircle{
    background: #ffffff;
    border-radius: 50px;
    height: 100px;
	width: 100px;
}

.evmCircle{
    background: #ffffff;
    border-radius: 80px;
    height: 160px;
	width: 160px;
}

.sensors{   
            display:flex;
            flex-direction:column;
            height: 100%;
            width: 200px;
            justify-content: center;
            align-items: center;
        }
.sensor{
    padding: 10px 10px 10px 10px;
}
.gaia{
    
    display:flex;
    justify-content: center;
    align-items: center;
    width: 200px;
    height:100%;
}

.evm{
    display:flex;
    justify-content: center;
    align-items: center;
    width:50%;
    height:100%;
}
</style>
