<template>
  <footer>
    <div class="container">
      <div class="row">
        <div class="col-lg-6 offset-lg-3">
          <ul class="footer d-flex flex-wrap">
            <nav-item :link="links.footer.link" classItem="footer__item">
              <img
                :src="require(`@/assets/logo/${links.footer.icon}`)"
                alt="logo"
              />
            </nav-item>

            <nav-item
              v-for="link in links.other"
              :key="link.id"
              :link="link.link"
              :text="link.text"
              classItem="footer__item"
            ></nav-item>
          </ul>
        </div>
      </div>
      <img
        class="beanslogo"
        src="@/assets/logo/Beans_logo_dark.svg"
        alt="Beans logo"
      />
    </div>
  </footer>
</template>

<script>
import NavItem from "./NavItem.vue";
export default {
  components: { NavItem },
  computed: {
    links() {
      return this.$store.getters["getFooterLinks"];
    },
  },
};
</script>
