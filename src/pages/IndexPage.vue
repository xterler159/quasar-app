<template>
  <q-page class="flex flex-center" style="flex-direction: column">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    />
    <AjaxBarDemo />
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

import AjaxBarDemo from "src/components/AjaxBarDemo.vue";

export default defineComponent({
  name: "IndexPage",
  components: { AjaxBarDemo },
});
</script>
