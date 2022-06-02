<template>
  <div>
   <input type="text" @input="handleInput">
  </div>
</template>
<script>
export default {
  data() {
    return {};
  },
  methods: {
    handleInput(event) {
      this.$emit('onInputChange', event.target.value);
    },
  },
};
</script>
