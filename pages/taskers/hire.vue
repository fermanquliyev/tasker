<template>
  <div class="container mt-2">
    <div class="row">
      <div class="col-md-3"></div>
      <div class="col-md-6">
        <step-indicator :currentStep="currentStepIndex" :steps="steps"></step-indicator>
      </div>
      <div class="col-md-3"></div>
    </div>
    <div class="row">

    </div>
  </div>
</template>


<script>
import StepIndicator from '../../components/StepIndicator.vue'
export default {
  components: { StepIndicator },
  data() {
    return {
      steps:[
        'Task',
        'Payment'
      ],
      currentStep:'Task'
    }
  },

  computed:{
     currentStepIndex(){
      return this.steps.indexOf(this.currentStep);
    }
  }
}
</script>
