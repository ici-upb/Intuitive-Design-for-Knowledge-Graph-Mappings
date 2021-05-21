<template>
  <v-row>
    <v-col cols="11">
      <v-card flat tile height="800">
        <BlocklyComponent id="blockly2" :options="options" ref="foo"></BlocklyComponent>
      </v-card>
    </v-col>
    <v-col cols="1" justify="start" class="pt-5 button-section">
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn @click="saveFile()" color="white" icon v-bind="attrs" v-on="on">
            <v-icon>mdi-download</v-icon>
          </v-btn>
        </template>
        <span>Download Mapping as .json</span>
      </v-tooltip>
    </v-col>
  </v-row>
</template>

<script>
import BlocklyComponent from "./BlocklyComponent"
import '../blocks/blocks'
import BlocklyJS from 'blockly/javascript';

export default {
  name: 'app',
  components: {
    BlocklyComponent
  },
  data() {
    return {
      code: '',
      mapping: '',
      options: {
        trashcan: true,
        grid: {
          spacing: 25,
          length: 3,
          colour: '#ccc',
          snap: true
        },
        toolbox: `<xml>
          <category name="Class" colour="green">
          <block type="class_block"></block>
          </category>
          <category name="ID" colour="blue">
          <block type="id_block"></block>
          </category>
          <category name="Relation" colour="red">
          <block type="relation_block"></block>
          </category>
          <category name="Value" colour="black">
                <block type="value_block"></block>
            </category>
          <category name="Function" colour="purple">
          <block type="uc_block"></block>
          <block type="lc_block"></block>
          </category>
          <category name="Type" colour="yellow">
          <block type="str_block"></block>
          <block type="num_block"></block>
          </category>
        </xml>`
      }
    }
  },
  methods: {
    saveFile: function () {
      console.log('this.code')
      this.code = BlocklyJS.workspaceToCode(this.$refs["foo"].workspace)
      console.log('this.code', this.code)
      let json = this.code.slice(0, -2)
      console.log('json', json)
      this.mapping = JSON.parse(json)
      const data = JSON.stringify(this.mapping, null, 2)
      const blob = new Blob([data], {
          type: 'text/plain'
      })
      const e = document.createEvent('MouseEvents'),
      a = document.createElement('a');
      a.download = "mapping.json";
      a.href = window.URL.createObjectURL(blob);
      a.dataset.downloadurl = ['text/json', a.download, a.href].join(':');
      e.initEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
      a.dispatchEvent(e);
    },
  }
}
</script>

<style>
  #blockly2 {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
  }
  .button-section {
    background-color: #2196F3;
  }
</style>
