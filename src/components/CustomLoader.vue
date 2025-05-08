<script setup lang="ts"></script>

<template>
  <div class="lds-container">
    <div class="lds-dual-ring" />
  </div>
</template>

<style scoped>
.lds-container {
  height: 80px;
  width: 80px;
}

.lds-dual-ring {
  display: inline-block;
  width: 100%;
  height: 100%;
  padding: 8px;
}

.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 80%;
  height: 80%;

  border-radius: 50%;
  border: 6px solid #fff;
  border-color: #fff transparent #fff transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}

@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
