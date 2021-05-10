<!-- FORM UTILIZZATO PER LA COACH REGISTRATION -->

<template>
   <form @submit.prevent='submitForm'>
      <div class='form-control' :class="{invalid: !firstName.isValid}">
         <label for="firstname" > FirstName </label>
         <input type='text' id='firstname' v-model='firstName.val' @blur="clearValidity('firstName')"/>
         <p v-if='!firstName.isValid'> Firstname empty. Uguale per tutti log </p>
      </div>
      <div class='form-control' :class="{invalid: !lastName.isValid}">
         <label for="lastname"> LastName </label>
         <input type='text' id='lastname' v-model='lastName.val' @blur="clearValidity('lastName')"/>
      </div>
      <div class='form-control'>
         <label for="description"> Description </label>
         <textarea type='text' id='description' row='5' v-model='description.val' :class="{invalid: !description.isValid}"> </textarea>
      </div>
      <div class='form-control'>
         <label for="rate"> Hourly rate </label>
         <textarea type='number' id='rate' row='5' v-model.number='rate.val' :class="{invalid: !rate.isValid}"> </textarea>
      </div>
      <div class='form-control' :class="{invalid: !areas.isValid}">
         <h3> Area of experties </h3>
         <div>
            <input type='checkbox' id='frontend' value='frontend' v-model='areas.val'>
            <label for='frontend'> Frontend </label>
         </div>
         <div>
            <input type='checkbox' id='backend' value='backend' v-model='areas.val'>
            <label for='backend'> Backend </label>
         </div>
         <div>
            <input type='checkbox' id='career' value='career' v-model='areas.val'>
            <label for='career'> Career </label>
         </div>
         <p v-if='!formIsValidate'> Please fix the error</p>
         <base-button> Register </base-button>
      </div>
   </form>
</template>

<script>
   export default {
      emits: ['save-data'],
      data(){
         return {
            firstName: {
               val: '',
               isValid: true
            },
            lastName: {
               val: '',
               isValid: true
            },
            description: {
               val: '',
               isValid: true
            },
            rate:{
               val: '',
               isValid: true
            },
            areas: {
               val: [],
               isValid: true
            },
            formIsValidate: true,
         }
      },
      methods: {
         clearValidity(input) {
            this[input].isValid = true;
         },
         validateForm(){
           this.formIsValidate = true;
           if(this.firstName.val === ''){
              this.firstName.isValid = false;
              this.formIsValidate = false;
           }
            if(this.lastName.val === ''){
               this.lastName.isValid = false;
               this.formIsValidate = false;
            }
            if(this.rate.val < 0 || !this.rate){
               this.rate.isValid = false;
               this.formIsValidate = false;
            }
            if(this.description.val === ''){
               this.description.isValid = false;
               this.formIsValidate = false;
            }
            if(this.areas.val.length === 0){
               this.areas.isValid = false;
               this.formIsValidate = false;
            }
         },
         submitForm() {
            this.validateForm();
            if(!this.formIsValidate){
               return ;
            }
            const formData = {
               first: this.firstName.val,
               last: this.lastName.val,
               desc: this.description.val,
               rate: this.rate.val,
               areas: this.areas.val,
            }

            this.$emit('save-data',formData); //passo il form al component padre
         }
      }
   }
</script>


<style>
.form-control {
   margin: 0.5rem 0;
}

label {
   font-weight: bold;
   display: block;
   margin-bottom: 0.5rem;
}

input[type='checkbox'] + label {
   font-weight: normal;
   display: inline;
   margin: 0 0 0 0.5rem;
}

input,
textarea {
   display: block;
   width: 100%;
   border: 1px solid #ccc;
   font: inherit;
}

input:focus,
textarea:focus {
   background-color: #f0e6fd;
   outline: none;
   border-color: #3d008d;
}

input[type='checkbox'] {
   display: inline;
   width: auto;
   border: none;
}

input[type='checkbox']:focus {
   outline: #3d008d solid 1px;
}

h3 {
   margin: 0.5rem 0;
   font-size: 1rem;
}

.invalid label {
   color: red;
}

.invalid input,
.invalid textarea {
   border: 1px solid red;
}
</style>
