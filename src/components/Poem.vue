<script setup lang="ts">
import { defineProps, ref } from 'vue';

import Quatrain from '../components/Quatrain.vue';

import type { Poem } from '../types/index';

const props = defineProps<{
  poem: Poem;
}>();

const quatrains = props.poem.text.split('\n\n');

const disabledQuatrains = ref<number[]>([]);

const toggleQuatrain = (quatrainIndex: number) => {
  const index = disabledQuatrains.value.indexOf(quatrainIndex);

  if (index === -1) {
    if (quatrains.length - disabledQuatrains.value.length === 1) {
      return;
    }

    disabledQuatrains.value.push(quatrainIndex);
  } else {
    disabledQuatrains.value.splice(index, 1);
  }

  console.log(disabledQuatrains.value);
};
</script>

<template>
  <div class="poem">
    <div class="poem__head">
      <h1 class="poem__title">{{ poem.title }}</h1>
      <p class="poem__author">By {{ poem.author }}</p>
    </div>
    <div class="poem__controls">
      <button
        v-for="(quatrains, index) of quatrains"
        :key="index"
        :class="[
          'poem__control',
          { 'poem__control--disabled': disabledQuatrains.includes(index) },
        ]"
        @click="toggleQuatrain(index)"
      />
    </div>
    <div class="poem__text">
      <Quatrain
        v-for="(quatrain, index) of quatrains"
        :key="index"
        :quatrain="quatrain"
        :class="[
          'poem__quatrain',
          { 'poem__quatrain--disabled': disabledQuatrains.includes(index) },
        ]"
      />
    </div>
  </div>
</template>

<style>
.poem {
  display: grid;
  grid-template-columns: auto 400px;
  grid-template-rows: repeat(2, auto);
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.poem__head {
  position: relative;
  grid-column: 2;
  grid-row: 1;
  justify-self: center;
}

.poem__title {
  display: inline-block;
  font-size: 1.8rem;
  font-weight: 600;
  margin: 0;
}

.poem__author {
  position: absolute;
  font-size: 0.9rem;
  bottom: 4px;
  right: -200px;
}

.poem__text {
  grid-column: 2;
  grid-row: 2;
  justify-self: self-start;
  display: flex;
  flex-direction: column;
  font-size: 1.1rem;
}

.poem__controls {
  grid-column: 1;
  grid-row: 2;
  align-self: self-start;
  display: flex;
  gap: 8px;
  margin-top: 3px;
}

.poem__control {
  width: 20px;
  height: 20px;
  border: 1px solid #000;
  background: #000;
  cursor: pointer;
}

.poem__control--disabled {
  background: transparent;
}

.poem__quatrain--disabled {
  display: none;
}

@media (max-width: 767px) {
  .poem {
    display: flex;
    flex-direction: column;
  }

  .poem__head {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .poem__author {
    position:static;
  }

  .poem__controls {
    align-self: center;
  }
}

@media (min-width: 1921px) {
  .poem__author {
    right: -260px;
  }
}
</style>
