<template>
    <div>
        <input class="form-control search-input" type="text"
        :value="term" @input="changeHandler" placeholder="Kinolarni...">
    </div>  
</template>


<script>
export default {
    props: {
        updateTermHandler: {
            type: Function,
            required: true
        }
    },
    data(){
        return {
            term: '',
        }
    },
    methods: {
        changeHandler(e){
            this.term = e.target.value,
            this.updateTermHandler(this.term)
        }  
    },
}
</script>

<style scoped>
.search-input {
    margin-bottom: 1rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15)  
}
</style>