<template>
    <ul>
        <li v-for="(task, id) in tasks" v-bind:key="id">
            <span
              v-if="(currentlyEditing != id)"
              key="0"
              v-on:click="edit(id)">{{task.name}}
            </span>
            <input
              ref="input"
              v-else
              key="1"
              v-model.lazy.trim="task.name"
              v-on:change="stopEditing()"
              v-on:focusout="stopEditing()"
            >
            <Clock class="miniclock"
              v-bind:secs="task.seconds"
              v-bind:mins="task.minutes"
              v-bind:hrs="task.hours"
              delimiter=":"
            />
        </li>
    </ul>
</template>

<script>
import Clock from './Clock.vue'

export default {
  name: 'Tasks',
  props: {
    tasks: Array,
    currentTaskId: Number
  },
  components: {
    Clock
  },
  data: function () {
    return {
      currentlyEditing: Number
    }
  },
  methods: {
    edit: function (id) {
      this.currentlyEditing = id
      this.$nextTick(function () {
        this.$refs.input[0].focus()
      })
    },
    stopEditing: function () {
      this.currentlyEditing = null
    },
    cl: function () {
      console.log(123)
    }
  }
}

</script>

<style lang="scss">
  .miniclock > div{
    display: inline;
  }
  li{
    display: flex;
    justify-content: space-between;
  }
</style>>
