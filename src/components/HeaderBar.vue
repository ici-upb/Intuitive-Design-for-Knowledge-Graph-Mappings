<template>
  <v-toolbar color="#2196F3" dark>
    <v-btn v-if="activeBackButton" icon @click="openDialog">
      <v-icon>mdi-arrow-left</v-icon>
    </v-btn>
    <v-toolbar-title>Knowledge Graph Mapping Tool</v-toolbar-title>

    <v-row class="text-right">
      <v-col>
        <v-tooltip v-if="activeBackButton" bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-btn icon v-bind="attrs" v-on="on" @click="openHelp">
              <v-icon> mdi-help </v-icon>
            </v-btn>
          </template>
          <span>Help</span>
        </v-tooltip>
        
        <v-tooltip v-if="activeBackButton" bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-btn icon v-bind="attrs" v-on="on" @click="openInfo">
              <v-icon> mdi-information </v-icon>
            </v-btn>
          </template>
          <span>Information about the project</span>
        </v-tooltip>

        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-btn icon v-bind="attrs" v-on="on" target="_blank" href="https://github.com/SWENG-Group-10/Intuitive-Design-for-Knowledge-Graph-Mappings">
              <v-icon> mdi-github </v-icon>
            </v-btn>
          </template>
          <span>Project repository</span>
        </v-tooltip>

      </v-col>
    </v-row>
  </v-toolbar>
</template>

<script>
export default {
  name: 'HeaderBar',
  props: {
    activeBackButton: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  methods: {
    openHelp() {
      this.$emit('openHelp');
    },
    openInfo() {
      this.$emit('openInfo');
    },
    openDialog() {
      this.$emit('openDialog');
    }
  },
};
</script>
