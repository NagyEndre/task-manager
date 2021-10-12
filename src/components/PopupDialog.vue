<template>
  <transition name="shade">
    <div id="shade" v-if="open">
      <dialog open>
        <slot></slot>
      </dialog>
    </div>
  </transition>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";

@Component
export default class PopupDialog extends Vue {
  @Prop(Boolean) open!: boolean;
}
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
.shade-leave-to,
.shade-enter {
  opacity: 0;
}
.shade-leave-active,
.shade-enter-active {
  transition: opacity 0.2s ease-out;
}
.shade-leave,
.shade-enter-to {
  opacity: 1;
}
</style>
