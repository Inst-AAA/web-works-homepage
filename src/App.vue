<template>
  <v-app style="user-select: none">
    <!--    <v-app-bar-->
    <!--      app-->
    <!--      absolute-->
    <!--      color="transparent"-->
    <!--      dark-->
    <!--    >-->

    <!--    </v-app-bar>-->

    <!--  localization button  -->
    <v-btn
      fab
      small
      outlined
      color="secondary"
      @click="changeLanguage"
      style="position:fixed; top:12px; right: 16px; z-index: 2998; background-color: rgba(255,255,255,0.34)"
    >
      <v-icon size="20px">mdi-translate-variant</v-icon>
    </v-btn>

    <v-main>
      <BackToTop></BackToTop>

      <TopNavi></TopNavi>
      <HeadCard></HeadCard>
      <PageFooter></PageFooter>

      <!--  SIMForms  -->
      <AppCard
        :color="COLORS.APP01_BG"
        :title-color="COLORS.APP01"
        :images="simformsImages"
        image-trasition="fade"
        img-position="left"
        apptitle="SIMForms"
        :app-description="$t('simformsDesc')"
        :app-feature="['simformsFea1','simformsFea2','simformsFea3']"
        link="https://web.archialgo.com/simforms/"
      ></AppCard>

      <!--  Silk  -->
      <AppCardFill
        :color="COLORS.APP03_BG"
        :title-color="COLORS.APP03"
        :text-color="COLORS.APP03"
        :image="publicPath+'/images/genart.jpg'"
        text-position="right"
        apptitle="GenArt"
        :appDescription="$t('genartDesc')"
        :gallery-paths=scarvesGallery
      ></AppCardFill>

      <!--  TypoGen  -->
      <AppCard
        :color="COLORS.APP02_BG"
        :title-color="COLORS.APP02"
        :images="typogenImages"
        image-trasition="slide"
        img-position="right"
        apptitle="TypoGen"
        :appDescription="$t('typogenDesc')"
        :app-feature="['typogenFea1','typogenFea2','typogenFea3']"
      ></AppCard>
    </v-main>
  </v-app>
</template>

<script>
import AppCard from './components/AppCard';
import AppCardFill from "@/components/AppCardFill.vue";
import {COLORS} from "@/color/colors";
import BackToTop from "@/components/BackToTop.vue";
import HeadCard from "@/components/HeadCard.vue";
import {publicPath} from "../vue.config";
import TopNavi from "@/components/TopNavi.vue";
import PageFooter from "@/components/PageFooter.vue";

export default {
  name: 'App',
  components: {
    PageFooter,
    TopNavi,
    BackToTop,
    AppCard,
    AppCardFill,
    HeadCard,
  },

  data: () => ({
    COLORS,
    publicPath,

    // localization
    isChinese: true,
    supportedChinese: [
      'zh', 'zh-CN', 'zh-HK', 'zh-TW',
    ],

    // back-to-top
    showButton: false,

    // gallery paths
    simformsImages: [],
    typogenImages: [],
    scarvesGallery: []
  }),

  methods: {
    changeLanguage() {
      if (this.isChinese) {
        this.$i18n.locale = 'en-US';
      } else {
        this.$i18n.locale = 'zh-CN';
      }
      this.isChinese = !this.isChinese
    },
  },

  mounted() {
    const navLang = navigator.language
    // console.log('browser language: ' + navLang)

    if (this.supportedChinese.includes(navLang)) {
      this.isChinese = true
      this.$i18n.locale = 'zh-CN'
    } else {
      this.isChinese = false
      this.$i18n.locale = 'en-US'
    }
  },

  created() {
    // load scarves imgs
    this.simformsImages = []
    const path1 = publicPath + '/images/simforms/'
    for (let i = 0; i < 4; i++) {
      this.simformsImages.push(path1 + (i + 1) + '.jpg')
    }

    // load scarves imgs
    this.typogenImages = []
    const path2 = publicPath + '/images/typogen/'
    for (let i = 0; i < 4; i++) {
      this.typogenImages.push(path2 + (i + 1) + '.jpg')
    }

    // load scarves imgs
    this.scarvesGallery = []
    const path3 = publicPath + '/images/genartGallery/'
    for (let i = 0; i < 20; i++) {
      this.scarvesGallery.push(path3 + (i + 1) + '.jpg')
    }
  }
};
</script>
