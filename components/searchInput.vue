<template>
    <div>
        <div class="searchBar">
            <input type="text"
            v-model="userInput"
            id="userInputId"
            @keyup.enter="search"
            placeholder="Search photos">
            <button @click="search">
            Search
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'searchInput',

    data() {
        return {
            userInput: '',
            clientId: '5f39d0a9e6755434f948e418ab5ce36ae00b133409a4b988c59a633ddbe594ba'
        }
    },

    methods: {
        async search() {
            const ip = await this.$axios.$get('https://api.unsplash.com/photos/search/?query=' + 'popular' + '&client_id=' + this.clientId )

            this.$nuxt.$emit('IMAGE_DATA', ip)
        }
    }
    
}
</script>

