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
        <v-btn @click="process(enteredValue)"
          >Click Me to Make Your Life Easier</v-btn
        >

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
      // let string = {"operationName":"getSubscriptions","variables":{},"query":"query getSubscriptions {\n  getSubscriptions(\n    filter: {tenant_id: \"5f335bf8a3cedf00018d442e\", rate_plan_type: staas}\n    pagination: {limit: 10, offset: 0, order_by: desc, sort_by: \"created_at\"}\n  ) {\n    Subscriptions {\n      id\n      name\n      tenant_id\n      zone {\n        name\n        __typename\n      }\n      rate_plans_staas {\n        service_level {\n          name\n          __typename\n        }\n        commitment_gib\n        start_date\n        end_date\n        term_length\n        __typename\n      }\n      created_at\n      __typename\n    }\n    pagination_result {\n      limit\n      offset\n      returned_records\n      total_records\n      __typename\n    }\n    __typename\n  }\n}\n"}
      let string = JSON.stringify(value);
      string = string
        .substring(string.lastIndexOf("query"), string.length - 3)
        .replace(/\\n/g, "")
        .replace(/__typename/g, "")
        .replace(/\\/g, "");
      this.output = string;
    },
  },
};
</script>
