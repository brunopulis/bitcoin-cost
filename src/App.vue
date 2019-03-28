<template>
  <div id="app">
    <Bitcoin/>
  </div>
</template>

<script>
import Bitcoin from "./components/Bitcoin";

export default {
  name: "app",
  components: {
    Bitcoin
  }
};
</script>

<style>
body {
  background: #7e8d85;
}
#app {
  align-items: center;
  display: flex;
  font-family: "Open Sans";
  justify-content: center;
  line-height: 1.4;
  margin-top: 60px;
  text-align: center;
}
</style>
