<template>
  <div>
    <v-app-bar
      app
      color="transparent"
      flat
      style="background: linear-gradient(rgba(100, 100, 100, 0.5), rgba(0, 0, 0, 0)); z-index: 99"
    >
      <v-row class="d-flex align-end mx-3 text-subtitle-1">

        <a class="text-decoration-none" href=" " style="color:#000000;">
          <v-img
            alt="Logo"
            class="shrink mr-2"
            contain
            src="@/assets/logo-black-500.png"
            transition="scale-transition"
            width="30"
          />
        </a>
        <a class="text-decoration-none" href="/#/" style="color:#000000;">
          <h2 class="pr-2">ArchiWeb</h2>
        </a>


      </v-row>


    </v-app-bar>
  </div>
</template>

<script>
export default {
  methods: {
    checkURL(url) {
      // console.log(url)
      if (url.indexOf('viewboard') >= 0 || url === '/')
        return true;
      return false;
    },
    scrollToPosition(key) {
      document.querySelector('#' + key).scrollIntoView();
    }
  }
}

</script>