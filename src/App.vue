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
      v-if="!(localeLang==='en-US')"
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

      <HeadCard></HeadCard>

      <!--  SIMForms  -->
      <AppCard
        :color="COLORS.APP01_BG"
        :title-color="COLORS.APP01"
        :image="publicPath+'/images/simforms.gif'"
        img-position="left"
        apptitle="SIMForms"
        :app-description="$t('simformsDesc')"
        :app-feature="['simformsFea1','simformsFea2','simformsFea3']"
        link="https://web.archialgo.com/simforms/"
      ></AppCard>

      <!--  TypoGen  -->
      <AppCard
        :color="COLORS.APP02_BG"
        :title-color="COLORS.APP02"
        :image="publicPath+'/images/typogen.jpg'"
        img-position="right"
        apptitle="TypoGen"
        :appDescription="$t('typogenDesc')"
        :app-feature="['typogenFea1','typogenFea2','typogenFea3']"
      ></AppCard>

      <!--  Silk  -->
      <AppCardFill
        :color="COLORS.APP03_BG"
        :title-color="COLORS.APP03"
        :text-color="COLORS.APP03"
        :image="publicPath+'/images/scarves.jpg'"
        text-position="right"
        apptitle="GenArt"
        :gallery-paths=scarvesGallery
      ></AppCardFill>
    </v-main>

    <v-footer dark padless>
      <v-col
        class="text-center"
        cols="12"
      >
        {{ new Date().getFullYear() }} ©<strong>Inst. AAA</strong>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
import AppCard from './components/AppCard';
import AppCardFill from "@/components/AppCardFill.vue";
import {COLORS} from "@/color/colors";
import BackToTop from "@/components/BackToTop.vue";
import HeadCard from "@/components/HeadCard.vue";
import {publicPath} from "../vue.config";

export default {
  name: 'App',
  components: {
    BackToTop,
    AppCard,
    AppCardFill,
    HeadCard,
  },

  data: () => ({
    COLORS,
    publicPath,

    // localization
    isLocale: true,
    localeLang: '',
    supportedLang: [
      'en', 'en-US', 'en-GB', 'zh', 'zh-CN', 'zh-HK', 'zh-TW',
    ],

    // back-to-top
    showButton: false,

    // gallery paths
    scarvesGallery: []
  }),

  methods: {
    changeLanguage() {
      if (this.isLocale) {
        this.$i18n.locale = 'en-US';
      } else {
        this.$i18n.locale = this.localeLang;
      }
      this.isLocale = !this.isLocale
    },
  },

  mounted() {
    const navLang = navigator.language
    console.log('browser language: ' + navLang)

    if (this.supportedLang.includes(navLang)) {
      this.localeLang = navLang
    } else {
      this.localeLang = 'en-US'
    }
    this.$i18n.locale = this.localeLang;
  },

  created() {
    // load scarves imgs
    this.scarvesGallery = []
    const path = publicPath + '/images/scarvesImgs/'
    for (let i = 0; i < 20; i++) {
      this.scarvesGallery.push(path + (i + 1) + '.jpg')
    }
  }
};
</script>
