<template>
  <ConversorDeMonedas />
</template>

<script>
import ConversorDeMonedas from "./components/conversor.vue";

export default {
  name: "App",
  components: {
    ConversorDeMonedas,
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: "Poppins", sans-serif;
}

#app {
  min-height: 100vh; /* Asegura que ocupe toda la pantalla */
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(
    135deg,
    #1b5e20,
    /* Verde fuerte */ #4caf50,
    /* Verde normal */ #1b5e20 /* Verde fuerte */
  );
}
</style>
