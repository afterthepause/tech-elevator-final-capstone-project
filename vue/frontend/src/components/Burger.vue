<template>
  <div id="burger" :class="{ 'active' : isBurgerActive }" @click.prevent="toggle">
    <slot>
      <button type="button" class="burger-button" title="Menu">
        <span class="hidden">Toggle menu</span>
        <span class="burger-bar burger-bar--1"></span>
        <span class="burger-bar burger-bar--2"></span>
        <span class="burger-bar burger-bar--3"></span>
      </button>
    </slot>
  </div>
</template>
<script>
import { store, mutations } from "@/store.js";

export default {
  computed: {
    isBurgerActive() {
      return store.isNavOpen;
    }
  },
  methods: {
    toggle() {
      mutations.toggleNav();
    }
  }
};
</script>

<style>
.hidden {
  visibility: hidden;
  z-index: 999;
}

button {
  cursor: pointer;
  z-index: 999;
}

/* remove blue outline */
button:focus {
  outline: 0;
  z-index: 999;
}

.burger-button {
  position: relative;
  height: 30px;
  width: 32px;
  display: block;
  z-index: 999;
  border: 0;
  border-radius: 0;
  background-color: transparent;
  pointer-events: all;
  transition: transform 0.6s cubic-bezier(0.165, 0.84, 0.44, 1);
  z-index: 999;
}

.burger-bar {
  background-color: #130f40;
  position: absolute;
  top: 95%;
  z-index: 999;
  right: 5px;
  left: 8px;
  height: 3px;
  width: auto;
  margin-top: -1px;
  transition: transform 0.6s cubic-bezier(0.165, 0.84, 0.44, 1),
    opacity 0.3s cubic-bezier(0.165, 0.84, 0.44, 1),
    background-color 0.6s cubic-bezier(0.165, 0.84, 0.44, 1);
}

.burger-bar--1 {
  -webkit-transform: translateY(-6px);
  transform: translateY(-6px);
}

.burger-bar--2 {
  transform-origin: 100% 30%;
  transform: scaleX(0.6);
}

.burger-button:hover .burger-bar--2 {
  transform: scaleX(1);
}

.no-touchevents .burger-bar--2:hover {
  transform: scaleX(1);
}

.burger-bar--3 {
  transform: translateY(6px);
}

#burger.active .burger-button {
  transform: rotate(0deg);
  z-index: 999;
}

#burger.active .burger-bar {
  background-color: #fff;
  z-index: 999;
}

#burger.active .burger-bar--1 {
  transform: rotate(45deg);
  z-index: 999;
}

#burger.active .burger-bar--2 {
  opacity: 0;
  z-index: 999;
}

#burger.active .burger-bar--3 {
  transform: rotate(-45deg);
  z-index: 999;
}
</style>