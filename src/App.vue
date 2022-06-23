<template>
  <main>
    <InputComponent 
      label="lastname:" 
      v-model="dataToSend.lastname" 
      :errors="v$.lastname.$errors"
    />
    <InputComponent 
      label="firstname:" 
      v-model="dataToSend.firstname" 
      :errors="v$.firstname.$errors"
    />
    <InputComponent 
      label="phone number:" 
      v-model="dataToSend.phoneNumber" 
      :errors="v$.phoneNumber.$errors"
    />
    <InputComponent 
      label="email:" 
      v-model="dataToSend.email" 
      :errors="v$.email.$errors"
    />
    <div>
      <button @click="submit">submit form</button>
    </div>     
  </main>
</template>

<script>
  import { reactive } from "vue";

  import InputComponent from "./components/InputComponent.vue";
  import { helpers, required } from "@vuelidate/validators";
  import { useVuelidate } from "@vuelidate/core";
  
  export default {
    name: "App",
    components: {
      InputComponent
    },
    setup(){
      const dataToSend = reactive({
        lastname: "",
        firstname: "",
        phoneNumber: "",
        email: "",
      });

      const rules = {
        lastname: {
          required: helpers.withMessage(
            "we need your lastname",
            required
          ),
        },
        firstname: {
          required: helpers.withMessage(
            "we need your firstname",
            required
          ),
        },
        email: {
          required: helpers.withMessage(
            "we need your email",
            required
          ),
        },
        phoneNumber: {
          required: helpers.withMessage(
            "we need your phone number",
            required
          ),
        },
      }

      const v$ = useVuelidate(rules, dataToSend);
      const submit = async () => {
        const result = await v$.value.$validate();
        if(result) {
          alert("Everything is ok; your data has been saved!");
        }
        else {
          alert("Something went wrong please check if all field are filled!");
        }
      };

      return { 
        v$,
        submit,
        dataToSend
      }
    }
  }
</script>

<style>
  main {
    width: 100%;
    height: 100%;
    position: absolute;
    background: linear-gradient(10deg, rgba(223, 230, 217, 0.12), rgba(83, 33, 95, 0.12), rgb(33, 216, 137));
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

  }
  button {
    height: 50px;
    width: 400px;
    border-radius: 5px;
    font-size: 16px;
    color: white;
    margin-top: 20px;
    border: 1px solid transparent;
    background-color: rgb(129, 119, 184);
  }
</style>