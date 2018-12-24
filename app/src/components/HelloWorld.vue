<template>
  <v-container>
    <v-layout text-xs-center wrap>
      <v-flex xs12>
        <v-img :src="require('../assets/xmas.jpg')" class="my-3" contain height="400"></v-img>
      </v-flex>

      <v-flex mb-4>
        <h1 class="display-2 font-weight-bold mb-3">Frohe Weihnachten!</h1>
        <countdown-timer
          ereignis="Jahreswechsel"
          :zielDatum="endOfYear"
          class="subheading font-weight-regular"
        ></countdown-timer>
      </v-flex>

      <v-flex mb-4 xs4>
        <ul>
          <li>
            <v-text-field
              label="Name:"
              placeholder="Bitte gib deinen Namen ein"
              v-model="nameInput"
            ></v-text-field>
          </li>
          <li>
            <v-menu
              ref="menu"
              :close-on-content-click="false"
              v-model="menu"
              :nudge-right="40"
              lazy
              transition="scale-transition"
              offset-y
              full-width
              min-width="290px"
            >
              <v-text-field
                slot="activator"
                v-model="date"
                label="Geburtstag"
                prepend-icon="event"
                readonly
              ></v-text-field>
              <v-date-picker
                ref="picker"
                v-model="date"
                :max="new Date().toISOString().substr(0, 10)"
                min="1950-01-01"
                @change="save"
              ></v-date-picker>
            </v-menu>
          </li>
        </ul>
        <v-btn small @click="addNameAndBirthday">Hinzufügen</v-btn>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import CountdownTimer from "./CountdownTimer.vue";

export default {
  data: () => ({
    namesAndDates: [],
    nameInput: "",
    birthdayInput: null,
    date: null,
    menu: false,
    endOfYear: null
  }),
  methods: {
    addNameAndBirthday() {
      const newEntry = {
        name: this.nameInput,
        birthday: this.birthdayInput
      };
      this.namesAndDates.push(newEntry);
    },
    save(date) {
      this.$refs.menu.save(date);
    }
  },
  watch: {
    menu(val) {
      val && this.$nextTick(() => (this.$refs.picker.activePicker = "YEAR"));
    }
  },
  beforeMount: function() {
    this.endOfYear = new Date(2018, 11, 31).getTime();
  },
  components: { CountdownTimer }
};
</script>

<style>
</style>
