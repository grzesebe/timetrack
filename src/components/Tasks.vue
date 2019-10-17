<template>
    <ul>
        <li v-for="(task, id) in tasks" v-bind:key="id">
          <div class="name">
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
          </div>
          <Clock class="miniclock"
            v-bind:secs="task.seconds"
            v-bind:mins="task.minutes"
            v-bind:hrs="task.hours"
            delimiter=":"
          />
          <div class="setTask">
            <input type="radio" name="currentTask" :value="id" :id="id"
            :checked="currentTask == id ? 'checked' : null"
             v-on:input="$emit('input', id)"
             >
          </div>
        </li>
    </ul>
</template>

<script>
import Clock from './Clock.vue'

export default {
  name: 'Tasks',
  props: {
    tasks: Array,
    value: Number,
    status: String
  },
  components: {
    Clock
  },
  data: function () {
    return {
      currentlyEditing: null,
      currentTask: this.value
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
@import './../colors.scss';
  .miniclock > div{
    display: inline;
  }
  li{
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid $color-text;
    margin-bottom: 1em;
    div.name{
      text-align: left;
      flex-grow: 1;
    }
  }
</style>>
