<template>
  <div class="tomato">
    <div class="tomato__left">
      <div class="tomato__left__clock">
        <audio
          ref="audioPlayer"
          preload>
          <source src="./music/clock_sound_1.mp3"></source>
          Your browser isn't invited for super fun audio time.
        </audio>
        <div 
          class="tomato__left__clock__button"
          @click="playClick">
          <i 
            v-if="!isCountDown"
            class="fas fa-play"></i>
          <i
            v-else
            class="fas fa-pause"></i>
        </div>
        <div class="tomato__left__clock__circle"></div>
        <div class="tomato__left__clock__leaf">
          <img src="./images/leaf.svg">  
        </div>
      </div>
      <div class="tomato__left__info">
        <div class="tomato__left__info__time">
          <h2 v-html="showNowTime"></h2>
        </div>
        <div class="tomato__left__info__line"></div>
        <p
          class="tomato__left__info__title"
          v-html="nowMissing"></p>
      </div>
    </div>
    <div class="tomato__right">
      <div class="tomato__right__menu">
        <div
          :class="{active: nowShow === 'ToDoList'}"
          class="item"
          @click="changeComponent('ToDoList')">
          <div class="item__icon">
            <i class="fas fa-list"></i>
          </div>
          <div class="item__text">TO DO LIST</div>
        </div>
        <div 
          :class="{active: nowShow === 'Analyics'}"
          class="item"
          @click="changeComponent('Analyics')">
          <div class="item__icon">
            <i class="far fa-chart-bar"></i>
          </div>
          <div class="item__text">ANALYTICS</div>
        </div>
        <div 
          :class="{active: nowShow === 'Setting'}"
          class="item"
          @click="changeComponent('Setting')">
          <div class="item__icon">
            <i class="fas fa-cog"></i>
          </div>
          <div class="item__text">SETTING</div>
        </div>
      </div>
      <div class="tomato__right__component">
        <ToDoList 
          v-if="nowShow === 'ToDoList'"
          v-on:set-now-playing="setNowMissing"/>
        <Analyics
          v-if="nowShow === 'Analyics'"/>
        <Setting
          v-if="nowShow === 'Setting'"/>
      </div>
    </div>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList'
import Analyics from './components/Analyics'
import Setting from './components/Setting'

export default {
  name: 'App',
  components: {
    ToDoList,
    Analyics,
    Setting
  },
  data() {
    return {
      second: 1500,
      isClockDone: false,
      nowMissing: '',
      nowShow: 'ToDoList',
      isCountDown: false
    }
  },
  computed:{
    source() {
      return this.nowAudio.src
    },
    nowMin() {
      let min = Math.floor(Math.floor(this.second % 3600) / 60)
      let splitMin = min.toString().split("")
      if(splitMin.length <= 1) {
        splitMin.unshift('0')
      }
      let nowMin = splitMin.toString().replace(',', '')
      return nowMin
    },
    nowSec() {
      let sec = this.second % 60
      let splitSec = sec.toString().split("")
      if(splitSec.length <= 1) {
        splitSec.unshift('0')
      }
      let nowSec = splitSec.toString().replace(',', '')
      return nowSec
    },
    showNowTime() {
      return `${this.nowMin}：${this.nowSec}`
    }
  },
  methods:{
    changeComponent(component){
      this.nowShow = component
    },
    timmer() {
      let clock = window.setInterval(() => {
        if(this.isCountDown) {
          this.second--
          if (this.second < 0) {
            this.isCountDown = false
            this.second = 1500
            this.isCountDown = false
            const audio = this.$refs.audioPlayer
            audio.pause()
            audio.currentTime = 0
            audio.play()
          }
        } else {
          window.clearInterval(clock)
          this.isCountDown = false
          this.second = 1500
        }
      },1000)
    },
    playClick() {
      this.isCountDown = !this.isCountDown
      this.timmer()
    },
    setNowMissing(missing) {
      this.nowMissing = missing
    }
  }
}
</script>
<style lang="sass" scoped>
@font-face
  font-family: TaipeiSansTCBeta-Bold
  src: url('/src/fonts/TaipeiSansTCBeta-Bold.ttf')

@font-face
  font-family: TaipeiSansTCBeta-Light
  src: url('/src/fonts/TaipeiSansTCBeta-Light.ttf')

@font-face
  font-family: TaipeiSansTCBeta-Regular
  src: url('/src/fonts/TaipeiSansTCBeta-Regular.ttf')

$white: #FFFFFF;
$black: #000000;
$red: #BA000D;
$tomatoRed: #F44336;
$gray: #707070;
$darkGray: #6A6868;

.tomato
  font-family: TaipeiSansTCBeta-Regular
  display: flex
  width: 100%
  height: 100vh

  &__left
    width: 45%
    background-color: $black
    color: $white
    display: flex
    align-items: center
    justify-content: center
    flex-direction: column
    
    &__clock
      position: relative

      &__button
        width: 193px
        height: 193px
        background-color: $tomatoRed
        border-radius: 50%
        margin: 0 auto
        position: absolute
        top: 16px
        left: 50%
        transform: translateX(-50%)
        display: flex
        align-items: center
        justify-content: center
        font-size: 60px
        cursor: pointer

      &__circle
        width: 215px
        height: 215px
        border: 5px solid $red
        border-radius: 50%
        margin: 0 auto

      &__leaf
        position: absolute
        top: -35%
        left: -35%

    &__info
      margin-top: 40px

      &__time
        width: 100%
        h2
          margin: 0
          font-size: 90px
          font-family: TaipeiSansTCBeta-Bold
          font-weight: bold
          line-height: 108px

      &__line
        width: 140px
        height: 6px
        border: none
        background-color: $white
        margin: 18px 0

      &__title
        font-size: 22px
        font-family: TaipeiSansTCBeta-Bold
        font-weight: bold
  &__right 
    width: 55%
    color: $black
    padding-top: 120px

    &__menu
      display: flex
      justify-content: space-between
      max-width: 525px
      width: 100%
      margin: 0 auto
      margin-bottom: 40px
      
      .item
        display: flex
        align-items: center
        cursor: pointer
        
        &__icon
          font-size: 24px

        &__text
          font-size: 20px
          font-family: TaipeiSansTCBeta-Bold
          font-weight: bold
          margin-left: 12px

      .active
        color: $tomatoRed
        cursor: default
        pointer-events: none
        border-bottom: 3px solid
</style>