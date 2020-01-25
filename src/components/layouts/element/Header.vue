<template lang="pug">
  nav.navbar.has-shadow(role='navigation', aria-label='main navigation')
    .navbar-brand
      router-link.navbar-item(:to="{name: 'index'}")
        img(src='@/assets/img/logo/tut-logo.png', width='112', height='28')
      a.navbar-burger.burger(role='button' :class="[active ? 'is-active' : null]")
        span(aria-hidden='true')
        span(aria-hidden='true')
        span(aria-hidden='true')
    .navbar-menu
      .navbar-start
        router-link.navbar-item(:to="{name: 'map'}")
          | {{ 'SiteMap (Dev)' }}
      .navbar-end
        a.navbar-item(@click.prevent='switchLang')
          b-icon.mr-5(icon="earth")
          |
          | {{ 'switch' }}
        .navbar-item
          .tags.has-addons
            span.tag Mode
            span.tag.is-warning TUT Site
        .navbar-item
          .buttons
            router-link.button.is-primary(:to="{name: isAuthenticated ? 'my-account' : 'auth'}")
              strong {{ isAuthenticated ? 'Profile' : 'Sign in'}}
</template>

<script>
import GithubIcon from 'vue-ionicons/dist/logo-github.vue';
import TwitterIcon from 'vue-ionicons/dist/logo-twitter.vue';
import WechatIcon from 'vue-material-design-icons/Wechat.vue';

export default {
  data() {
    return {
      active: false,
      GithubIcon,
      TwitterIcon,
      WechatIcon,
    };
  },
};
</script>

<style lang="sass" scoped>
  .mr-5
    margin-right: 5px !important
</style>
