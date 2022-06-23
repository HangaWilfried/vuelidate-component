<template>
    <div class="block">
        <label for="">{{label}}</label>
        <input 
            type="text" 
            :value="modelValue"
            @input="$emit('update:modelValue', $event.target.value)" 
        />
        <div class="error" v-for="error of errors" :key="error.$uid">
            {{ error.$message }}
        </div>   
    </div>

</template>
<script>
    export default{
        name: "InputComponent",
        emit: ["update:modelValue"],
        props: {
            label: {
                type: String,
                required: true,
            },
            modelValue: {
                required: true,
            },
             errors: {
                type: Object,
                required: true,
            },
        }
    }
</script>

<style>
    .block{
        display: flex;
        flex-direction: column;
        padding: 12px 20px;
        gap: 4px;
    }
    input {
        height: 35px;
        width: 400px;
        border-radius: 5px;
        border: 1px solid transparent;
    }
    .error {
        color: red;
        font-size: 14px;
    }
</style>