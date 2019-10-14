<template>
  <div v-bind:class="{clock: styled}">
    <div>
        <span class="time">{{ hrs }}</span>
        <span v-if="!delimiter">hours</span>
        <span v-else>{{delimiter}}</span>
    </div>
    <div>
        <span class="time">{{ mins }}</span>
        <span v-if="!delimiter">minutes</span>
        <span v-else>{{delimiter}}</span>
    </div>
    <div>
        <span class="time">{{ secs }}</span>
        <span v-if="!delimiter">second</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Clock',
  props: {
    hrs: Number,
    mins: Number,
    secs: Number,
    delimiter: String,
    styled: Boolean
  }
}
</script>

<style lang="scss">
  .clock{
    border-radius: 50%;
    border: 2px solid black;
    width: 300px;
    height: 300px;
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;

    & > div {
      display: flex;
      flex-direction: column;

      .time{
        font-size: 40px;
      }
    }
  }
</style>
