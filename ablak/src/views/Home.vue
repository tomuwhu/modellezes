<template>
  <div class="home">
    <h1>Mozgás</h1>
    <button v-if="!started" @click="start()">Start</button>
    <button v-if="started" @click="stop()">Stop</button>
    <button @click="gravity=!gravity">Gravity</button>
    <input type="range" v-model="av">
    <svg viewBox="0 0 1000 700">
      <circle :cx="k1xp" :cy="k1yp" r="20"/>
    </svg>
    {{k1vx}}
  </div>
</template>

<script>
var interval
export default {
  name: 'home',
  data: () => ({
    k1xp: 250,
    k1yp: 110,
    k1vx: 3,
    k1vy: 3,
    started: false,
    gravity: false,
    av: 0
  }),
  methods: {
    start() {
      this.started=true
      interval=setInterval(() => {
        this.k1xp+=this.k1vx
        this.k1yp+=this.k1vy
        if (this.k1xp>980) this.k1vx = -this.k1vx
        if (this.k1xp<20) this.k1vx = -this.k1vx
        if (this.k1yp>680) this.k1vy = -this.k1vy
        if (this.k1yp<20) this.k1vy = -this.k1vy
        if (this.gravity) this.k1vy+=0.05
        this.k1vx=this.k1vx*(1-this.av/10000)
        this.k1vy=this.k1vy*(1-this.av/10000)
      },30)
    },
    stop() {
      this.started=false
      clearInterval(interval)
    }
  }
}
</script>
