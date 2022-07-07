<template>
  <div class="about">
    <Calcu />
  </div>
</template>
<style scoped>
.about {
  background-color: cornflowerblue;
  min-height: 800px;
}
</style>

<script>
import Calcu from "@/components/Calcu.vue";
export default {
  components: { Calcu },
};
</script>
