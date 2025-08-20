<template>
  <h1>영화정보</h1>
  <div>
    <h3 class="bg-yellow">{{ title }}</h3>
    <p>{{ year }}</p>
    <p>{{ category }}</p>
    <p v-for="food in foods" :key="food">{{ food }}</p>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      foods: ["김밥", "순대", "만두"],
      title: "노량",
      year: 2023,
      category: "액션, 드라마"
    }
  }
}
</script>

<style>
.bg-yellow {
  background-color: #FF8A00;
}
</style>
