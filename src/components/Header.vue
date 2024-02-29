<template>
  <header>
    <h1>To Do List</h1>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
header {
  width: 100%;
  height: 90px;
  background-color: #de3f53;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10px 10px 0 0;
}

header h1 {
  color: #ffffff;
  text-transform: uppercase;
  font-size: 50px;
}
</style>
