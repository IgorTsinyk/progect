<template>
  <div class="v-main-page">
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>

export default {
  name: "v-main-page",
  data() {
    return {
      title: "Main Page"
    };
  },
  props: {},
  computed: {},
  methods: {},
  watch: {}
};
</script>

<style>
.v-main-page {
  max-width: 900px;
  margin: 0 auto;
}
</style>