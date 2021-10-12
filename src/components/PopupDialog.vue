<template>
  <dialog open>
    <slot></slot>
  </dialog>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component
export default class PopupDialog extends Vue {}
</script>

<style scoped>
dialog {
  position: fixed;
  background: white;
  padding: 1rem;
  margin: 0;
  top: 20vh;
  left: 30%;
  width: 40%;
}
</style>
