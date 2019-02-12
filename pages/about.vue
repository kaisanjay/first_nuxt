<template>
    <div>
        <h1>about</h1>
        <div v-for='i in ip'>
            {{i.id}}
            <img :src='i.urls.regular' class="image-box">
        </div>
    </div>
</template>

<style lang="sass">
.image-box
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2)
    transition: 0.3s
    width: 30%
    border-radius: 5px
    padding: 1rem 3rem
    padding-bottom: 4rem
    margin-top: 2.5rem
    border-top-style: dashed
    border-width: 2px
    border-color: grey
    &:hover
        box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2)
    &--content
        margin-top: 2%

</style>



<script>
export default {
    data() {
        return {

        }
    },

    async asyncData({ $axios }) {
        const ip = await $axios.$get('https://api.unsplash.com/photos/search/?query=about&client_id=5f39d0a9e6755434f948e418ab5ce36ae00b133409a4b988c59a633ddbe594ba')
        return { ip }
    },

    methods: {}
}
</script>

