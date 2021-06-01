<template>
    <div class="label">
        <div class="error">{{ error }}</div>
    </div>
    <input
        type="checkbox"
        :checked="checked"
        @click="change"
        id="terms" 
    />
    <label for="terms">Terms and condition</label>
</template>

<script>

export default{
    emits: ['change'],
    
    props:{
        // emit: ['change'],

        checked: {
            type: Boolean
        },
        error: {
            type: String
        }
    },

    created(){
        this.$emit('change', {
                value: this.checked,
                error: this.validate(this.checked)
            });
    },

    methods: {
        change($event){
            console.log('the target is ' + $event.target.checked)
            // this.checked = $event.target.checked
            this.$emit('change', {
                checked: $event.target.checked,
                error: this.validate()
            })
            console.log($event.target.checked);
        },
        validate(){

            if(this.checked === false){
                return 'Agree to the terms and conditions to continue'
            }
        }
    }
}
</script>


<style scoped>
    .error {
        color: red;
    }

    input[type=checkbox] + label {
        display: block;
        margin: 0.2em;
        cursor: pointer;
        padding: 0.2em;
    }

    input[type=checkbox] {
        display: none;
    }

    input[type=checkbox] + label:before {
        content: "\2714";
        border: 0.1em solid #000;
        border-radius: 0.2em;
        display: inline-block;
        width: 1em;
        height: 1em;
        padding-left: 0.2em;
        padding-bottom: 0.3em;
        margin-right: 0.2em;
        vertical-align: bottom;
        color: transparent;
        transition: .2s;
    }

    input[type=checkbox] + label:active:before {
        transform: scale(0);
    }

    input[type=checkbox]:checked + label:before {
        background-color: MediumSeaGreen;
        border-color: MediumSeaGreen;
        color: #fff;
    }

    input[type=checkbox]:disabled + label:before {
        transform: scale(1);
        border-color: #aaa;
    }

    input[type=checkbox]:checked:disabled + label:before {
        transform: scale(1);
        background-color: #bfb;
        border-color: #bfb;
    }
</style>