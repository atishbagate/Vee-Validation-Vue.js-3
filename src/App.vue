<template>
  <Form @submit="onSubmit" :validation-schema="schema">
<!--    <label for="email">Your Email</label>-->
<!--    <Field id="email_addr" name="email_addr" type="email" />-->
<!--    <ErrorMessage name="email_addr" />-->

<!--    <label for="password">Your Password</label>-->
<!--    <Field id="password" name="acc_pazzword" type="password" />-->
<!--    <ErrorMessage name="acc_pazzword" />-->

    <label for="image">Your Image</label>
    <Field id="image" name="acc_image" type="file" rules="ext:jpg,png" />
    <ErrorMessage name="acc_image" />
    <button>Submit</button>
  </Form>
</template>

<script>
import { Field, Form, ErrorMessage } from "vee-validate";
import * as Yup from "yup";

export default {
  name: "App",
  components: {
    Field,
    Form,
    ErrorMessage,
  },
  setup() {
    const schema = Yup.object().shape({
      // email_addr: Yup.string().email().required().label("Email Address"),
      // acc_pazzword: Yup.string().min(5).required().label("Your Password"),
      acc_image:  Yup.mixed().required('A file is required'),
    });

    function onSubmit(values) {
      alert(JSON.stringify(values, null, 2));
    }

    return {
      schema,
      onSubmit,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

input,
label {
  display: block;
  margin-top: 20px;
}

input + span {
  display: block;
}

button {
  margin-top: 20px;
}
</style>
