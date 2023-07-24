<template lang="pug">
div
  v-bottom-navigation(
    fixed
    shift
    class="navigation"
    v-model="value"
    grow
  )
    v-btn(
      v-for="item in buttons" 
      :key="item.id"
      @click="$router.push(item.link)"
    )
      span {{ item.span }}
      v-icon mdi-{{ item.icon }}
    v-btn(@click="pushSupport")
      span Support
      v-icon mdi-lifebuoy
</template>

<script>
export default {
  name: "TheBottomNavigation",
  data() {
    return {
      value: null,
      profileIcon: null,
      buttons: [
        {
          span: "Home",
          icon: "home",
          link: "/",
        },
        // {
        //   span: "Projects",
        //   icon: "semantic-web",
        //   link: "#projects",
        // },
      ],
    };
  },
  watch: {
    user() {
      this.changeProfileIcon();
    },
  },
  methods: {
    pushSupport() {
      window.scrollTo(0, document.body.scrollHeight);
    },
  },
};
</script>

<style scoped lang="scss">
.navigation {
  z-index: 120;
  display: none;
}

@media screen and (max-width: 1142px) {
  .navigation {
    display: flex;
  }
}
</style>
