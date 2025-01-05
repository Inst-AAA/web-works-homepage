<template>
  <v-sheet
    :color="COLORS.TITLE_WHITE"
    style="align-content: center"
    :style="{ backgroundImage: 'url(' + backgroundImage + ')',backgroundSize: 'cover', width: sheetWidth + 'px', height: 750 + 'px' }"
  >
    <div>
      <br>
      <br>
      <h1>
        Works
      </h1>

      <br>
      <p class="institution-text">
        {{ $t('head1') }}
      </p>
      <p class="institution-text">
        {{ $t('head2') }}
      </p>
      <v-img
        src="@/assets/logo-black-500.png"
        width="70"
      >
      </v-img>
      <p style="font-size: 11px">
        <b>
          建筑运算与应用实验室<br>
          Laboratory of Architectural Algorithm and Application
        </b>
      </p>
      <br>
    </div>
  </v-sheet>

</template>

<script>

import {COLORS} from "@/color/colors";
import {publicPath} from "../../vue.config";

export default {
  data() {
    return {
      COLORS,
      sheetWidth: 0,
      sheetHeight: 0,
      backgroundImage: publicPath + "/images/default_bg.jpg",
    };
  },


  computed: {
    isLandscape() {
      return this.sheetWidth * 1.2 > this.sheetHeight;
    },
  },

  created() {
    this.updateSheetSize();
    window.addEventListener('resize', this.updateSheetSize);
  },

  destroyed() {
    window.removeEventListener('resize', this.updateSheetSize);
  },

  methods: {
    updateSheetSize() {
      const viewportWidth = window.innerWidth || document.documentElement.clientWidth;
      const viewportHeight = window.innerHeight || document.documentElement.clientHeight;

      this.sheetWidth = viewportWidth;
      this.sheetHeight = viewportHeight;
    },

  },
};
</script>

<style scoped>
div {
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}

h1 {
  font-size: 48px;
  font-family: "TitleFont", sans-serif;
  padding-bottom: 6px;
  display: inline-block;
  text-align: center;
}

p {
  padding-top: 6px;
  font-size: 18px;
  font-family: "Microsoft YaHei UI", sans-serif;
  display: inline-block;
  text-align: center;
}

p.institution-text {
  font-family: "Microsoft YaHei UI", sans-serif;
  display: inline-block;
  text-align: justify;
  text-indent: 3.5ch;
  padding-left:3em;
  padding-right:3em;
  /* Set default font size */
  font-size: 11px;
}

/* Media query for larger screens */
@media only screen and (min-width: 768px) {
  p.institution-text {
    width: 800px;
    font-size: 15px; /* Set larger font size for larger screens */
  }
}

@font-face {
  font-family: 'TitleFont';
  src: url('../assets/fonts/swissek.ttf') format('truetype')
}
</style>