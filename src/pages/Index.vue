<template>
  <q-page class="flex flex-center">
    <div class="main-container">
      <div class="rowone">
        <q-select
          outlined
          v-model="select1"
          @input="select1changed"
          :options="options1"
          :dense="dense"
          class="text-h6 selectvalue"
          :options-dense="denseOpts"
        >
          <template v-slot:prepend>
            <q-icon size="16px" color="black">{{select1sym}}</q-icon>
          </template>
        </q-select>

        <q-icon color="red" @click="togglecurrency()" v-ripple name="compare_arrows" size="48px" />

        <q-select
          outlined
          @input="select2changed"
          v-model="select2"
          :options="options2"
          :dense="dense"
          class="text-h6 selectvalue"
          :options-dense="denseOpts"
        >
          <template v-slot:prepend>
            <q-icon size="16px" color="black">{{select2sym}}</q-icon>
          </template>
        </q-select>
      </div>

      <div class="rowtwo">
        <q-form @submit="submitForm()">
          <q-input
            outlined
            bottom-slots
            v-model="inputvalue"
            label="Enter Amount"
            type="number"
            :dense="dense"
          >
            <template v-slot:append>
              <q-btn @click="submitForm()" color="accent" glossy label="Convert" />
            </template>
          </q-input>
        </q-form>
      </div>

      <div class="rowthree">
        <p class="text-h3">{{answer}}</p>
      </div>
    </div>
  </q-page>
</template>

<script>
import axios from "axios";
import currencyToSymbolMap from "currency-symbol-map/map";
export default {
  name: "PageIndex",
  computed: {
    select1changed() {
      this.select1sym = currencyToSymbolMap[this.select1];
    },

    select2changed() {
      this.select2sym = currencyToSymbolMap[this.select2];
    }
  },
  methods: {
    submitForm() {
      console.log(this.inputvalue.length);
      if (this.inputvalue.length === 0) {
        this.$q.notify({
          message: "Enter valid amount",
          color: "red"
        });
      } else if (this.inputvalue === "0") {
        this.$q.notify({
          message: "0 Cannot be converted",
          color: "red"
        });
      } else {
        var v = +parseFloat(this.inputvalue);
        v = v.toFixed(2);
        axios
          .get("https://api.exchangerate-api.com/v4/latest/" + this.select1)
          .then(response => {
            if (response.status === 200) {
              var tovalue = parseFloat(response.data.rates[this.select2]);
              var answer = (v * tovalue).toFixed(2);
              this.answer = answer + " " + currencyToSymbolMap[this.select2];
            }
          });
      }
    },
    togglecurrency() {
      let value1 = this.select2;
      this.select2 = this.select1;
      this.select1 = value1;
      this.select1sym = currencyToSymbolMap[this.select1];
      this.select2sym = currencyToSymbolMap[this.select2];
      if (this.inputvalue !== "0" && this.inputvalue.length > 0) {
        this.submitForm();
      }
    }
  },
  data() {
    return {
      inputvalue: "",
      errorshow: false,
      answer: "0.00",
      select1: "USD",
      select2: "EUR",
      select1sym: currencyToSymbolMap["USD"],
      select2sym: currencyToSymbolMap["EUR"],

      options1: [],
      options2: [],

      dense: false,
      denseOpts: false
    };
  },
  mounted() {
    axios
      .get("https://api.exchangerate-api.com/v4/latest/USD")
      .then(response => {
        // handle success
        console.log(response.data.rates);
        const data = Object.keys(response.data.rates);
        var v = [];
        for (var i = 0; i < data.length; i++) {
          this.options1.push(data[i]);
          this.options2.push(data[i]);
        }
      });
  }
};
</script>

<style scoped>
.main-container {
  width: 90%;
  margin: 0 auto;
  max-width: 500px;
  display: grid;
  grid-gap: 50px;
  grid-template-columns: 1fr;
  justify-content: center;
}

.rowone {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  align-items: center;
  justify-items: center;
}
.selectvalue {
  width: 100%;
}
.rowthree {
  justify-self: center;
}
</style>