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
    <div ref="anim" class="anim" v-bind:class="status"></div>
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
    styled: Boolean,
    status: String
  }
}
</script>

<style lang="scss">
  .clock{
    margin: 20px 0;
    border-radius: 50%;
    border: 3px solid black;
    width: 300px;
    height: 300px;
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;
    position: relative;
    .anim{
      position: absolute;
      border-radius: 50%;
      border: 0px solid black;
      height: 100%;
      width: 100%;
      pointer-events: none;
      &.work{
        animation: pulse 1s linear infinite;
      }
    }
    & > div {
      display: flex;
      flex-direction: column;

      .time{
        font-size: 40px;
      }
    }
  }
  @keyframes pulse {
    0%{
      transform: scale(1);
    }
    50%{
      transform: scale(1.1);
      border-width: 5px;
      border-color: transparent;
    }
    75%{
      border-color: transparent;
      transform: scale(1);
    }
    80%{
      border-width: 0px;
      border-color: initial;
    }
  }
</style>
