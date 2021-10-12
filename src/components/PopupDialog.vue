<template>
  <div id="shade">
    <dialog open>
      <slot></slot>
    </dialog>
  </div>
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
  border-radius: 0.5rem;
}
#shade {
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.5);
  height: 100%;
  width: 100%;
  z-index: 999;
}
</style>
