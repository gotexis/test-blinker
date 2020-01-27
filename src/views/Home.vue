<template lang="pug">
  .home.has-text-centered
    img(src="@/assets/logo.png")
    h1.title.is-size-2 Blinker
    p Blinker site makes everyone's life easier.
    br
    .d-flex.flex-justify-center
      b-field
        .control.search-box.is-clearfix
          input.input(
            placeholder="Input make, model or keyword..."
            v-model="searchInput"
            @input="messageActivated = true"
            v-on:keyup.enter="find"
          )
        .control
          button.button.is-primary(
            @click="find"
            :disabled="messageActivated && String(searchInput).length < 3"
          ) Find
    p {{ message }}
</template>

<script>

export default {
  methods: {
    find() {
      if (String(this.searchInput).length < 3) {
        this.messageActivated = true;
        return;
      }
      this.$router.push({
        name: 'search',
        query: {
          q: this.searchInput,
        },
      });
    },
  },
  data() {
    return {
      messageActivated: false,
      searchInput: '',
    };
  },
  computed: {
    message() {
      if (this.messageActivated && String(this.searchInput).length < 3) {
        return 'Input more than 3 characters';
      }
      return '';
    },
  },
};
</script>

<style lang="sass">
.search-box
  width: 500px
  @media(max-width: 500px)
    width: 100%
</style>
