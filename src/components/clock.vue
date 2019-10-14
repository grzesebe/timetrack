<template>
  <div>
    <div>
        <span>{{ hrs }}</span>
        <span>hours</span>
    </div>
    <div>
        <span>{{ mins }}</span>
        <span>minutes</span>
    </div>
    <div>
        <span>{{ secs }}</span>
        <span>second</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Clock',
  props: {
    hrs: null,
    mins: null,
    secs: null
  }
}
</script>

<style>

</style>
