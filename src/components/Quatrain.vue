<script setup lang="ts">
const props = defineProps<{
  quatrain: string;
}>();

const lines = props.quatrain.split('\n');
</script>

<template>
  <div class="quatrain">
    <p
      v-for="(line, index) of lines"
      :key="index"
      class="quatrain__line"
    >
      <span
        v-if="index % 2 === 1"
        class="quatrain__tab"
      />{{ line }}
    </p>
  </div>
</template>

<style>
.quatrain {
  display: flex;
  flex-direction: column;
  gap: 2px;
  margin-bottom: 16px;
}

.quatrain__line {
  display: inline-flex;
}

.quatrain__tab {
  margin-left: 26px;
}

@media (max-width: 767px) {
  .quatrain__tab {
    margin-left: 16px;
  }
}
</style>
