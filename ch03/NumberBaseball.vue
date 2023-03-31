<template>
    <div>
        <h1>{{result}}</h1>
        <form v-on:submit="onSubmitForm">
            <input ref="answer" maxlength="4" v-model="value">
            <button>입력</button>
        </form>
        <div>시도: {{  }}</div>
    </div>
</template>

<script>
    const getNumbers = () => {
        const candidates = [1, 2, 3, 4, 5, 6, 7, 8, 9];
        const array = [];

        for(let i = 0; i < 4; ++i){
            const chosen = candidates.splice(Math.random());
        }

    }



    export default {
        data(){
            return{
                value: '',
                result: ''
            }
        }, 
        methods: {

            onSubmitForm(e){
                e.preventDefault();
            }
        }
    };
</script>

<style>

</style>
