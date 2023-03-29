<template>
    <div>
      <template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="6" md="4">
        <v-card>
          <v-card-title>Add New API</v-card-title>
          <v-card-text>
            <v-form ref="form" @submit.prevent="submitForm">
              <v-text-field
                label="API Name"
                v-model="apiName"
                :rules="[requiredRule]"
                required
              ></v-text-field>
              <v-text-field
                label="API URL"
                v-model="apiUrl"
                :rules="[requiredRule]"
                required
              ></v-text-field>
              <v-btn type="submit" color="primary">Add API</v-btn>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        apiName: "",
        apiUrl: "",
        requiredRule: (value) => !!value || "This field is required",
      };
    },
 
  methods: {
    async submitForm() {
      if (this.$refs.form.validate()) {
        // Call your API to add the new API data
        try {
          const response = await this.$http.post("/your-api-endpoint", {
            name: this.apiName,
            url: this.apiUrl,
          });

          if (response.status === 200) {
            // Handle successful API addition
            this.$refs.form.reset();
            this.$router.push("/your-success-page");
          } else {
            // Handle errors
            console.error("Error adding API:", response);
          }
        } catch (error) {
          console.error("Error adding API:", error);
        }
      }
    },
  },
};

  </script>
  
  <style scoped>
  /* Your CSS styles go here */
  </style>