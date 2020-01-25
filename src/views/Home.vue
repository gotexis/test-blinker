<template lang="pug">
  .home.has-text-centered
    img(src="@/assets/logo.png")
    h1.title.is-size-2 TUT
    p TUT site makes everyone's life easier.
    hr
    .d-flex.flex-justify-center
      b-field
        .control.search-box.is-clearfix
          input.input(
            placeholder="Input university, country, course..."
            v-model="searchInput.value"
            @input="messageActivated = true"
            v-on:keyup.enter="find"
          )
        .control
          button.button.is-primary(
            @click="find"
            :disabled="messageActivated && String(searchInput.value).length < 3"
          ) Find
    p {{ message }}
</template>

<script>
// import { CharField } from '@/utils/forms/field'

export default {
  methods: {
    find() {
      if (String(this.searchInput.value).length < 3) return (this.messageActivated = true);
      this.$router.push({
        name: 'mentor-find',
      });
    },
  },
  data() {
    return {
      messageActivated: false,
    };
  },
  computed: {
    message() {
      if (this.messageActivated && String(this.searchInput.value).length < 3) {
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
