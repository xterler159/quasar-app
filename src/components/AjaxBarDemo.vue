<template>
  <q-ajax-bar ref="ajaxBar" color="accent" size="10px" skip-hijack />
  <button @click="triggerAjaxBar">trigger ajaxbar</button>
</template>

<script>
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "IndexPage",
  setup() {
    const ajaxBar = ref(null);

    const triggerAjaxBar = () => {
      const ajaxBarRef = ajaxBar.value;
      ajaxBarRef.start();

      setTimeout(() => {
        if (ajaxBarRef) {
          ajaxBarRef.stop();
        }
      }, 5000);
    };

    return {
      ajaxBar,
      triggerAjaxBar,
    };
  },
});
</script>
