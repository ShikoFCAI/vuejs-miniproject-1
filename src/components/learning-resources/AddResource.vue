<template>
    <base-dialogue v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
        <template #main>
            <p> Invalid Input was entered </p>  
            <p> Please try again. </p>  
        </template>
        <template #actions>
            <base-button @click="confirmError"> 
                Okay
            </base-button>  
        </template>
    </base-dialogue>
    <base-card> 
        <form @submit.prevent="onSubmit">
            <h2> Add Resource </h2>
            <div>
                <label> Title </label>
                <input type="text" id="title" name="title" v-model="titleInput"/>
            </div>
            <div>
                <label> Description </label>
                <textarea type="text" id="Description" name="Description" rows="3" v-model="descInput"/>
            </div>
            <div>
                <label> Link </label>
                <input type="url" id="Link" name="Link" v-model="linkInput"/>
            </div>
            <base-button> Add Resource </base-button> 
        </form>
    </base-card>
</template>


<script>
import BaseCard from '../UI/BaseCard.vue';
export default {
    inject: ['addResource'],
    data() {
        return {
            titleInput: "",
            descInput: "",
            linkInput: "",
            inputIsInvalid: false,
        };
    },
    components: {
         BaseCard
    },
    methods: {
        onSubmit(){
            if (this.titleInput.trim() === '' || this.descInput.trim() === '' || this.linkInput.trim() === ''){
                this.inputIsInvalid = true;
                return;
            }

            this.addResource(this.titleInput, this.descInput, this.linkInput);
        },
        confirmError(){
            this.inputIsInvalid = false;
        },
    },
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