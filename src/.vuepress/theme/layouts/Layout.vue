<template>
  <v-app
    class="theme-container"
    :class="pageClasses"
    @touchstart="onTouchStart"
    @touchend="onTouchEnd"
  >
    <Header ref="header" @toggle-sidebar="toggleSidebar"></Header>

    <div class="sidebar-mask" @click="toggleSidebar(false)"></div>
    <Sidebar :items="sidebarItems" @toggle-sidebar="toggleSidebar">
      <slot name="sidebar-top" slot="top" />
      <slot name="sidebar-bottom" slot="bottom" />
    </Sidebar>

    <Home v-if="$page.frontmatter.home" />

    <Page v-else :sidebar-items="sidebarItems">
      <slot name="page-top" slot="top" />
      <slot name="page-bottom" slot="bottom" />
    </Page>
  </v-app>
</template>

<script>
import Home from "@theme/components/Home.vue";
import Page from "@theme/components/Page.vue";
import Sidebar from "@theme/components/Sidebar.vue";
import Header from "@theme/components/Header.vue";
import { resolveSidebarItems } from "../util";

export default {
  components: { Home, Page, Sidebar, Header },

  data() {
    return {
      isSidebarOpen: false,
      previousPageUrl: null,
    };
  },

  computed: {
    shouldShowSidebar() {
      const { frontmatter } = this.$page;
      return (
        !frontmatter.home &&
        frontmatter.sidebar !== false &&
        this.sidebarItems.length
      );
    },

    sidebarItems() {
      /* Fail safe, previousPage will be null if coming from external source, thus load neon for enrichments and export formats*/
      if (this.previousPageUrl === null) {
        if (
          this.$page.regularPath.includes("enrichments") ||
          this.$page.regularPath.includes("export-formats")
        ) {
          this.previousPageUrl = "/neon/";
        } else {
          this.previousPageUrl = this.$page.regularPath;
        }
      }
      console.log(this.previousPageUrl);
      return resolveSidebarItems(
        this.$page,
        this.previousPageUrl,
        this.$site,
        this.$localePath
      );
    },

    pageClasses() {
      const userPageClass = this.$page.frontmatter.pageClass;
      return [
        {
          "no-navbar": !this.shouldShowNavbar,
          "sidebar-open": this.isSidebarOpen,
          "no-sidebar": !this.shouldShowSidebar,
        },
        userPageClass,
      ];
    },
  },

  mounted() {
    this.$router.afterEach((to, from) => {
      this.isSidebarOpen = false;
      /* This part here checks from which page comes from and sets the previous url accordingly.*/
      if (from.path.includes("invisible")) {
        if (
          this.$page.regularPath.includes("enrichments") ||
          this.$page.regularPath.includes("export-formats")
        ) {
          this.previousPageUrl = "/invisible/";
        } else {
          this.previousPageUrl = to.path;
        }
      } else if (
        from.path.includes("enrichments") ||
        from.path.includes("export-formats")
      ) {
        if (
          this.$page.regularPath.includes("enrichments") ||
          this.$page.regularPath.includes("export-formats")
        ) {
          this.previousPageUrl = from.$page.previousPageUrl;
        } else {
          this.previousPageUrl = to.path;
        }
      } else {
        if (
          this.$page.regularPath.includes("enrichments") ||
          this.$page.regularPath.includes("export-formats")
        ) {
          this.previousPageUrl = "/neon/";
        } else {
          this.previousPageUrl = to.path;
        }
      }
    });
  },

  methods: {
    toggleSidebar(to) {
      this.isSidebarOpen = typeof to === "boolean" ? to : !this.isSidebarOpen;
    },

    // side swipe
    onTouchStart(e) {
      this.touchStart = {
        x: e.changedTouches[0].clientX,
        y: e.changedTouches[0].clientY,
      };
    },

    onTouchEnd(e) {
      const dx = e.changedTouches[0].clientX - this.touchStart.x;
      const dy = e.changedTouches[0].clientY - this.touchStart.y;
      if (Math.abs(dx) > Math.abs(dy) && Math.abs(dx) > 40) {
        if (dx > 0 && this.touchStart.x <= 80) {
          this.toggleSidebar(true);
        } else {
          this.toggleSidebar(false);
        }
      }
    },
  },
};
</script>

<style src="prismjs/themes/prism-tomorrow.css"></style>
