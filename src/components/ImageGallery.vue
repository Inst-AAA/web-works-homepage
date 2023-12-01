<template>

  <v-carousel
    height="100%"
    hide-delimiters
  >
    <v-carousel-item
      v-for="(item,i) in imgPath"
      :key="i"
      :src="item"
    >

    </v-carousel-item>
  </v-carousel>

</template>

<script>

import {COLORS} from "@/color/colors";

export default {
  data: () => ({
    COLORS,
  }),

  props: {
    show: {
      type: Boolean,
      default: false,
    },
    imgPath: Array,
    height: Number,
    width: Number,
  }
}
</script>

<style scoped lang="scss">
@import "@/color/colors.scss";

.style-container {
  margin-top: 10px;
  margin-bottom: 10px;
}

.database-toolbar {
  background-color: $SECONDARY;
  color: $TITLE_WHITE;
}

.style-card {
  transition: opacity .3s ease-in-out;
  opacity: 0.3;
  filter: grayscale(100%);
}

.hover-style-card {
  transition: opacity .3s ease-in-out;
  box-shadow: 0 0 12px $INFO;
  filter: grayscale(0%);
}

.selected-style-card {
  opacity: 1;
  box-shadow: 0 0 18px $PRIMARY;
  filter: grayscale(0%);
}

.button-group {
  margin-top: 5px;
  margin-bottom: 5px;
  text-align: right;
}

</style>