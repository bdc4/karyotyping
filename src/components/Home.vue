
<template>
  <v-container class="d-flex flex-row" v-if="isLoggedIn">
    <v-row>
      <v-col cols="2">
        <v-tabs vertical v-model="tabSelection" bg-color="primary">
          <v-tab :value="0">Introduction</v-tab>
          <v-tab :value="1">Patient A</v-tab>
          <v-tab :value="2">Patient B</v-tab>
          <v-tab :value="3">Patient C</v-tab>
        </v-tabs>
      </v-col>
      <v-col cols="10">
        <v-window v-model="tabSelection">
          <v-window-item :value="0">
            <Introduction></Introduction>
          </v-window-item>

          <v-window-item :value="1">
            <PatientActivity id="A"></PatientActivity>
          </v-window-item>

          <v-window-item :value="2">
            <PatientActivity id="B"></PatientActivity>
          </v-window-item>

          <v-window-item :value="3">
            <PatientActivity id="C"></PatientActivity>
          </v-window-item>
        </v-window>
      </v-col>
    </v-row>

  </v-container>
</template>

<script>
import Introduction from './Introduction.vue';
import PatientActivity from './PatientActivity.vue';

export default {
  name: 'Home',
  components: {
    Introduction,
    PatientActivity
  },
  data() {
    return {
      tabsModel: {
        active: 0,
        login: false,
        password: '12345'
      }
    }
  },
  computed: {
    tabSelection: {
      get() {
        return this.tabsModel.active
      },
      set(newVal) {
        this.tabsModel.active = newVal;
      }
    },
    isLoggedIn () {
      var correct = this.checkPasswordMatch();
      while (!correct) {
        correct = this.checkPasswordMatch();
      }
      return correct;
    }
  },
  methods: {
    checkPasswordMatch() {
      // Take that, SEO!!
      var guess = prompt("Please enter the password");
      var password = "SCCbio";
      return guess == password;
    }
  }
}
</script>
