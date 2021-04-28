<template>
  <div class="container">
    <div>
      <h1 class="title">
        You are: {{ trueSelf.name }}
      </h1>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Index',
  props: {
    trueSelf: Object,
  },
  data(){
    return {
    }
  }
};
</script>