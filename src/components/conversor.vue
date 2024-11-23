<template>
  <div class="conversor-container">
    <h1>Conversor de Monedas</h1>
    <div class="form-container">
      <label for="amount">Cantidad:</label>
      <input
        id="amount"
        type="number"
        v-model="amount"
        placeholder="Ingresa la cantidad"
      />

      <label for="currency">Moneda de origen:</label>
      <select id="currency" v-model="selectedCurrency">
        <option v-for="(name, key) in currencies" :key="key" :value="key">
          {{ name }}
        </option>
      </select>
    </div>

    <div class="results-container" v-if="amount > 0">
      <h2>Conversiones:</h2>
      <ul>
        <li v-for="key in filteredCurrencies" :key="key">
          {{ currencies[key] }}: {{ convertCurrency(key) }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "ConversorDeMonedas",
  data() {
    return {
      amount: 0,
      selectedCurrency: "MXN",
      exchangeRates: {
        MXN: 1, // Peso mexicano
        USD: 0.057, // Dólar
        EUR: 0.052, // Euro
        JPY: 8.33, // Yen
        CNY: 0.41, // Yuan
      },
      currencies: {
        MXN: "Peso Mexicano",
        USD: "Dólar Estadounidense",
        EUR: "Euro",
        JPY: "Yen Japonés",
        CNY: "Yuan Chino",
      },
    };
  },
  computed: {
    filteredCurrencies() {
      // Devuelve solo las monedas diferentes a la seleccionada
      return Object.keys(this.currencies).filter(
        (key) => key !== this.selectedCurrency
      );
    },
  },
  methods: {
    convertCurrency(toCurrency) {
      const fromRate = this.exchangeRates[this.selectedCurrency];
      const toRate = this.exchangeRates[toCurrency];
      const convertedAmount = (this.amount / fromRate) * toRate;
      return convertedAmount.toFixed(2);
    },
  },
};
</script>

<style scoped>
/* Fondo del cuerpo con un degradado de colores verdes */
body {
  background: linear-gradient(
    135deg,
    #4caf50,
    #81c784
  ); /* Gradiente verde vibrante */
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0;
  font-family: "Poppins", sans-serif;
}

.conversor-container {
  max-width: 600px; /* Más ancho */
  margin: 0 auto;
  padding: 30px;
  text-align: center;
  background-color: #ffffff; /* Blanco para resaltar */
  border-radius: 20px; /* Bordes más suaves */
  box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.2); /* Sombra más profunda */
}

/* Estilo para el encabezado */
h1 {
  color: #4caf50; /* Verde vibrante */
  font-size: 32px;
  margin-bottom: 20px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
}

/* Contenedor del formulario */
.form-container {
  margin-bottom: 30px;
}

/* Etiquetas */
label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
  color: #333;
}

/* Inputs y select con estilo */
input,
select {
  width: calc(100% - 20px); /* Centrado exacto */
  padding: 12px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  background-color: #e8f5e9; /* Verde pastel */
  box-shadow: inset 0px 2px 4px rgba(0, 0, 0, 0.1);
  margin: 0 auto 15px;
  display: block; /* Centrado automático */
}

input:focus,
select:focus {
  outline: none;
  border: 2px solid #388e3c; /* Verde más intenso */
  background-color: #ffffff;
}

/* Contenedor de resultados */
.results-container {
  text-align: left;
  background-color: #f1f8e9; /* Verde pastel */
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.1);
}

.results-container h2 {
  color: #4caf50; /* Verde vibrante */
  margin-bottom: 15px;
  font-size: 22px;
}

/* Lista de conversiones */
ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px 0;
  font-size: 18px;
  color: #555;
  border-bottom: 1px solid #dcedc8; /* Verde claro */
  padding-bottom: 5px;
}

li:last-child {
  border-bottom: none;
}

li span {
  font-weight: bold;
  color: #4caf50; /* Verde consistente */
}

/* Botón con estilo atractivo */
button {
  background-color: #388e3c; /* Verde fuerte */
  color: #ffffff;
  border: none;
  border-radius: 8px;
  padding: 12px 24px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #2e7d32; /* Verde más oscuro */
}

button:active {
  background-color: #1b5e20; /* Verde intenso */
}

footer {
  margin-top: 20px;
  font-size: 14px;
  color: #fafafa;
  text-align: center;
}
</style>
