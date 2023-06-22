<template>
  <q-page class="flex flex-center" style="flex-direction: column">
    <UsersPage />

    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    />
    <AjaxBarDemo />
    <AvatarDemo />
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

import AjaxBarDemo from "src/components/AjaxBarDemo.vue";
import AvatarDemo from "src/components/AvatarDemo.vue";
import UsersPage from "src/pages/UsersPage.vue";

export default defineComponent({
  name: "IndexPage",
  components: { AjaxBarDemo, AvatarDemo, UsersPage },
});
</script>
