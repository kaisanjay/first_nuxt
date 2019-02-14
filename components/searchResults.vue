<template>
    <div>
        <div v-for="a in apiData" class="image-box">
            <img :src='a.urls.small'>
        </div>
        <div v-if="apiData.length === 0">
            No Results Found
        </div>
    </div>
</template>

<script>
export default {
    name: 'searchResults',
    data() {
        return {
            apiData : []

        }
    },

    created() {
        let gthis = this

        this.$nuxt.$on('IMAGE_DATA', data => {
            this.apiData = data;
        })

        console.log(this.apiData)
        console.log('fired')
    }
}
</script>

