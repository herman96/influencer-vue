<template>
    <option v-if="item in socialNetworks" :key="item.id" value="{{ item.id }}">{{ item.name }}</option>
</template>

<script>
import axios from 'axios'

export default {
    name: 'SocialNetworks',
    data() {
        return {
            socialnetworks: [],
        }
    },
    methods: {
        getSocialNetworks() {
            axios.get('/api/social-networks')
                .then(response => {
                    this.socialnetworks = response.data.data;
                })
                .catch(function(error){
                    console.log(error)
                })
        }
    },
    created() {
        this.getSocialNetworks();
    },
}

</script>
  