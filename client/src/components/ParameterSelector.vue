<template>
  <v-card outlined :loading="loading">
    <v-card-title>Parameter Tuner</v-card-title>
    <v-card-text>
      <p>
        Here you can alternate the parameters to get different results.<br>
        K1 and K2 are the weighting factors used in path recommendation, T1 and T2
        are the weighting factors used in information-layout recommendation.
      </p>
      <v-row no-gutters>
        <v-col class="pa-2" sm="2"><code>MV:</code></v-col>
        <v-col sm="4">
          <v-select :items="dataSource.mvcount"
                    v-model="parameter.mv"
                    placeholder="Select multivis count."
                    dense
          ></v-select>
        </v-col>
        <v-col class="pa-2" sm="6">
          <p>(Multi vis count)</p>
        </v-col>
      </v-row>

      <v-row no-gutters>
        <v-col class="pa-2" sm="2"><code>K1:</code></v-col>
        <v-col sm="4">
          <v-text-field
              dense
              v-model="parameter.k1"
          ></v-text-field>
        </v-col>
        <v-col class="pa-2" sm="2"><code>K2:</code></v-col>
        <v-col sm="4">
          <v-text-field
              dense
              v-model="parameter.k2"
          ></v-text-field>
        </v-col>
      </v-row>

      <v-row no-gutters>
        <v-col class="pa-2" sm="2"><code>T1:</code></v-col>
        <v-col sm="4">
          <v-text-field
              dense
              v-model="parameter.t1"
          ></v-text-field>
        </v-col>
        <v-col class="pa-2" sm="2"><code>T2:</code></v-col>
        <v-col sm="4">
          <v-text-field
              dense
              v-model="parameter.t2"
          ></v-text-field>
        </v-col>
      </v-row>

      <v-card-actions>
        <v-spacer></v-spacer>
        <p v-if="!fileSelected" class="warning--text mx-2 mt-2">You need to select file first.</p>
        <v-btn :disabled="!fileSelected" @click="confirmParameter" depressed>Confirm</v-btn>
      </v-card-actions>

    </v-card-text>
  </v-card>
</template>

<script>
import { EventBus } from "../plugins/event-bus";
import consts from "../config/consts.json";

export default {
  name: "ParameterSelector",
  data: () => ({
    loading: false,
    fileSelected: false,
    dataSource: {
      mvcount: [4, 5, 6, 7]
    },
    parameter: {
      mv: 4,
      k1: 0.5,
      k2: 0.5,
      t1: 0.5,
      t2: 0.5
    },
  }),
  mounted() {
    EventBus.$on(consts.events.DID_SELECT_FILE, ( { file }) => {
      this.fileSelected = file ? true : false;
    })
  },
  methods: {
    confirmParameter: function () {
      this.loading = true;
      setTimeout(() => {
        EventBus.$emit(consts.events.DID_SELECT_PARAMETER,
            { parameter: this.parameter,
              layoutData: {},
              graphData: {}});
        this.loading = false;
      }, Math.random() * 1000 + 500);
    }
  }
}
</script>

<style scoped>

</style>
