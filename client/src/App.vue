<template>
  <v-app>
    <v-app-bar
      app
      color="blue-grey"
      dark
    >
      <div class="d-flex align-center">
        <h3> Data-driven Dashboard Recommendation System </h3>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/billchen2k/multiview-vis-demo"
        target="_blank"
        text
      >
<!--        <span class="mr-2"></span>-->
        <v-icon>mdi-github</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container fluid>

        <v-row>

          <v-col lg="3">
            <file-selector class="my-3"></file-selector>
            <parameter-selector class="my-3"></parameter-selector>
            <graph-viewer class="my-3"></graph-viewer>

<!--            <tree-viewer class="my-3"></tree-viewer>-->

          </v-col>

          <v-col lg="6">
<!--            <v-row no-gutters>-->
<!--            </v-row>-->
            <v-row no-gutters>
              <layout-viewer class="my-3"></layout-viewer>
            </v-row>
            <v-row no-gutters>
              <multiview-chart-preview class="my-3"></multiview-chart-preview>
              <!--            <line-chart :data="data" :options="{}"></line-chart>-->
            </v-row>
          </v-col>


          <v-col lg="3">
            <chart-selector  class="my-3"></chart-selector>
          </v-col>
        </v-row>
      </v-container>


    </v-main>
  </v-app>
</template>

<script>

import ChartSelector from './components/ChartSelector';
import FileSelector from "./components/FileSelector";
import LayoutViewer from "./components/LayoutViewer";
import MultiviewChartPreview from "./components/MultiviewChartPreview";
import ParameterSelector from "./components/ParameterSelector";
import TreeViewer from "./components/TreeViewer";
import GraphViewer from "./components/GraphViewer";

import { EventBus } from "./plugins/event-bus";
import consts from "./config/consts.json";

export default {
  name: 'App',

  components: {
    GraphViewer,
    // LineChart,
    ChartSelector,
    FileSelector,
    LayoutViewer,
    MultiviewChartPreview,
    ParameterSelector
  },
  mounted() {
    setTimeout(() => {

    }, 1000);
  },

  data: () => ({
    currentStage: 0,
    selectedFile: "",
  })

};
</script>
