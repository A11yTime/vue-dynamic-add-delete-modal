<template>
   <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
   <template #default>
      <p>Unfortunate, at least one input value is invalid</p>
      <p>Please check all inputs and make sure you enter at least some character on each input field</p>
   </template>
   <template #actions > 
     <base-button @click="confirmError" ref="btn">Okay</base-button>
   </template>

  </base-dialog>
    <base-card>
<form @submit.prevent="submitData">
    <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput"/>
    </div>
    <div class="form-control">
        <label for="description">Description</label>
        <textarea name="description" id="description" rows="3" ref="desInput"></textarea>
    </div>
    <div class="form-control">
        <label for="link">link</label>
        <input id="link" name="link" type="url" ref="linkInput"/>
    </div>
    <div>
        <base-button type="submit">Add Resource</base-button>
    </div>
</form>

</base-card>
</template>
 
<script>
export default{
       data(){
        return{
          inputIsInvalid: false,
        }
       },
      inject: ['addResource', 'focusOnEditButton'],
      methods: {
        submitData(){
          const enterTitle = this.$refs.titleInput.value;
          const eneterDesc = this.$refs.desInput.value;
          const enterUrl = this.$refs.linkInput.value;

          if(enterTitle.trim() === '' || 
          eneterDesc.trim() === '' ||
          enterUrl.trim() === ''
          ){
            this.inputIsInvalid = true;
         
            return;
            

          }

          this.addResource(enterTitle,eneterDesc, enterUrl);
          
        },
        confirmError(){
          this.inputIsInvalid = false
         }
       }
      }
      

</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>