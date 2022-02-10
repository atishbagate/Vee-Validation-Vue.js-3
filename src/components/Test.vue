<template>
  <Form @submit="onSubmit">
    <!-- 1 image  -->
    <div class="col-md-6 offset-md-3 ">
      <label for="input">1) Insert Image</label>
      <Field
        name="input"
        class="form-control"
        type="file"
        rules="required|image"
      />
      <!--        <span>{{ errors.input }}</span>-->
      <ErrorMessage class="text-danger" name="input" />
    </div>
    <!-- 2 Email  -->
    <div class="col-md-6 offset-md-3 ">
      <label for="email">2) Insert Email</label>
      <Field class="form-control" name="email" rules="required|email" />
      <!--        <span>{{ errors.email }}</span>-->
      <ErrorMessage class="text-danger" name="email" />
    </div>
    <!-- 3) Insert the File -->
    <div class="col-md-6 offset-md-3 ">
      <label for="doc">3) Insert the File</label>
      <Field
        name="doc"
        class="form-control"
        type="file"
        rules="required|mimes:application/vnd.openxmlformats-officedocument.wordprocessingml.document"
      />
      <!--        <span>{{ errors.email }}</span>-->
      <ErrorMessage class="text-danger" name="doc" />
      <br />
      <br />
    </div>
    <br />
    <br />
    <!-- 1) Insert the File -->
    <!-- custom input field  -->
    <div class="col-md-6 offset-md-3">
      <div class="form-group" v-for="(input, k) in inputs" :key="k">
        <label :for="`inputs[${k}].name`">1) Insert Email</label>
        <Field
          :name="`inputs[${k}].name`"
          type="email"
          class="form-control"
          v-bind="input.name"
          rules="required|email"
        />
        <span>
          <button
            type="button"
            class="btn btn-outline-light text-dark"
            @click="add(k)"
            v-show="k == inputs.length - 1 && inputs.length < 3"
          >
            add
          </button>
          <button
            type="button"
            class="btn btn-outline-light text-dark"
            @click="remove(k)"
            v-show="k || (!k && inputs.length > 1)"
          >
            remove
          </button>
        </span>
        <ErrorMessage class="text-danger" :name="`inputs[${k}].name`" />
        <!-- <span class="error"> {{errors[`name`]?.split(".")[1] }}</span> -->
      </div>
    </div>
    <!-- 2) Insert the File -->
    <div class="col-md-6 offset-md-3">
      <div class="form-group" v-for="(file, k) in files" :key="k">
        <label :for="`files[${k}].file`">2) Insert File</label>
        <Field
          :name="`files[${k}].file`"
          type="file"
          class="form-control"
          v-bind="file.file"
          rules="required|mimes:application/vnd.openxmlformats-officedocument.wordprocessingml.document"
        />
        <span>
          <button
            type="button"
            class="btn btn-outline-light text-dark"
            @click="addFile(k)"
            v-show="k == files.length - 1 && files.length < 3"
          >
            add
          </button>
          <button
            type="button"
            class="btn btn-outline-light text-dark"
            @click="removeFile(k)"
            v-show="k || (!k && files.length > 1)"
          >
            remove
          </button>
        </span>
        <ErrorMessage class="text-danger" :name="`files[${k}].file`" />
      </div>
    </div>
    <!-- 3) Insert Image -->
    <div class="col-md-6 offset-md-3">
      <div class="form-group" v-for="(image, k) in images" :key="k">
        <label :for="`images[${k}].image`">3) Insert Image</label>
        <Field
          :name="`images[${k}].image`"
          type="file"
          class="form-control"
          v-bind="images.image"
          rules="required|image"
        />
        <span>
          <button
            type="button"
            class="btn btn-outline-light text-dark"
            @click="addImage(k)"
            v-show="k == images.length - 1 && images.length < 3"
          >
            add
          </button>
          <button
            type="button"
            class="btn btn-outline-light text-dark"
            @click="removeImage(k)"
            v-show="k || (!k && images.length > 1)"
          >
            remove
          </button>
        </span>
        <ErrorMessage class="text-danger" :name="`images[${k}].image`" />
      </div>
    </div>
    <br />
    <br />
    <!-- 1) Enter Your Details-->
    <div class="col-md-6 offset-m-3" style="margin:0px auto">
      <div class="form-group card" v-for="(card, k) in cards" :key="k">
        <div class="card-header"><h2>1) Enter Your Details</h2></div>
        <div class="card-body">
          <label>Insert name</label>
          <Field
            :name="`cards[${k}].name`"
            type="text"
            class="form-control"
            v-bind="card.name"
            rules="required|alpha"
          />
          <ErrorMessage class="text-danger" :name="`cards[${k}].name`" />
          <br />
          <label>insert Image</label>
          <Field
            :name="`cards[${k}].file`"
            type="file"
            class="form-control"
            v-bind="card.file"
            rules="required|image"
          />
          <ErrorMessage class="text-danger" :name="`cards[${k}].file`" />
          <br />
          <span>
            <button
              type="button"
              class="btn btn-outline-primary mr-2"
              @click="addCard(k)"
              v-show="k == cards.length - 1 && cards.length < 3"
            >
              add
            </button>
            <button
              type="button"
              class="btn btn-outline-warning"
              @click="removeCard(k)"
              v-show="k || (!k && card.length > 1)"
            >
              remove
            </button>
          </span>
        </div>
        <div class="card-footer">
          <h5>verify the Details entered above the Card.</h5>
        </div>
      </div>
    </div>

    <div class="col-md-6 offset-md-3">
      <input type="submit" class="btn btn-primary" value="Submit" />
    </div>
  </Form>
  <Parent class="card" />
</template>

<script>
import { Form, Field, ErrorMessage, defineRule, configure } from "vee-validate";
import * as rules from "@vee-validate/rules";
import { localize } from "@vee-validate/i18n";

import Parent from "./Parent.vue";
import { onMounted } from "@vue/runtime-core";

// defineRule('alpha', rules.alpha);
// this is to re define the configuration in vee validation

// Install all rules
Object.keys(rules).forEach((rule) => {
  defineRule(rule, rules[rule]);
});
export default {
  name: "Test",
  components: {
    Form,
    Field,
    ErrorMessage,
    Parent,
  },
  // defining data for input field
  data() {
    return {
      inputs: [
        {
          name: "",
        },
      ],
      files: [
        {
          file: "",
        },
        {
          email: "",
        },
      ],
      images: [
        {
          image: "",
        },
      ],
      cards: [
        {
          name: "",
          file: "",
        },
      ],
    };
  },

  methods: {
    onSubmit(values) {
      console.log(values);
      alert(JSON.stringify(values, null, 2));
    },
    // methods for input value
    add(index) {
      console.log(`email added on position : ${index}`);
      this.inputs.push({ name: "" });
    },
    remove(index) {
      console.log(`email removed on position : ${index}`);
      this.inputs.splice(index, 1);
    },
    //methods for adding Files
    addFile(index) {
      console.log(`File added on position : ${index}`);
      this.files.push(index);
    },
    removeFile(index) {
      console.log(`File removed on position : ${index}`);
      this.files.splice(index, 1);
    },
    //methods for adding Images
    addImage(index) {
      console.log(`Image added on position : ${index}`);
      this.images.push(index);
    },
    removeImage(index) {
      console.log(`Image removed on position : ${index}`);
      this.images.splice(index, 1);
    },
    //methods to add and remove card
    addCard(index) {
      console.log(`card added on position ${index}`);
      this.cards.push(index);
    },
    removeCard(index) {
      console.log(`card is removed on position ${index}`);
      this.cards.splice(index, 1);
    },
  },
  setup() {
    onMounted(() => {
      // to define the rule and its custom name
      defineRule("required", rules.required);
      configure({
        // Generates an English message locale generator
        generateMessage: localize("en", {
          messages: {
            required: "This field is requireds",
          },
        }),
        validateOnInput: true,
        //    validateOnModelUpdate: true,
      });
    });
  },
};
</script>

<style scoped></style>
