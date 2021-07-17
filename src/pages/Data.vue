<template>
  <div>
    <p>We're connected to the server!</p>
    <p>Message from server: "{{ 'socketMessage' }}"</p>
    <button @click="pingServer()">Ping Server</button>
  </div>
</template>

<script>
// import LineChart from "../LineChart.js";
import io from 'socket.io-client';
let socket = io.connect('http://localhost:2000');

export default {
  created() {
    socket.on('binFull', (data) => {
      console.log(data, 'receiving notifications');
    });
  },
  data() {
    return {
      isConnected: false,
      socketMessage: '',
    };
  },

  methods: {
    pingServer() {
      // Send the "pingServer" event to the server.
    },
  },
};
</script>
