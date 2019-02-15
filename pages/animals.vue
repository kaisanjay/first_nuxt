<template>
  <div>
    <div class="hero">
			<div class="searchBar">
        <input
          type="text"
          v-model="userInput"
          id="userInputId"
          @keyup.enter="search"
          placeholder="Search photos"
        >
        <button @click="search">Search</button>
      </div>
    </div>
    <div class="tabs">
      <nuxt-link class="format-anchor" to="/popular">
        <button class="tabs__btn" id="popular-tab">Popular</button>
      </nuxt-link>
      <nuxt-link class="format-anchor" to="/nature">
        <button class="tabs__btn" id="nature-tab">Nature</button>
      </nuxt-link>

      <nuxt-link class="format-anchor" to="/animals">
        <button class="tabs__btn" id="animals-tab">Animals</button>
      </nuxt-link>
    </div>

    <div v-for="i in ip" class="image-box" :key="i.id">
      <img :src="i.urls.small">
    </div>
  </div>
</template>

<script>
export default {
	data() {
    return {
      userInput: '',
      clientId: '5f39d0a9e6755434f948e418ab5ce36ae00b133409a4b988c59a633ddbe594ba'
    }
  },

  async asyncData({ $axios }) {
    const ip = await $axios.$get(
      "https://api.unsplash.com/photos/search/?query=animals&client_id=5f39d0a9e6755434f948e418ab5ce36ae00b133409a4b988c59a633ddbe594ba"
    );
    return { ip };
  },

  mounted() {
    document.getElementById("animals-tab").classList.add("tabs__active");
	},
	
	methods: {
		async search() {
      document.querySelectorAll('.tabs__btn').forEach((el) => {
          el.classList.remove('tabs__active');
      })

      const ip = await this.$axios.$get('https://api.unsplash.com/photos/search/?query=' + this.userInput + '&client_id=' + this.clientId )
      this.ip = ip
    },
	}
};
</script>

<style lang="sass">
@import '~/assets/main.sass'

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


