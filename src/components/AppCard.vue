<template>
  <v-sheet
    :color=color
    height="900px"
    :style="{ width: sheetWidth + 'px'}"
  >
    <!-- 相册 -->
    <v-dialog
      v-model="showGallery"
      width="800"
    >
      <ImageGallery
        height="100%"
        :img-path="galleryPaths"
      />
    </v-dialog>

    <!-- 横屏左图 -->
    <v-row
      v-if="isLandscape&&imgPosition==='left'"
      justify="center"
      align="center"
      style="height: 100%"
      class="ma-0 pa-0"
    >
      <!-- 图片 -->
      <v-col
        cols="7"
        class="pa-0"
        style="height: 100%"
        id="videoArea"
      >
        <div class="slider" v-if="imageTrasition==='fade'">
          <transition name="fade" mode="out-in" :duration="{ enter: 500, leave: 500 }">
            <img :key="currentImage" :src="getImagePath" class="slide" alt="Slider Image">
          </transition>
        </div>
        <v-carousel
          v-if="imageTrasition==='slide'"
          height="100%"
          cycle
          interval="3000"
          hide-delimiters
          :show-arrows="false"
        >
          <v-carousel-item
            v-for="(item,i) in images"
            :key="i"
            :src="item"
          >
          </v-carousel-item>
        </v-carousel>
      </v-col>
      <!-- 文字 -->
      <v-col
        cols="5"
        class="px-16"
      >
        <h1
          :style="{color: titleColor}"
        >
          {{ apptitle }}
        </h1>
        <p :style="{color: textColor}">{{ appDescription }}</p>
        <ul>
          <li
            v-for="(fea, id) in appFeature"
            :key="id"
            :style="{color: textColor}"
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
          target="_blank"
          outlined
        >
          <v-icon left>mdi-view-gallery-outline</v-icon>
          {{ $t('gallery') }}
        </v-btn>
      </v-col>
    </v-row>

    <!-- 横屏右图 -->
    <v-row
      v-else-if="isLandscape&&imgPosition==='right'"
      justify="center"
      align="center"
      style="height: 100%"
      class="ma-0 pa-0"
    >
      <!-- 文字 -->
      <v-col
        cols="5"
        class="px-16"
      >
        <h1 :style="{color: titleColor}">{{ apptitle }}</h1>
        <p :style="{color: textColor}">{{ appDescription }}</p>
        <ul>
          <li
            v-for="(fea, id) in appFeature"
            :key="id"
            :style="{color: textColor}"
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
          target="_blank"
          outlined
        >
          <v-icon left>mdi-view-gallery-outline</v-icon>
          {{ $t('gallery') }}
        </v-btn>
      </v-col>
      <!-- 图片 -->
      <v-col
        cols="7"
        class="pa-0"
        style="height: 100%"
      >
        <div class="slider" v-if="imageTrasition==='fade'">
          <transition name="fade" mode="out-in" :duration="{ enter: 500, leave: 500 }">
            <img :key="currentImage" :src="getImagePath" class="slide" alt="Slider Image">
          </transition>
        </div>
        <v-carousel
          v-if="imageTrasition==='slide'"
          height="100%"
          cycle
          interval="3000"
          hide-delimiters
          :show-arrows="false"
        >
          <v-carousel-item
            v-for="(item,i) in images"
            :key="i"
            :src="item"
          >
          </v-carousel-item>
        </v-carousel>
      </v-col>
    </v-row>

    <!-- 竖屏 -->
    <v-container
      v-else
      style="height: 100%;justify-content: center;align-content: center"
      class="ma-0 pa-0"
    >
      <!-- 图片 -->
      <v-row
        style="height: 35%"
        class="pa-0 ma-0"
      >
        <v-col cols="12" class="pa-0 ma-0">
          <div class="slider" v-if="imageTrasition==='fade'">
            <transition name="fade" mode="out-in" :duration="{ enter: 500, leave: 500 }">
              <img :key="currentImage" :src="getImagePath" class="slide" alt="Slider Image">
            </transition>
          </div>
          <v-carousel
            v-if="imageTrasition==='slide'"
            height="100%"
            cycle
            interval="3000"
            hide-delimiters
            :show-arrows="false"
          >
            <v-carousel-item
              v-for="(item,i) in images"
              :key="i"
              :src="item"
            >
            </v-carousel-item>
          </v-carousel>
        </v-col>
      </v-row>
      <!-- 文字 -->
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
            target="_blank"
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
// import videojs from "video.js";

export default {
  components: {ImageGallery},
  data() {
    return {
      sheetWidth: 0,
      sheetHeight: 0,

      currentImage: 0,

      showGallery: false,
    };
  },

  props: {
    color: String,
    titleColor: String,
    textColor: String,

    images: Array,
    imageTrasition: {
      type: String,
      default: 'slide',
      validator: function (value) {
        return ['fade', 'slide'].includes(value);
      },
    },
    apptitle: String,

    appDescription: String,
    appFeature: Array,

    link: String,
    galleryPaths: Array,

    imgPosition: {
      type: String,
      default: 'left',
      validator: function (value) {
        return ['left', 'right'].includes(value);
      },
    },
  },

  mounted() {
    this.interval = setInterval(this.nextImage, 3000);
  },
  beforeDestroy() {
    clearInterval(this.interval);
  },
  computed: {
    getImagePath() {
      return this.images[this.currentImage];
    },
    isLandscape() {
      return this.sheetWidth * 1.2 > this.sheetHeight;
    },
  },

  created() {
    // this.videoPlayer = videojs('my-video', {
    //   autoplay: 'muted'
    // });
    this.updateSheetSize();
    window.addEventListener('resize', this.updateSheetSize);
  },

  destroyed() {
    window.removeEventListener('resize', this.updateSheetSize);
  },

  methods: {
    nextImage() {
      this.currentImage = (this.currentImage + 1) % this.images.length;
    },

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
.slider {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.slide {
  width: 100%;
  height: 100%;
  object-fit: cover;
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