<template>
  <div class="container">
    <div class="row justify-content-center">
      <div v-show="!isWorking" class="col-sm-12 col-md-6 col-lg-4">
        <div class="jumbotron text-center">
          <div class="container">
            <img class="img-fluid rounded" src="../../../assets/pushups.png" alt="">
            <h2>Push-ups</h2>
            <p class="lead">
              Description: lorem ipsum
            </p>
          </div>
        </div>
      </div>
      <div class="col-sm-12 col-md-6 col-lg-8">
        <count-down-timer @finished="togglePomodoro" :time="time"></count-down-timer>
      </div>
    </div>
  </div>
</template>
<script>
  import CountDownTimer from './timer/CountDownTimer'
  import config from '../../../config'

  export default {
    data () {
      return {
        isWorking: true,
        isShortBreak: false,
        isLongBreak: false,
        pomodoros: 0
      }
    },
    computed: {
      time () {
        let minutes
        if (this.isWorking) {
          minutes = config.workingPomodoro
        } else if (this.isShortBreak) {
          minutes = config.shortBreak
        } else if (this.isLongBreak) {
          minutes = config.longBreak
        }

        return minutes * 60
      }
    },
    components: {
      CountDownTimer
    },
    methods: {
      togglePomodoro () {
        this.isWorking = !this.isWorking
        this.isShortBreak = this.isLongBreak = false
        if (this.isWorking) {
          return
        }
        this.pomodoros ++
        this.isLongBreak = this.pomodoros % config.pomodorosTillLongBreak === 0
        this.isShortBreak = !this.isLongBreak
      }
    }
  }
</script>
<style scoped lang="scss">

</style>
