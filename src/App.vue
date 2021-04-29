<template>
  <v-container fluid fill-height>
    <v-row class="justify-center align-center">
      <v-col cols="12" sm="4">
        <v-card>
          <v-card-title
            >Please Enter a GQL query copied from chrome network
            Tab</v-card-title
          >
        </v-card>
        <v-text-field v-model="enteredValue" :clearable="true"></v-text-field>
        <v-btn @click="process(enteredValue)">Convert</v-btn>

        <v-card v-if="output !== ''">
          <v-card-text>
            <div>{{ output }}</div></v-card-text
          >
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
 

<script>
export default {
  name: "App",
  data() {
    return {
      enteredValue: "",
      output: "",
    };
  },
  methods: {
    process(value) {
      let string = JSON.stringify(value);
      // prettier-ignore
      string = string.substring(string.lastIndexOf("query"), string.length - 3).replace(/\\n/g, "").replace(/__typename/g, "").replace(/\\/g, "");
      this.output = string;
    },
  },
};
</script>
