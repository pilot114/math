<template>
    <line-chart
        width="100%"
        height="300px"
        :data="data"
        label="y"
        :min="-2"
        :max="2"
    />
<!--    xtitle="x"-->
<!--    ytitle="y"-->
<!--    :colors="['#b00', '#666']"-->
<!--    :discrete="true"-->
<!--    :legend="true"-->
</template>

<script>
export default {
  name: 'Plane',
  props: {
    data: Object
  }
}
</script>

<style scoped>
</style>
