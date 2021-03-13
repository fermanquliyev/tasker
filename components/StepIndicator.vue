<template>
  <ul class="progressbar">
    <li
      v-for="(item, index) of steps"
      :key="index"
      :class="{ active: index <= currentStep }"
    >
      {{ item }}
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    steps: Array,
    currentStep: Number
  }
};
</script>

<style scoped>
.progressbar li {
flex-grow: 1;
    flex-basis: 0;
  position: relative;
  text-align: center;
}
.progressbar {
  counter-reset: step;
  list-style: none;
  display: flex;
  flex-direction: row;
}
.progressbar li:before {
  content: counter(step);
  counter-increment: step;
  width: 35px;
  height: 35px;
  border: 2px solid #bebebe;
  display: block;
  margin: 0 auto 10px auto;
  border-radius: 50%;
  line-height: 32px;
  background: white;
  color: #bebebe;
  text-align: center;
  font-weight: bold;
}

.progressbar li:after {
  content: "";
  position: absolute;
  width: 100%;
  height: 3px;
  background: #979797;
  top: 15px;
  left: -50%;
  z-index: -1;
}
.progressbar li:first-child:after {
  content: none;
}
.progressbar li.active + li:after {
  background: #3aac5d;
}
.progressbar li.active::before {
  border-color: #3aac5d;
  background: #3aac5d;
  color: white;
}
</style>
