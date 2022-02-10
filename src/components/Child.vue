<template>
  <h2>this is Child Component and Recieve Schema as Props</h2>
  <Form>
      <div class="card-body"
      v-for="{as, name, label, ...attrs} in schema.fields" :key="name">
      <label class="text-secondary" :for="name">{{  label }}</label>
      <Field  class="form-control" :as="as" :id="name" :name="name" v-bind="attrs" />
      <ErrorMessage :name="name" />
    </div>
  </Form>
</template>
<script>
import {Form,Field,ErrorMessage } from 'vee-validate'
 
export default {
    name:"Child",
    components:{
        Form,
        Field,
        ErrorMessage 
    }, 
    props: {
    schema: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style>

</style>