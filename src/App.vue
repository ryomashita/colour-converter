<template>
  <div>
    <div>
      <label for="red-input">R:</label>
      <input type="number" id="red-input" v-model="rgb.red" @input="updateYCbCr" />
    </div>
    <div>
      <label for="green-input">G:</label>
      <input type="number" id="green-input" v-model="rgb.green" @input="updateYCbCr" />
    </div>
    <div>
      <label for="blue-input">B:</label>
      <input type="number" id="blue-input" v-model="rgb.blue" @input="updateYCbCr" />
    </div>
    <div>
      <label for="y-input">Y:</label>
      <input type="number" id="y-input" v-model="ycbcr.y" @input="updateRGB" />
    </div>
    <div>
      <label for="cb-input">Cb:</label>
      <input type="number" id="cb-input" v-model="ycbcr.cb" @input="updateRGB" />
    </div>
    <div>
      <label for="cr-input">Cr:</label>
      <input type="number" id="cr-input" v-model="ycbcr.cr" @input="updateRGB" />
    </div>
    <div :style="{ backgroundColor: rgbColor, width: '100px', height: '100px' }"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rgb: { red: 0, green: 0, blue: 0 },
      ycbcr: { y: 16, cb: 128, cr: 128 },
      rgbColor: "rgb(0, 0, 0)",
    };
  },
  methods: {
    updateColor() {
      this.color = `rgb(${this.redValue}, ${this.greenValue}, ${this.blueValue})`;
    },
    updateYCbCr() {
      const { red, green, blue } = this.rgb;
      const y = 0.183 * red + 0.614 * green + 0.062 * blue + 16;
      const cb = -0.101 * red - 0.339 * green + 0.439 * blue + 128;
      const cr = 0.439 * red - 0.399 * green - 0.040 * blue + 128;
      this.ycbcr = { y, cb, cr };
      this.rgbColor = `rgb(${red}, ${green}, ${blue})`;
    },
    updateRGB() {
      const { y, cb, cr } = this.ycbcr;
      const red = 1.164 * (y - 16) + 1.793 * (cr - 128);
      const green = 1.164 * (y - 16) - 0.213 * (cb - 128) - 0.533 * (cr - 128);
      const blue = 1.164 * (y - 16) + 2.112 * (cb - 128);
      this.rgb = { red, green, blue };
      this.rgbColor = `rgb(${red}, ${green}, ${blue})`;
    },
  },
};
</script>