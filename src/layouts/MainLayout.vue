<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title>Live Currency Converter</q-toolbar-title>
        <div class="navbar">
        <q-separator dark vertical />
        <q-btn
          :class="{'active':homeactive}"
          @click="homepressed()"
          to="/"
          stretch
          flat
          label="Home"
          
        />
        <q-separator dark vertical />
        <q-btn
          :class="{'active':aboutactive}"
          @click="aboutpressed()"
          to="/about"
          stretch
          flat
          label="About"
        />
        <q-separator dark vertical />
        <q-btn
          type="a"
          href="https://github.com/immohanravi/livecurrencyconverter.git"
          target="_blank"
          color="yellow"
          class="text-overline"
          stretch
          flat
          label="Github"
        />
</div>
      </q-toolbar>
    </q-header>
   <q-footer>
      <q-tabs>
        <q-route-tab
          v-for="link in essentialLinks"
          :key="link.title"
          :to="link.link"
          :icon="link.icon"
          :label="link.title"
        />
      </q-tabs>
    </q-footer>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: "MainLayout",

  components: {},
  data() {
    return {
      tab: "",
      homeactive: true,
      aboutactive: false,
      essentialLinks: [
        {
          title: "Home",
          caption: "",
          icon: "home",
          link: "/"
        },
        {
          title: "About",
          caption: "",
          icon: "perm_device_information",
          link: "/about"
        }
      ]
    };
  },
  methods: {
    homepressed() {
      this.homeactive = true;
      this.aboutactive = false;
    },
    aboutpressed() {
      this.homeactive = false;
      this.aboutactive = true;
    }
  }
};
</script>
<style scoped>
.active {
  background: #0c2780;
}
.navbar{
  display: flex;
}
.q-footer{
  display: none;
}
@media screen and (max-width: 600px) {
  .q-footer {
    display: inline-block;
  }
  .navbar{
    display: none;
  }

  q-toolbar-title{
    text-align: center;
  }
}
</style>