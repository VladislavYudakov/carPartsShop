<script>
import {ref, watch} from "vue";
import Csv2json from "csvjson-csv2json";

export default {
  setup() {

    const file = ref();
    const fileContentsToJson = ref();

    // const addCells = ref(new Set());
    const addCells = ref([]);

    /* Detect input file */
    watch(file, (file) => {
      if (file instanceof File) {
        extractFileContents(file);
      }
    });

    watch(fileContentsToJson, async () => {
      console.log(fileContentsToJson);
    });

    const extractFileContents = (file) => {
      // file.value.file = this.$refs['file-input'].files[0];

      let reader = new FileReader();
      reader.onload = () => {
        fileContentsToJson.value = Csv2json.csv2json(reader.result);
      };
      reader.readAsText(file);
    };

    const clearFiles = () => {
      // this.$refs['file-input'].reset()
      file.value = null;
    }

    const addCellsByInput = (e) => {
      if (!addCells.value.find(cell => cell === e.target.value)) {
        addCells.value.push(e.target.value);
        console.log(addCells.value);
        e.target.value = "";
      }
    }

    return {file, fileContentsToJson, addCells, extractFileContents, clearFiles, addCellsByInput};
  }
}
</script>

<template>
  <div>
    <b-form-file v-model="file" ref="file-input" class="mb-2"></b-form-file>

    <div class="d-flex justify-content-center align-items-center">
      <p class="mt-3">Selected file: <b>{{ file ? file.name : '' }}</b></p>
      <!--    <b-button @click="file = null">Reset via v-model</b-button>-->
      <b-button v-if="file != null" @click="clearFiles" class="ml-2" size="sm">Reset</b-button>
    </div>
    <div v-if="fileContentsToJson" class="d-flex justify-content-around">
      <div class="col-8">
        <b-table bordered hover responsive head-variant="light" :items="fileContentsToJson"></b-table>
      </div>
      <div class="col-4">
        <b-input type="text" v-on:keyup.enter="addCellsByInput"/>
<!--        <p>{{addCells.values()}}</p>-->
        <b-list-group>
          <b-list-group-item v-bind:key="cell" v-for="cell in addCells">
            {{ cell }}
          </b-list-group-item>
        </b-list-group>
      </div>
    </div>
  </div>
</template>

