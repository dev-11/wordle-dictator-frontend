<template>
  <div>
    <div class="letter-row">
      <div v-bind:key="i" v-for="(char, i) in word" class="letter-box">
        {{ char }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Wordle",
  props: {
    word: String
  },
};
</script>

<style>
.letter-box {
  border: 2px solid #787c7e;
  margin: 2px;
  font-size: 2.5rem;
  font-weight: 700;
  height: 3rem;
  width: 3rem;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
}

.letter-row {
  display: flex;
}
</style>
