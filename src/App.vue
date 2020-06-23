<template>
  <div>
    <sampleHeader></sampleHeader>
    <sampleHeader></sampleHeader>
    <sampleHeader></sampleHeader>
    <sampleHeader></sampleHeader>

    <p v-if="msg.length > 0">{{ msg }}</p>
    <p v-else>no text</p>
    <input type="text" v-model="msg" />
    <button v-on:click="clear()">clear</button>
  </div>
</template>

<script>
import sampleHeader from "./components/SampleHeader";

export default {
  components: {
    sampleHeader
  },
  data() {
    return {
      msg: "hello world."
    };
  },
  methods: {
    clear() {
      this.msg = "";
    }
  },
  created() {
    fetch(
      "http://www.geonames.org/postalCodeLookupJSON?postalcode=10504&country=US"
    )
      .then(response => this.response = response.json())
      .then(json => this.msg = json.postalcodes[0].adminName1);
  }
};
</script>
