<template>
  <div>
    <h1>
      {{log}}
    </h1>
    <p>
      Capture:
      <select v-model="selected">
        <option v-for="option in options" :key="option.text" :value="option">
          {{ option.text }}
        </option>
      </select>
    </p>

    <hr />

    <p class="decode-result">
      Last result: <b>{{ result }}</b>
    </p>

    <div v-if="selected.id === 0 || selected.id === 1" style="height: 40vh; width:  40vh;">
      <qrcode-stream   :facingMode="selected.value" @decode="onDecode" @init="onInit" />
    </div>
    <qrcode-capture v-if="selected.id === 2" @detect="onDetect" @decode="onDecode"/>
  </div>
</template>

<script>
import { QrcodeStream, QrcodeCapture } from 'vue-qrcode-reader'

export default {
  components: { QrcodeCapture , QrcodeStream},

  data() {
    const options = [
      { id: 0, text: 'Default camera', value: 'environment' },
      { id: 1, text: 'Front camera', value: 'user' },
      { id: 2, text: 'Choose file', value: false }
    ]

    return {
      log: 'START',
      result: '',
      options,
      selected: options[0]
    }
  },

  methods: {
    onInit(promiseInit) {
      // eslint-disable-next-line no-console
      promiseInit
      .then( data => {
        // eslint-disable-next-line no-console
        console.log('SUCCESS INIT ', data);
        this.log = 'SUCCESS INIT '+ data;
      })
      .catch(err => {
        // eslint-disable-next-line no-console
        console.log('ERROR INIT ', err);
        this.log = 'ERROR INIT ' + err;
      })
    },
    onDecode(url) {
      this.result = url;
    },
  }
}
</script>