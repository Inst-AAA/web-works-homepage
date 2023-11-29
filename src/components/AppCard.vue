<template>
  <v-sheet
    :color=color
    :style="{ width: sheetWidth + 'px', height: sheetHeight + 'px' }"
  >
    <v-row
      justify="center"
      align="center"
      style="height: 100%"
      class="ma-0 pa-0"
    >
      <v-col
        cols="6"
        class="pa-0"
      >
        <v-img
          src="https://tse4-mm.cn.bing.net/th/id/OIP-C.duz6S7Fvygrqd6Yj_DcXAQHaF7?rs=1&pid=ImgDetMain"
        />
      </v-col>
      <v-col
        cols="6"
      >
        <p>Right Text</p>
      </v-col>
    </v-row>
  </v-sheet>
</template>

<script>

export default {
  data() {
    return {
      sheetWidth: 0,
      sheetHeight: 0,
    };
  },

  props: {
    color: Object,
    appID: Number,
  },

  computed: {
    isLandscape() {
      return this.sheetWidth > this.sheetHeight;
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

    getContentStyle() {
      return {
        display: 'flex',
        flexDirection: this.isLandscape ? 'row' : 'column',
        justifyContent: this.isLandscape ? 'flex-start' : 'center',
        alignItems: this.isLandscape ? 'center' : 'flex-start',
      };
    },
  },
};
</script>

<style scoped>

</style>