<template>
<div>
  <div>
  {{time.status}}
    <Clock
      :secs="time.work.seconds"
      :mins="time.work.minutes"
      :hrs="time.work.hours"
      :styled="true"
      :status="time.status"
     />
    <StartStop
      v-on:start="time.startWork()"
      v-on:stop="time.takeBreak()"
      v-on:pause="time.pauseClock()"
      v-bind:status="time.status"
    />
  </div>
  <div class="tasks">
    <Tasks v-bind:tasks="time.tasks"/>
  </div>
</div>

</template>

<script>
import Clock from './Clock.vue'
import StartStop from './StartStop.vue'
import Tasks from './Tasks.vue'

class TimeTrack {
  allSeconds = 0
  get hours () { return ~~(this.allSeconds / (3600)) }
  get minutes () { return ~~((this.allSeconds % 3600) / 60) }
  get seconds () { return ~~(this.allSeconds % 3600 % 60) }
}

class Task extends TimeTrack {
  constructor (name, locked) {
    super()
    this.name = name
    this.locked = locked || false
  }
}

const time = {
  work: new TimeTrack(),
  break: new TimeTrack(),
  tasks: [new Task('Other', true), new Task('Otasdasdher', true)],
  currentTask: 0,
  status: 'pause',
  interval: null,
  startInterval: function () {
    this.interval = this.interval || setInterval(() => {
      if (this.status === 'work') {
        this.work.allSeconds++
        this.tasks[this.currentTask].allSeconds++
      } else if (this.status === 'break') {
        this.break.allSeconds++
      } else {

      }
    }, 1000)
  },
  startWork () {
    this.status = 'work'
  },
  takeBreak () {
    this.status = 'break'
  },
  pauseClock () {
    this.status = 'pause'
  }
}

export default {
  name: 'MainView',
  data: function () {
    return {
      time: time
    }
  },
  components: {
    Clock,
    StartStop,
    Tasks
  },
  created: function () {
    time.startInterval()
  }
}

</script>

<style lang="scss">

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
.tasks{
  max-width: 300px;
}
</style>
