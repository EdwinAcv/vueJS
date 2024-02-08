
<template>
    <div>
        <div>
            <h2 >{{ tittle || customTittle }}</h2>
            <p> {{ counter }} <sup>2</sup> = {{ squereCounter }} </p>
        </div>

        <div>
            <button @:click='increase'>+1</button>
            <button @:click='decrease'>-1</button>
        </div>

    </div>
</template>

<script>
export default {

    props: {
        tittle: String,
        start: {
            type: Number,
            default: 10
        }
    }  ,
    // name: 'Patito'
    data(){
        return {
            counter: this.start
        }
    },

    methods: {
        increase(){
            this.counter ++
        },
        decrease(){
            this.counter --
        }
    },
    computed: {
        squereCounter(){
            return this.counter * this.counter;
        },
        customTittle(){
            return 'Counter';
        }
    }
}
</script>

<style>
    button {
        background-color: #64b687;
        border-radius: 5px;
        border: 1px solid white;
        color: white;
        cursor: pointer;
        margin: 0 5px;
        padding: 5px 15px;
        transition: 0.3s ease-in-out;
    }

    button:hover {
        background-color: #5aa67b;
        transition: 0.3s ease-in-out;
    }
</style>
