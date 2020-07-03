<template>
  <div class="barcode">
    <input
      class="barcode__input"
      :class="error && 'barcode__input--error'"
      v-model="code"
      v-mask="mask"
    >
    <div class="barcode__svg" v-if="barcodeSVG" v-html="barcodeSVG"></div>
    <div v-if="error" class="barcode__message">{{ error }}</div>
  </div>
</template>

<script>
import Boleto from "boleto.js";
import { mask } from "vue-the-mask";

const MAX_CODE_LENGTH = 54;

export default {
  name: "BarcodeGen",
  directives: { mask },
  data: () => ({
    code: "",
    barcodeSVG: null,
    error: null,
    mask: "#####.##### #####.###### #####.###### # ##############"
  }),

  watch: {
    code() {
      try {
        if (this.code.length === MAX_CODE_LENGTH) {
          this.barcodeSVG = new Boleto(this.code).toSVG();
        } else {
          this.barcodeSVG = null;
        }
        this.error = null;
      } catch (err) {
        this.barcodeSVG = null;
        this.error = "Invalid Code!";
      }
    }
  }
};
</script>

<style scoped>
.barcode {
  width: 50vw;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

.barcode__input {
  height: 32px;
  border-radius: var(--border-radius);
  border: 1px solid #ddd;
  padding: 0px 10px;
  transition: all 0.25s ease;
  width: calc(100% - 20px);
}

.barcode__input.barcode__input--error {
  border: 1px solid #fff;
  box-shadow: var(--danger-color) 0px 0px 3.33px !important;
}

.barcode__input:hover {
  border: 1px solid #aaa;
}

.barcode__input:focus {
  border: 1px solid #fff;
  box-shadow: var(--main-color) 0px 0px 3.33px;
  outline: none;
}

.barcode__message {
  color: var(--danger-color);
  font-weight: bold;
}

.barcode__svg {
  margin-top: 1rem;
  width: 100%;
}
</style>
