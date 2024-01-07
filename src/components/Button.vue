<template>
  <!-- the vbind style in vue -->
  <button @click="onClick()" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
  },
//declare a method
  methods: {
    onClick() {
      this.$emit("btn-click");
    },
  },
};
</script>
