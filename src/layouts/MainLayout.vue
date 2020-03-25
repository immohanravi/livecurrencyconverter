<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
         <q-toolbar-title >
          Live Currency Converter
        </q-toolbar-title>

           <q-separator dark vertical />
      <q-btn :class="{'active':homeactive}" @click="homepressed()" to="/" stretch flat label="Home" />
      <q-separator dark vertical />
      <q-btn :class="{'active':aboutactive}" @click="aboutpressed()" to="/about" stretch flat label="About" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',

  components: {
   
  },
  data () {
    return {
      tab: '',
      homeactive: true,
      aboutactive: false
    }
  },
  methods: {
    homepressed(){
      this.homeactive = true;
      this.aboutactive = false;
    },
    aboutpressed(){
      this.homeactive = false;
      this.aboutactive = true;
    }
  }

 
  
}
</script>
<style scoped>
.active{
  background: #0c2780;
}
</style>