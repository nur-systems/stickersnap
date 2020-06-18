<template>
  <div class="container">
    <p>
      This section is intended for <b>nerds</b>. You can change the endpoint that the App sends requests to so that you can have complete control of the service. It also serves as a handy way of testing in-browser!
    </p>

    <p>
      Use the <b>Check Status</b> button to send a GET request to the root. It will display if everything is A-OK (e.g. 200 response).
    </p>

    <ul v-if="this.statusResponse != null">
      <li>
        <b>Response: </b> {{ this.statusResponse }} (Running: {{ this.serviceLive }})
      </li>
      <li>
        <b>Body: </b> {{ this.statusBody }}
      </li>
    </ul>

    <b-field grouped>
      <b-field expanded>
        <b-input expanded v-model="modelSvcUrl">
        </b-input>
        <p class="control expanded">
          <button class="button is-primary" @click="checkStatus">Check Status</button>
        </p>
      </b-field>
    </b-field>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: ['modelSvcUrl'],
  data: function () {
    return {
      statusResponse: null,
      statusBody: "",
      serviceLive: false
    }
  },
  methods: {
    checkStatus: function () {
      axios.get(this.modelSvcUrl).then(
        response => {
          this.statusResponse = response.status;
          this.serviceLive = (this.statusResponse == 200);
          this.statusBody = response.data;
        }
      ).catch(error => {
        this.statusResponse = -1;
        this.serviceLive = false;
        this.statusBody = 'There was a problem performing the request: the service might be unavailable! The error object has been logged into console for your convenience.';
        console.log(error);
      })
    }
  }
} 
</script>
