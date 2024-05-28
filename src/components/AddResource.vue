<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
        <template #default>
            <p>Unfortunately, at least one input value is invalid.</p>
            <p>Please check all input and make sure your enter at least a few character into each input field</p>
        </template>
        <template #actions>
            <base-button @click="confirmError">Okay</base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="">Title</label>
                <input type="text" name="title" id="title" ref="inputTitle">
            </div>
            <div class="form-control">
                <label for="">Description</label>
                <textarea name="description" id="description" rows="3" ref="inputDescription"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="link" name="link" id="link" ref="inputLink">
            </div>
            <div>
                <base-button type="submit">Add Resource</base-button>
            </div>
            

        </form>
    </base-card>
</template>

<script>
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  components: { BaseDialog },
    inject:['addResource'],
    data() {
        return {
            inputIsInvalid: false,
        }
    },
    methods: {
        submitData() {
            const enteredTitle = this.$refs.inputTitle.value;
            const enteredDescription = this.$refs.inputDescription.value;
            const enteredLink = this.$refs.inputLink.value;

            if(enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredLink === '') {
                this.inputIsInvalid = true;
                return;
            }
            this.addResource(enteredTitle, enteredDescription, enteredLink);
        },
        confirmError() {
            this.inputIsInvalid = false;
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