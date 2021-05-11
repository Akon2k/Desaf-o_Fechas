<template>
  <div>
    <h1>Cuenta regresiva</h1>
    <hr />
    <br />
    <h2>{{ Temporizador }}</h2>
    <br />
    <div class="botones">
      <button @click="setTemporizador(0)">3 s</button>
      <button @click="setTemporizador(1)">1 m</button>
      <button @click="setTemporizador(2)">5 m</button>
      <button @click="setTemporizador(3)">10 m</button>
      <button @click="setTemporizador(4)">30 m</button>
      <!-- <button @click="setTemporizador(5)">60 m</button> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "Timer",
  data() {
    return {
      tiempoBotones: [3, 60, 300, 600, 1800],
      temporizador: new Date("1900-01-01 00:00:00"),
      interval: null,
    };
  },

  methods: {
    setTemporizador(i) {
      const objFecha = new Date("1900-01-01 00:00:00");
      const agregarsegundos = this.tiempoBotones[i];
      objFecha.setSeconds(agregarsegundos);
      this.temporizador = new Date(objFecha);
      if (this.interval) clearInterval(this.interval);
      this.interval = setInterval(() => {
        const segactuales = this.temporizador.getSeconds();
        const minactuales = this.temporizador.getMinutes();
        if (segactuales !== 0 || minactuales !== 0) {
          this.temporizador.setSeconds(segactuales - 1);
          this.temporizador = new Date(this.temporizador);
        }
      }, 1000);
    },
  },

  computed: {
    Temporizador() {
      return `${this.temporizador.getMinutes()}:${this.temporizador.getSeconds()} Min/Seg`;
    },
  },
};
</script>

<style scoped>
button {
  margin: 0 5px;
}
</style>
