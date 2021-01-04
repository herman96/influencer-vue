<template>
    <option v-for="item in categories" :key="item.id" value="{{ item.id }}">{{ item.name }}</option>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Categories',
    data() {
        return {
            categories: [],
        }
    },
    methods: {
        getCategories() {
            axios.get('/api/categories')
                .then(response => {
                    this.categories = response.data.data;
                })
                .catch(function(error){
                    console.log(error)
                })
        },
    },
    created() {
        this.getCategories();
    }
}
</script>