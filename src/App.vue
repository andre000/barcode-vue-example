<template>
  <div id="app">
    <h1>Barcode Generator</h1>
    <barcode-gen/>
  </div>
</template>

<script>
import BarcodeGen from "./components/BarcodeGen";
export default {
  name: "App",
  components: {
    BarcodeGen
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Barlow:ital,wght@0,400;1,800&display=swap");

:root {
  --main-color: #64b9ff;
  --danger-color: #ff6464;
  --border-radius: 4px;
}

body {
  margin: 0px;
  background-color: var(--main-color);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: "Barlow";
}

#app {
  padding: 1rem 2rem 2rem 2rem;
  border-radius: var(--border-radius);
  background: #fff;
}

h1 {
  font-family: "Barlow", sans-serif;
  font-style: italic;
  color: #333;
}
</style>
