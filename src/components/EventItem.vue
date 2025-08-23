<template>
  <div class="event" :class="{ show: isOpen }">
    <p>{{ text }}</p>
    <button @click="isOpen=!isOpen">X</button>
  </div>
</template>

<script>
export default {
  name: "EventComponent",
  props: {
    text: String,
  },
  data() {
    return {
      isOpen: true
    }
  }
}
</script>

<style>
.event {
  background: #444;
  color: #fff;
  padding: 10px 20px;
  text-align: center;
  font-size: small;
  display: none;
  align-items: center;
  justify-content: space-between;
}

.event.show {
  display: flex;
}
.event p {
  margin: 0;
}
</style>