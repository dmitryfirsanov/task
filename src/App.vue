<script setup lang="ts">
import Poem from './components/Poem.vue';

const poem = {
  title: 'Invictus',
  author: 'William Ernest Henley',
  text: 'Out of the night that covers me,\nBlack as the pit from pole to pole,\nI thank whatever gods may be\nFor my unconquerable soul.\n\nIn the fell clutch of circumstance\nI have not winced nor cried aloud.\nUnder the bludgeonings of chance\nMy head is bloody, but unbowed.\n\nBeyond this place of wrath and tears\nLooms but the Horror of the shade,\nAnd yet the menace of the years\nFinds and shall find me unafraid.\n\nIt matters not how strait the gate,\nHow charged with punishments the scroll,\nI am the master of my fate,\nI am the captain of my soul.',
};
</script>

<template>
  <main>
    <Poem :poem="poem" />
  </main>
</template>

<style>
main {
  width: 1000px;
  margin: 100px auto;
}


@media (max-width: 1023px) {
  main {
    width: 800px;
  }
}

@media (max-width: 767px) {
  main {
    width: 400px;
  }
}

</style>
