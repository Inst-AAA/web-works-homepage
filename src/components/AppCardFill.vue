<template>
  <v-sheet
    :color=color
    :style="{ width: sheetWidth + 'px', height: sheetHeight + 'px' }"
  >
    <!-- 相册 -->
    <v-dialog
      v-model="showGallery"
      width="65%"
    >
      <ImageGallery
        height="100%"
        :img-path="galleryPaths"
      />
    </v-dialog>

    <!-- 横屏满铺 -->
    <v-img
      v-if="isLandscape"
      :src="image"
      height="100%"
      width="100%"
    >

      <!-- 文字在左 -->
      <v-row
        v-if="textPosition==='left'"
        style="height: 100%"
        align="center"
      >
        <v-col
          cols="5"
          class="px-16"
        >
          <h1 :style="{color: titleColor}">{{ apptitle }}</h1>
          <p :style="{color: textColor}">{{ appDescription }}</p>
          <ul>
            <li
              :style="{color: textColor}"
              v-for="(fea, id) in appFeature"
              :key="id"
            >
              {{ $t(fea) }}
            </li>
          </ul>
          <v-btn
            v-if="link"
            :color="titleColor"
            :href="link"
            target="_blank"
            outlined
          >
            <div>{{ $t('view') }}</div>
          </v-btn>
          <v-btn
            v-if="galleryPaths"
            :color="titleColor"
            @click="showGallery=true"
            outlined
          >
            <div>{{ $t('gallery') }}</div>
          </v-btn>
        </v-col>
      </v-row>

      <!-- 文字在右 -->
      <v-row
        v-else
        style="height: 100%"
        align="center"
        justify="end"
      >
        <v-col
          cols="5"
          class="px-16"
        >
          <h1 :style="{color: titleColor}">{{ apptitle }}</h1>
          <p :style="{color: textColor}">{{ appDescription }}</p>
          <ul>
            <li
              :style="{color: textColor}"
              v-for="(fea, id) in appFeature"
              :key="id"
            >
              {{ $t(fea) }}
            </li>
          </ul>
          <v-btn
            v-if="link"
            :color="titleColor"
            :href="link"
            target="_blank"
            outlined
          >
            <v-icon left>mdi-launch</v-icon>
            {{ $t('view') }}
          </v-btn>
          <v-btn
            v-if="galleryPaths"
            :color="titleColor"
            @click="showGallery=true"
            outlined
          >
            <v-icon left>mdi-view-gallery-outline</v-icon>
            {{ $t('gallery') }}
          </v-btn>
        </v-col>
      </v-row>
    </v-img>


    <!-- 竖屏 -->
    <v-container
      v-else
      style="height: 100%;justify-content: center;align-content: center"
      class="ma-0 pa-0"
    >
      <v-row
        style="height: 35%"
        class="pa-0 ma-0"
      >
        <v-col cols="12" class="pa-0 ma-0">
          <v-img
            height="100%"
            :src="image"
          />
        </v-col>

      </v-row>
      <v-row
        style="height:65%"
        class="pa-0 ma-0"
      >
        <v-col cols="12" class="ma-0 px-8 pt-6 pb-4">
          <h1 class="h1Vertical" :style="{color: titleColor}">{{ apptitle }}</h1>
          <p :style="{color: textColor}" class="pVertical">{{ appDescription }}</p>
          <ul>
            <li
              :style="{color: textColor}"
              class="liVertical"
              v-for="(fea, id) in appFeature"
              :key="id"
            >
              {{ $t(fea) }}
            </li>
          </ul>
          <v-btn
            v-if="link"
            :color="titleColor"
            :href="link"
            target="_blank"
            outlined
          >
            <v-icon left>mdi-launch</v-icon>
            {{ $t('view') }}
          </v-btn>
          <v-btn
            v-if="galleryPaths"
            :color="titleColor"
            @click="showGallery=true"
            outlined
          >
            <v-icon left>mdi-view-gallery-outline</v-icon>
            {{ $t('gallery') }}
          </v-btn>
        </v-col>

      </v-row>
    </v-container>
  </v-sheet>
</template>

<script>

import ImageGallery from "@/components/ImageGallery.vue";

export default {
  components: {ImageGallery},
  data() {
    return {
      sheetWidth: 0,
      sheetHeight: 0,

      showGallery: false,
    };
  },

  props: {
    color: String,
    titleColor: String,

    image: String,
    apptitle: String,

    appDescription: String,
    appFeature: Array,

    link: String,
    galleryPaths: Array,

    textColor: String,
    textPosition: {
      type: String,
      default: 'left',
      validator: function (value) {
        return ['left', 'right'].includes(value);
      },
    },
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
.divFill {
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 500px;
}

h1 {
  font-size: 48px;
  font-family: "TitleFont", sans-serif;
  padding-bottom: 6px;
}

p {
  padding-top: 6px;
  font-size: 16px;
  font-family: "Microsoft YaHei UI", sans-serif;
}

ul {
  padding-bottom: 24px;
}

li {
  padding-top: 6px;

  font-style: italic;
  font-size: 16px;
  font-family: "Microsoft YaHei UI Light", sans-serif;
}

.h1Vertical {
  font-size: 38px;
  font-family: "TitleFont", sans-serif;
  padding-bottom: 6px;
}

.pVertical {
  padding-top: 6px;
  font-size: 13px;
  font-family: "Microsoft YaHei UI", sans-serif;
}

.liVertical {
  padding-top: 6px;

  font-style: italic;
  font-size: 13px;
  font-family: "Microsoft YaHei UI Light", sans-serif;
}

@font-face {
  font-family: 'TitleFont';
  src: url('../assets/fonts/swissek.ttf') format('truetype')
}

</style>