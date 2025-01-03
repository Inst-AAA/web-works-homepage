<template>
  <v-app>
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

      <!--  SnapRender  -->
      <AppCard
        :color="COLORS.APP05_BG"
        :title-color="COLORS.APP05"
        :images="snaprenderImages"
        image-trasition="fade"
        img-position="right"
        apptitle="SnapRender"
        :appDescription="$t('snaprenderDesc')"
        :app-feature="['snaprenderFea1','snaprenderFea2','snaprenderFea3']"
        link="https://web.archialgo.com/render/"
      ></AppCard>

      <!--  ANYSite  -->
      <AppCard
        :color="COLORS.APP02_BG"
        :title-color="COLORS.APP02"
        :images="anysiteImages"
        image-trasition="fade"
        img-position="left"
        apptitle="ANYSite"
        :appDescription="$t('anysiteDesc')"
        :app-feature="['anysiteFea1','anysiteFea2','anysiteFea3']"
        link="https://web.archialgo.com/anysite/"
      ></AppCard>

      <!--  NEXUSpace  -->
      <AppCard
        :color="COLORS.APP04_BG"
        :title-color="COLORS.APP04"
        :images="nexuspaceImages"
        image-trasition="fade"
        img-position="right"
        apptitle="NEXUSpace"
        :appDescription="$t('nexuspaceDesc')"
        :app-feature="['nexuspaceFea1','nexuspaceFea2','nexuspaceFea3']"
        link="https://web.archialgo.com/nexuspace/"
      ></AppCard>

      <!--  ANYPlace  -->
      <AppCard
        :color="COLORS.APP06_BG"
        :title-color="COLORS.APP06"
        :images="anyplaceImages"
        image-trasition="fade"
        img-position="left"
        apptitle="ANYPlace"
        :appDescription="$t('anyplaceDesc')"
        :app-feature="['anyplaceFea1','anyplaceFea2','anyplaceFea3']"
        link="https://web.archialgo.com/anyplace/"
      ></AppCard>

      <!--  FLEXUrban  -->
      <AppCard
        :color="COLORS.APP07_BG"
        :title-color="COLORS.APP07"
        :images="flexurbanImages"
        image-trasition="fade"
        img-position="right"
        apptitle="FLEXUrban"
        :appDescription="$t('flexurbanDesc')"
        :app-feature="['flexurbanFea1','flexurbanFea2','flexurbanFea3']"
        link="https://web.archialgo.com/flexurban/"
      ></AppCard>

      <!--  GenArt  -->
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
    simformsImages: ['https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181458128.png',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181455368.png',
      'https://amomorning-image-base.oss-cn-hangzhou.aliyuncs.com/images/202406121116588.png',
    ],
    anysiteImages: ['https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/Snipaste_2024-06-18_15-28-39.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406131622658.jpeg',
    ],
    nexuspaceImages: ['https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/nexuspace-interface-20240618.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/nexuspace-wangyichen.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/nexuspace-zhuchangqing.jpg'
    ],
    anyplaceImages: [
      "https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20241112224821.jpg",
      "https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20241112224818.jpg",
      "https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20241112224815.jpg",
      "https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20241112224811.jpg",
      "https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20241112224757.jpg",
      "https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20241112224824.jpg",
    ],
    flexurbanImages: [
      "https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/Snipaste_2024-11-12_22-57-18.jpg",
      "https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20241112231145.jpg",
      "https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/Snipaste_2024-11-12_23-10-32.jpg"
    ],
    genartGallery: [],
    snaprenderImages: ['https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181504528.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181446445.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181503735.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181445759.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181513523.png',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181512416.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181447616.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181446397.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181512840.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181511435.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181508951.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181456551.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181509280.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181443823.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181510657.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181457469.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181443018.jpg',
      'https://archialgo-com-sources.oss-cn-hangzhou.aliyuncs.com/images/202406181500624.jpg',]
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
    // this.simformsImages = []
    // const path1 = publicPath + '/images/simforms/'
    // for (let i = 0; i < 4; i++) {
    //   this.simformsImages.push(path1 + (i + 1) + '.jpg')
    // }

    // // load anysite imgs
    // this.anysiteImages = []
    // const path2 = publicPath + '/images/anysite/'
    // for (let i = 0; i < 4; i++) {
    //   this.anysiteImages.push(path2 + (i + 1) + '.jpg')
    // }
    //
    // load genart imgs
    this.genartGallery = []
    const path3 = publicPath + '/images/genartGallery/'
    for (let i = 0; i < 10; i++) {
      this.genartGallery.push(path3 + (i + 1) + '.jpg')
    }
  }
};
</script>
