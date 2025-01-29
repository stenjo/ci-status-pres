<template>
  <div class="black-layout">
    <slot />
  </div>
</template>

<style scoped>
.black-layout {
  background: black;
  color: white;
  padding: 2rem;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
