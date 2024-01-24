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

      <!--  AnySite  -->
      <AppCard
        :color="COLORS.APP02_BG"
        :title-color="COLORS.APP02"
        :images="[publicPath + '/images/anysite/1.gif']"
        image-trasition="slide"
        img-position="right"
        apptitle="AnySite"
        :appDescription="$t('anysiteDesc')"
        :app-feature="['anysiteFea1','anysiteFea2','anysiteFea3']"
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
        :gallery-paths=genartGallery
      ></AppCardFill>

      <!--  NEXSpace  -->
      <AppCard
        :color="COLORS.APP04_BG"
        :title-color="COLORS.APP04"
        :images="anysiteImages"
        :text-color="COLORS.EMPTY"
        image-trasition="slide"
        img-position="left"
        apptitle="NEXSpace"
        :appDescription="$t('nexspaceDesc')"
        :app-feature="['nexspaceFea1','nexspaceFea2','nexspaceFea3']"
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
    anysiteImages: [],
    genartGallery: []
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
    // load simforms imgs
    this.simformsImages = []
    const path1 = publicPath + '/images/simforms/'
    for (let i = 0; i < 4; i++) {
      this.simformsImages.push(path1 + (i + 1) + '.jpg')
    }

    // load anysite imgs
    this.anysiteImages = []
    const path2 = publicPath + '/images/anysite/'
    for (let i = 0; i < 4; i++) {
      this.anysiteImages.push(path2 + (i + 1) + '.jpg')
    }

    // load genart imgs
    this.genartGallery = []
    const path3 = publicPath + '/images/genartGallery/'
    for (let i = 0; i < 10; i++) {
      this.genartGallery.push(path3 + (i + 1) + '.jpg')
    }
  }
};
</script>
