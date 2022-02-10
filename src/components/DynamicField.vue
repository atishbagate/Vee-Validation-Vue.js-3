<template>
  <h2>this is Dynamic Field Form</h2>
  <Form v-slot="{ errors,values }" @submit="handleSubmit">
  <div class="card">
      <label>Name</label>
      <Field as="input" name="group-name" type="text" class="form-control" rules="required|min:8" />
  </div>
  <div class="card">
      <label>Members</label>
      <Field type="text" class="form-control mb-2" name="name" rules="required|min:8" />
      <Field type="email" class="form-control" name="email" rules="required|email" />
  </div>
  <div>
      <button class="btn btn-primary mr-2" type="submit">Submit</button>
      <button class="btn btn-secondary">Add Member</button>
  </div>
        <div class="card">
        <h2>validation information</h2>
        <pre>{{ values }}</pre>
        <h2>Error information</h2>
        <h2>{{ errors }}</h2>
        </div>
</Form>
<br><br><br>
</template>

<script>
import { onMounted,defineComponent } from 'vue'
import {configure ,Form,Field, defineRule} from 'vee-validate'
import {required,email,min}  from '@vee-validate/rules'
import { localize } from '@vee-validate/i18n';
export default defineComponent({
    name:"DynamicField",
    components:{
         Form,Field
    },
    // composition API approach 
    setup(){
        const handleSubmit = (values) => {
            console.log(values);
        };
        onMounted(()=>{
                configure({
                generateMessage:localize('en',{
                    messages:{
                        required: "this is important value to add."
                    }
                }),
                // validateOnChange: true,
                // validateOnInput: true,
                validateOnModelUpdate: true,
            });
            defineRule("required",required);
            defineRule("min",min);
            defineRule("email",email);

        })
        return{
            handleSubmit,
        }
    }

});
</script>

<style>

</style>