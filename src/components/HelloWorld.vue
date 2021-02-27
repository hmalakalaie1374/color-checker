<template>
  <div class="flex flex-col lg:flex-row lg:justify-between">
    <div class="mb-4 order-1 sm:order-1 px-6">
      <h2 class="mb-8 font-bold text-4xl">Foreground</h2>
      <input
        type="text"
        v-model="forgroundColor"
        v-on:input="runChecker && (forgroundColor = $event.target.value)"
        placeholder="#000000"
        class="mt-1 block w-full rounded-md bg-transparent border-grey-300 focus:border-gray-500 focus:bg-white focus:ring-0 text-center"
      />
    </div>
    <div class="mb-4 order-3 sm:order-2">
      <h4>Preview area</h4>
      <div class="previewColors mt-6">
        <div
          class="backBg w-10 h-10 mx-auto"
          :style="{ 'background-color': '#' + forgroundColor }"
        ></div>
        <div
          class="forBg w-40 h-40"
          :style="{ 'background-color': '#' + backgroundColor }"
        ></div>
      </div>
    </div>
    <div class="mb-4 order-2 sm:order-3 px-6">
      <h2 class="mb-8 font-bold text-4xl">Background</h2>
      <input
        type="text"
        v-model="backgroundColor"
        v-on:input="runChecker"
        placeholder="#000000"
        class="mt-1 block w-full rounded-md bg-transparent border-grey-300 focus:border-gray-500 focus:bg-white focus:ring-0 text-center"
      />
    </div>
  </div>
  <div class="flex flex-col lg:flex-row mt-8 md:mt-16">
    <div class="flex-1 order-2 sm:order-1">
      <h4 class="text-2xl font-bold">Large text</h4>
      AA:{{ AALargeResult }} / AAA:{{ AAALargeResult }}
    </div>
    <div
      class="flex-1 order-1 sm:order-2 p-4 md:p-8 bg-red-200 rounded-lg shadow-inner"
    >
      <h4 class="text-2xl font-bold mb-3">Contrast Ratio</h4>
      <h4 class="text-2xl font-bold">{{ contrastRatio }}:1</h4>
    </div>
    <div class="flex-1 order-3 sm:order-3">
      <h4 class="text-2xl font-bold">Normal text</h4>
      AA:{{ AASmallResult }} / AAA:{{ AAASmallResult }}
    </div>
  </div>
</template>

<script>
import tinycolor from "tinycolor2";
export default {
  name: "HelloWorld",
  props: {},
  data() {
    return {
      forgroundColor: "000",
      backgroundColor: "000",
      AASmallResult: "null",
      AAASmallResult: "null",
      AALargeResult: "null",
      AAALargeResult: "null",
      contrastRatio: "null",
    };
  },
  methods: {
    checkAASmall: function () {
      if (
        tinycolor.isReadable(this.forgroundColor, this.backgroundColor, {
          level: "AA",
          size: "small",
        })
      ) {
        this.AASmallResult = "true";
      } else {
        this.AASmallResult = "false";
      }
    },
    checkAALarge: function () {
      if (
        tinycolor.isReadable(this.forgroundColor, this.backgroundColor, {
          level: "AA",
          size: "large",
        })
      ) {
        this.AALargeResult = "true";
      } else {
        this.AALargeResult = "false";
      }
    },
    checkAAASmall: function () {
      if (
        tinycolor.isReadable(this.forgroundColor, this.backgroundColor, {
          level: "AAA",
          size: "small",
        })
      ) {
        this.AAASmallResult = "true";
      } else {
        this.AAASmallResult = "false";
      }
    },
    checkAAALarge: function () {
      if (
        tinycolor.isReadable(this.forgroundColor, this.backgroundColor, {
          level: "AAA",
          size: "large",
        })
      ) {
        this.AAALargeResult = "true";
      } else {
        this.AAALargeResult = "false";
      }
    },
    contrastCaluculate: function () {
      this.contrastRatio = tinycolor.readability(
        this.forgroundColor,
        this.backgroundColor
      );
    },
    runChecker: function () {
      this.checkAASmall();
      this.checkAALarge();
      this.checkAAASmall();
      this.checkAAALarge();
      this.contrastCaluculate();
    },
  },
};
</script>

<style scoped></style>
