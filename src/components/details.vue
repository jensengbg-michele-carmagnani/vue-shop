<template>
  <ul>
      <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
    </ul>
</template>

<script>
export default {
  name: 'productDetail',
  props:{
    details:{
      type: Array,
      require: true
    }
}
}

</script>

<style>

</style>