<template>
<base-dialogue v-if="inputIsInvalid" title="Invalid Input">
  <template #default>
    <p>Unfortunately there's an invalid input</p>
  </template>
  <template v-slot:actions>
    <base-button @click="confirmError">Okay!</base-button>
  </template>
</base-dialogue>
 <base-card> 
    <form @submit.prevent="submitData">
        <div class="form-control">
            <label for="title">Title</label>
            <input type="text" name="text" id="text" 
            ref="titleInput"/>

        </div>
        <div class="form-control">
            <label for="description">Description</label>
            <textarea type="textarea" name="description" id="description" rows="3" ref="descInput"></textarea>

        </div>
        <div class="form-control">
            <label for="link">Link</label>
            <input type="url" name="link" id="link" 
            ref="linkInput"/>

        </div>
        <div>
            <base-button type="submit">Add Resource</base-button>
        </div>
    </form>     

 </base-card>
    
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';

export default{
  components: { BaseButton },
    inject: ['addResource'],
    methods: {
        submitData(){
        const enteredTitle = this.$refs.titleInput.value;
        const enteredDescription = this.$refs.descInput.value;
        const enteredLink = this.$refs.linkInput.value;

        if(enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredLink.trim === ''){
            this.inputIsInvalid = true;
            return;
        }

        this.addResource(enteredTitle,enteredDescription,enteredLink);
        },
        confirmError(){
          this.inputIsInvalid = false;
        }
    },
    data(){
      return{
        inputIsInvalid: true
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