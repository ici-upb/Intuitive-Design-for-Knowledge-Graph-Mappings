<template>
  <v-card width="2400">
    <v-stepper v-model="actualStep">
      <v-stepper-header>
        <v-stepper-step :complete="actualStep > 1" step="1"> Ontology Viewer </v-stepper-step>

        <v-divider />

        <v-stepper-step :complete="actualStep > 2" step="2"> JSON Viewer </v-stepper-step>

        <v-divider/>

        <v-stepper-step :complete="actualStep > 3" step="3"> Mapping Creator </v-stepper-step>

        <v-divider/>

        <v-stepper-step :complete="actualStep > 4" step="4"> Downloading Mappings </v-stepper-step>

        <v-divider/>

        <v-stepper-step step="5"> Starting Over </v-stepper-step>
      </v-stepper-header>

      <v-stepper-items>
        <v-stepper-content step="1" class="text-center">
          <v-card class="mb-2 text-center" color="white" flat>                   
            <v-img src="../assets/ontology.png" max-width="1200"  class="mx-auto"/>
          </v-card>
          <h2 class="mb-12">The top right part of the page displays your ttl file on the WebVowl system.</h2>                
          <v-btn color="blue" dark @click="actualStep = 2" class="mr-2"> Continue </v-btn>
          <v-btn text @click="close()"> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-content step="2" class="text-center">    
          <v-card class="mb-2 text-center" color="white" flat>
            <v-img src="../assets/jsonview.png" max-width="1200" class="mx-auto"/>
          </v-card>
          <h2 class="mb-12">The bottom right part of the page displays your JSON file which you can scroll through.</h2>
          <v-btn color="blue" @click="actualStep = 3" class="mr-2" dark> Next </v-btn>
          <v-btn text @click="actualStep = 1"> Previous </v-btn>
        </v-stepper-content>

        <v-stepper-content step="3" class="text-center">
          <v-card class="mb-2" color="white" flat>
            <v-img src="../assets/mapping.png" max-width="1200" class="mx-auto"/>
          </v-card>
          <h2 class="mb-12">On the left hand side you can find jigsaw pieces in each of the categories on the left and then use these pieces to create your mappings.</h2>
          <v-btn color="blue" @click="actualStep = 4" class="mr-2" dark> Next </v-btn>
          <v-btn text @click="actualStep = 2"> Previous </v-btn>
        </v-stepper-content>

        <v-stepper-content step="4" class="text-center">
          <v-card class="mb-2" color="white" flat>
            <v-img src="../assets/button.png" max-width="1200" class="mx-auto"/>
          </v-card>
          <h2 class="mb-12">To download your Mapping by pressing the "Download Mapping" button at the bottom of the page.</h2>
          <v-btn color="blue" @click="actualStep = 5" class="mr-2" dark> Next </v-btn>
          <v-btn text @click="actualStep = 3"> Previous </v-btn>
        </v-stepper-content>

        <v-stepper-content step="5" class="text-center">
          <v-card class="mb-2" color="white" flat>
            <v-img :src="`${baseAssetsURL}reset.png`" max-width="1200" class="mx-auto"/>
          </v-card>
          <h2 class="mb-12">To upload new files please press the return button on the top left of the page which will bring you back to the original landing page.</h2>
          <v-btn color="blue" @click="actualStep = 1" class="mr-2" dark> Start Again </v-btn>
          <v-btn text @click="close(); actualStep = 1"> I Got It Thanks! </v-btn>
        </v-stepper-content>
      </v-stepper-items>
    </v-stepper>
  </v-card>
</template>

<script>

export default {
  name: 'Help',
  data: () => ({
    baseAssetsURL: '../assets/',
    actualStep: 1,
    help: false, //boolean for help button dialog box
    text: "",
    ttl: ""
  }),
  methods: {
    close() {
      this.$emit('close');
    }
  },
};
</script>
