<template>
  <div>
    <v-chip label color="accent custom-transparent" class="ma-1" v-for="(time, index) in allTimes" :key="index">
      <v-icon left>
        {{ $globals.icons.clockOutline }}
      </v-icon>
      {{ time.name }} |
      {{ time.value }}
    </v-chip>
  </div>
</template>

<script>
export default {
  props: {
    prepTime: String,
    totalTime: String,
    performTime: String,
  },
  computed: {
    showCards() {
      return [this.prepTime, this.totalTime, this.performTime].some(x => !this.isEmpty(x));
    },
    allTimes() {
      return [this.validateTotalTime, this.validatePrepTime, this.validatePerformTime].filter(x => x !== null);
    },
    validateTotalTime() {
      return !this.isEmpty(this.totalTime) ? { name: this.$t("recipe.total-time"), value: this.totalTime } : null;
    },
    validatePrepTime() {
      return !this.isEmpty(this.prepTime) ? { name: this.$t("recipe.prep-time"), value: this.prepTime } : null;
    },
    validatePerformTime() {
      return !this.isEmpty(this.performTime) ? { name: this.$t("recipe.perform-time"), value: this.performTime } : null;
    },
  },
  methods: {
    isEmpty(str) {
      return !str || str.length === 0;
    },
  },
};
</script>

<style scoped>
.time-card-flex {
  width: fit-content;
}
.custom-transparent {
  opacity: 0.7;
}
</style>
