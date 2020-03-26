<template>
  <q-page class="flex flex-center">
    <q-card dark bordered class="bg-grey-9 my-card">
      <q-card-section>
        <div class="text-h6 absolute-center">Live Currency Converter</div>
      </q-card-section>

      <q-separator dark inset />

      <q-card-section>
        <p>
          This is demo app using quasar framwork which fetchs exchange data from
          <a
            href="https://www.exchangerate-api.com/"
            target="_blank"
          >
            <b>Exchangerate-api.com</b>
          </a>. This app is for demonstration purpose only.
        </p>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex"
};
</script>

<style scoped>
.my-card {
  width: 100%;
  height: 100%;
  max-width: 500px;
  max-height: 500px;
}
a {
  color: white;
}
a:visited{
  color: yellow;
}
@media screen and (max-width: 600px) {

  .my-card{
    margin: 25px;
  }

}
</style>