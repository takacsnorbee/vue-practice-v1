<template>
  <div class="container border text-center mt-4">
    <appHeadline id="appHeadline">{{headline}}</appHeadline>
    <appInput :genderProp="genders" @inputsFilled="allFilled=$event" v-if="!allFilled"></appInput>
    <appPreview v-show="allFilled"></appPreview>
    <appProgress v-if="!allFilled"></appProgress>
  </div>
</template>

<script>
import Headline from './components/Headline';
import Input from './components/Input';
import Preview from './components/Preview';
import Progress from './components/Progress';

export default {
  data: function() {
    return {
      headline: "Vue.js practice v1.0!",
      genders: ['male', 'female'],
      allFilled: false
    }
  },
  components: {
    appHeadline: Headline,
    appInput: Input,
    appPreview: Preview,
    appProgress: Progress
  },
  methods: {

  }
}
</script>

<style scoped>
  #appHeadline {
    font-size: 2rem;
    font-style: italic;
    font-weight: bold;
    text-decoration: underline;
    margin-bottom: 2rem;
  }
</style>