<template>
  <v-app>
    <!--    <v-app-bar-->
    <!--      app-->
    <!--      color="primary"-->
    <!--      dark-->
    <!--    >-->

    <!--    </v-app-bar>-->

    <v-btn
      v-if="!(localeLang==='en-US')"
      fab
      small
      color="secondary"
      @click="changeLanguage"
      style="position:fixed; top:12px; right: 16px; z-index: 2998"
    >
      <v-icon size="20px">mdi-translate-variant</v-icon>
    </v-btn>

    <v-main>
      <AppCard
        v-for="appid in appNum"
        :key="appid"
        :color="appThemeColors[appid-1]"
      ></AppCard>
    </v-main>
  </v-app>
</template>

<script>
import AppCard from './components/AppCard';
import {COLORS} from "@/color/colors";

export default {
  name: 'App',
  components: {
    AppCard,
  },

  data: () => ({
    COLORS,

    // localization
    isLocale: true,
    localeLang: '',
    supportedLang: [
      'en', 'en-US', 'en-GB', 'zh', 'zh-CN', 'zh-HK', 'zh-TW',
    ],

    // apps
    appNum: 2,
    appThemeColors: [
      COLORS.APP01,
      COLORS.APP02,
    ],
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
};
</script>
