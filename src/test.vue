<template>
  <v-app>
    <v-card width="90%" class="mx-auto my-10">
      <vue-tiptap-katex/>
    </v-card>
<!--        <vue-tiptap-katex/>-->
  </v-app>
</template>

<script>
import VueTiptapKatex from "@/vue-tiptap-katex";
export default {
  name: "test",
  components: {VueTiptapKatex}
}
</script>

<style scoped>

</style>
