<template>
  <q-page class="flex flex-center" style="flex-direction: column">
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

export default defineComponent({
  name: "IndexPage",
  components: { AjaxBarDemo, AvatarDemo },
});
</script>
