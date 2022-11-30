<template>
  <div>
    <h3>The easiest way to create QR Code</h3>
    <h5>Generate a QR code and download it!</h5>
    <div class="urlInput">
      <input type="text" v-model="qr.url_input" size="35" @input="urlChanged" />
      &nbsp;
      <input type="text" readonly v-model="color" size="5" />
      <button
        :style="{ background: color }"
        @click="showcolorpicker = showcolorpicker ? false : true"
      >
        &nbsp;
      </button>

      <div v-show="showcolorpicker" style="position: absolute">
        <ColorPicker
          theme="light"
          :color="color"
          :sucker-hide="false"
          :sucker-canvas="suckerCanvas"
          :sucker-area="suckerArea"
          @changeColor="changeColor"
          @openSucker="openSucker"
        />
      </div>
    </div>

    <!--
https://developer.mozilla.org/en-US/docs/Web/CSS/minmax
https://css-tricks.com/snippets/css/complete-guide-grid/

      -->
    -->
    <div class="genOut">
      <div v-if="qr.output" class="text-center">
        <div v-html="qr.output" class="viewer mx-auto"></div>
      </div>
    </div>
  </div>
</template>

<script>
import { toString } from 'qrcode';
import { saveAs } from 'file-saver';
import { reactive, ref, watch } from 'vue';
import { ColorPicker } from 'vue-color-kit';
import 'vue-color-kit/dist/vue-color-kit.css';

export default {
  name: 'Colorpicker',
  components: {
    ColorPicker,
  },
  setup() {
    let color = ref('#000000');
    let suckerHide = ref(false);
    let suckerCanvas = null;
    let suckerArea = ref([]);
    let showcolorpicker = ref(false);
    const qr = reactive({
      url: '',
      svg_output: '',
      url_input: '',
      url_input_timeout: null,
      color_timeout: null,
    });
    function changeColor(_color) {
      //const { r, g, b, a } = _color.rgba;
      //color.value = `rgba(${r}, ${g}, ${b}, ${a})`;
      color.value = _color.hex;
    }
    function openSucker(isOpen) {
      if (isOpen) {
        // ... canvas be created
        // this.suckerCanvas = canvas
        // this.suckerArea = [x1, y1, x2, y2]
      } else {
        // this.suckerCanvas && this.suckerCanvas.remove
      }
    }
    /* *************  */
    const generateQr = () => {
      qr.url = qr.url.trim(); // trim spaces

      if (!qr.url) {
        qr.output = null;
        return;
      }
      toString(
        qr.url,
        { color: { dark: color.value, light: '#0000' } },
        (err, string) => {
          if (err) throw err;
          qr.output = string;
        }
      );
    };
    function urlChanged() {
      if (qr.url_input_timeout) {
        clearTimeout(qr.url_input_timeout);
      }
      qr.url_input_timeout = setTimeout(() => {
        qr.url = qr.url_input;
        console.log('urlC');
        generateQr();
      }, 800);
    }
    return {
      qr,
      color,
      suckerHide,
      suckerCanvas,
      suckerArea,
      changeColor,
      showcolorpicker,
      openSucker,
      urlChanged,
    };
  },
};
</script>

<style scoped>
input {
  border-radius: 10px;
  border: 1px solid gray;
  height: 2.5em;
}
input.:focus {
  border: 2px solid #73ad21;
}
button {
  width: 2.5em;
  height: 2.5em;
  border-radius: 50%;
}
.text-center {
  text-align: center;
}
.items-center {
  align-items: center;
}
</style>
