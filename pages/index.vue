<template>
  <div>
    <searchInput></searchInput>

    <div class="hero">
      <div class="searchBar">
        <input type="text"
        v-model="userInput"
        id="userInputId"
        placeholder="Search Photos"
        @keyup.enter="search">
        <button @click="search">Search</button>
      </div>
    </div>
    <div class="tabs">
      <button class="tabs__btn" @click="showTab"  id="popular-tab">Popular</button>
      <button class="tabs__btn" @click="showTab" >Nature</button>
      <button class="tabs__btn" @click="showTab" >Animals</button>
    </div>

    <searchResults></searchResults>

    <!-- <div v-for='i in ip' class="image-box">
      <img :src='i.urls.small'>
      <div class="image-box--content">
        <h4><b>Photographer:&nbsp;&nbsp;{{ i.user.first_name }}</b></h4>
        <p><b>Total likes:</b>&nbsp;&nbsp;{{ i.user.total_likes }}</p>
        <p><b>Location:</b>&nbsp;&nbsp;{{ i.user.location }}</p>
      </div>
    </div>
    <div v-if="ip.length === 0">
      No Results Found
    </div> -->
  </div>
</template>

<script>
import searchInput from '~/components/searchInput.vue'
import searchResults from '~/components/searchResults.vue'


export default {
  components: {
    searchInput,
    searchResults
  },
  data() {
    return {
      userInput: '',
      clientId: '5f39d0a9e6755434f948e418ab5ce36ae00b133409a4b988c59a633ddbe594ba'
    }
  },

  async asyncData({ $axios }) {
    const ip = await $axios.$get('https://api.unsplash.com/photos/search/?query=popular&client_id=5f39d0a9e6755434f948e418ab5ce36ae00b133409a4b988c59a633ddbe594ba')
    return { ip }
  },

  mounted() {
    document.getElementById('popular-tab').classList.add('tabs__active')
  },

  methods: {
    async search() {
      const ip = await this.$axios.$get('https://api.unsplash.com/photos/search/?query=' + this.userInput + '&client_id=' + this.clientId )
      this.ip = ip
      console.log(ip)
    },

    async showTab(event) {
      document.querySelectorAll('.tabs__btn').forEach((el) => {
          el.classList.remove('tabs__active');
      })
      event.target.classList.add('tabs__active')

      let query = event.currentTarget.textContent
      const ip = await this.$axios.$get('https://api.unsplash.com/photos/search/?query=' + query + '&client_id=' + this.clientId )
      this.ip = ip

      this.$nuxt.$emit('IMAGE_DATA', ip)

    }
  }

}
</script>

<style lang="sass">
.hero
  margin-top: 2%
  background-color: #B2B2B2
  width: 100%
  height: 200px
  padding-bottom: 0
  color: white
  clip-path: polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%)

.image-box
  display: block
  margin: 0 auto
  margin-top: 4%
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2)
  transition: 0.3s
  width: max-content !important
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

.searchBar
  padding-top: 4.5%
  display: flex
  justify-content: center
  input, button
    padding: 0.7em 1em
    font-size: 1rem
    font-weight: bold
    outline: none
    border: none
    border: 2px solid grey
    border-right: 0
  input
    width: 60%
    border-top-left-radius: 5px
    border-bottom-left-radius: 5px
  button
    cursor: pointer
    border-top-right-radius: 5px
    border-bottom-right-radius: 5px
    transition: all 0.4s
    background-color: #7F44D3 !important
    color: white !important
    border: 2px solid #7F44D3 !important
    &:hover
      background-color: white !important
      color: #7F44D3 !important

.tabs
  display: flex
  justify-content: center
  margin-bottom: 4%
  &__btn
    display: block
    font-size: 1.3em
    cursor: pointer
    padding: 12px 16px
    font-weight: bold
    outline: 0
    border: none
    border-bottom: 2px solid transparent
    background-color: transparent
    &:hover
      border-bottom: 2px solid #cccccc

.tabs__active
  font-weight: 900
  color: #7F44D3
  border-bottom: 2px solid #7F44D3
  &:hover
    border-bottom: 2px solid #7F44D3
</style>

