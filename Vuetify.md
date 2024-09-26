# Vuetify
## v-form
```vue
<template>
  <v-sheet class="mx-auto" width="300">
    <v-form ref="form">
      <v-text-field
        v-model="name"
        ref="name"
        :counter="10"
        :rules="[
          v => !!v || 'Name is required',
          v => (v && v.length <= 10) || 'Name must be 10 characters or less',
          checkbox || 'Check is required'
        ]"
        label="Name"
        required
      ></v-text-field>
      <v-checkbox
        v-model="checkbox"
        :rules="[v => !!v || 'You must agree to continue!']"
        label="Do you agree?"
        required
      ></v-checkbox>
      <div class="d-flex flex-column">
        <v-btn
          class="mt-4"
          color="success"
          block
          @click="validate"
        >
          Validate
        </v-btn>
        <v-btn
          class="mt-4"
          color="success"
          block
          @click="$refs.name.validate(true)"
        >
          Name validate pass
        </v-btn>
      </div>
    </v-form>
  </v-sheet>
</template>

<script>
export default {
  data: () => ({
    name: '',
    checkbox: false
  }),
  methods: {
    async validate () {
        const result = await this.$refs.form.validate()
        if (result.valid) alert('Form is valid')
    }
  }
}
</script>
```
