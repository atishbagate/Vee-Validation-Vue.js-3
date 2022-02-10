<template>
    <div class="section m-5">
      <DynamicField />
        <h2>This is Parent Component and Send a information as a Props.</h2>
        <Child :schema="definedSchema"/>
    </div>
</template>

<script>
import Child from './Child.vue';
import * as Yup from 'yup';

import DynamicField from './DynamicField.vue';
export default {
    name:"Parent",
    components:{
        Child,
        DynamicField
    },
    data:() => {
        const definedSchema = {
                  fields: [
        {
          label: 'Your Name',
          name: 'name',
          as: 'input',
          rules: Yup.string().required(),
        },
        {
          label: 'Your Password',
          name: 'password',
          as: 'input',
          type: 'password',
          rules: Yup.string().min(6).required(),
        }, 
      ],
        };
        return{
            definedSchema
        }
    }
}
</script>
<style>

</style>