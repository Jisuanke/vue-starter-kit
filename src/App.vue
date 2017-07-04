<template>
<div>
  <div>
    <input type="text" v-model.number="celsius" :class="tempClasses">℃<br>
    <button @click="increment()">+</button><button @click="decrement()">-</button><br>
    <input type="text" :value="fahrenheit" :class="tempClasses" readonly>℉<br>
    <button @click="log()">记录</button>
  </div>
  <div class="hint" v-if="danger">温度过高</div>
  <ol>
    <li v-for="log in logs" :class="isDanger(log) ? 'danger' : ''">{{ isDanger(log) ? `过热${log}` : log }}℃</li>
  </ol>
</div>
</template>

<script>
const THRESHOLD = 5

export default {
  data() {
    return {
      celsius: 0,
      logs: []
    }
  },
  computed: {
    danger() {
      return this.celsius > THRESHOLD
    },
    tempClasses() {
      return this.danger ? ['danger'] : []
    },
    fahrenheit() {
      return this.celsius * 9 / 5 + 32
    }
  },
  methods: {
    increment() {
      this.celsius++
    },
    decrement() {
      this.celsius--
    },
    log() {
      this.logs.push(this.celsius)
    },
    isDanger(temp) {
      return temp > THRESHOLD
    }
  }
}
</script>

<style scoped>
div {
  text-align: center;
  font-size: 60px;
}

input {
  font-size: 60px;
}

button {
  font-size: 30px;
}

ol {
  width: 500px;
  margin: 0 auto;
}

.danger {
  background-color: red;
}

.hint {
  color: red;
}
</style>
