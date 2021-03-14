<template>
  <div class="container mt-2">
    <div class="row">
      <div class="col-md-3"></div>
      <div class="col-md-6">
        <step-indicator
          :currentStep="currentStepIndex"
          :steps="steps"
        ></step-indicator>
      </div>
      <div class="col-md-3"></div>
    </div>
    <div class="row">
      <div class="col-md-8">
        <div class="task" role="tablist" v-if="currentStep == 'Task'">
          <b-card class="mb-1">
            <b-card-header @click="taskStep >= 0 ? (taskStep = 0) : null">
              Your task location
              <span v-show="taskStep != 0 && location"> : {{ location }}</span>
            </b-card-header>
            <b-collapse
              id="accordion-1"
              :visible="taskStep == 0"
              accordion="my-accordion"
              role="tabpanel"
            >
              <b-card-body>
                <b-card-text>
                  <b-form-group
                    id="location"
                    description="Enter address"
                    label="Enter your address"
                    label-for="input-location"
                    valid-feedback="Click save"
                    :invalid-feedback="invalidFeedback"
                    :state="locationState"
                  >
                    <b-form-input
                      id="input-location"
                      v-model.lazy.trim="location"
                      :state="locationState"
                      trim
                    ></b-form-input>
                  </b-form-group>
                  <b-button
                    class="float-right"
                    variant="success"
                    v-if="locationState"
                    @click="setTaskStep(1)"
                    >Save</b-button
                  >
                </b-card-text>
              </b-card-body>
            </b-collapse>
          </b-card>
          <b-card class="mb-1">
            <b-card-header @click="taskStep >= 1 ? (taskStep = 1) : null">
              Your task date
              <span v-show="taskStep != 1 && taskDate"> : {{ taskDate }}</span>
            </b-card-header>
            <b-collapse
              id="accordion-2"
              :visible="taskStep == 1"
              accordion="my-accordion-2"
              role="tabpanel"
            >
              <b-card-body>
                <b-card-text>
                  <b-form-group
                    id="taskDate"
                    description="Enter task date"
                    label="Enter your task date"
                    label-for="input-taskDate"
                    valid-feedback="Click save"
                    :state="taskDate != null"
                  >
                    <b-form-datepicker
                      id="input-taskDate"
                      v-model="taskDate"
                      class="mb-2"
                    ></b-form-datepicker>
                  </b-form-group>
                  <b-button
                    class="float-right"
                    variant="success"
                    v-if="taskDate"
                    @click="setTaskStep(2)"
                    >Save</b-button
                  >
                </b-card-text>
              </b-card-body>
            </b-collapse>
          </b-card>
          <b-card class="mb-1">
            <b-card-header @click="taskStep >= 2 ? (taskStep = 2) : null">
              Your task duration
              <span v-if="taskStep != 2 && duration">
                :
                {{ durationOptions.find(x => x.value == duration).text }}</span
              >
            </b-card-header>
            <b-collapse
              id="accordion-3"
              :visible="taskStep == 2"
              accordion="my-accordion-3"
              role="tabpanel"
            >
              <b-card-body>
                <b-card-text>
                  <b-form-group label="Select task duration">
                    <b-form-radio-group
                      id="radio-group-duration"
                      v-model="duration"
                      :options="durationOptions"
                      name="duration-options"
                    ></b-form-radio-group>
                  </b-form-group>
                  <b-button
                    class="float-right"
                    variant="success"
                    v-if="duration"
                    @click="setTaskStep(3)"
                    >Save</b-button
                  >
                </b-card-text>
              </b-card-body>
            </b-collapse>
          </b-card>
          <b-card class="mb-1">
            <b-card-header @click="taskStep >= 3 ? (taskStep = 3) : null">
              Your task description
            </b-card-header>
            <b-collapse
              id="accordion-4"
              :visible="taskStep == 3"
              accordion="my-accordion-4"
              role="tabpanel"
            >
              <b-card-body>
                <b-card-text>
                  <b-form-group label="About your task">
                    <b-form-textarea
                      id="textarea"
                      v-model.trim.lazy="description"
                      placeholder="Enter task description..."
                      rows="3"
                      max-rows="6"
                    ></b-form-textarea>
                  </b-form-group>
                </b-card-text>
              </b-card-body>
            </b-collapse>
          </b-card>
          <div class="mt-2">
            <b-button
              class="float-right"
              variant="success"
              v-if="canSaveTask"
              @click="currentStep = 'Payment'"
              >Save</b-button
            >
          </div>
        </div>
        <div class="payment" v-if="currentStep == 'Payment'">
          <payment-card-input></payment-card-input>
        </div>
      </div>
      <div class="col-md-4">
        <b-spinner
          v-if="!user"
          class="m-5"
          style="width: 5rem; height: 5rem;"
          variant="info"
          label="Loading..."
        ></b-spinner>
        <tasker-profile-card
          v-else
          :city="user.address.city"
          :name="user.name"
          :id="user.id"
          :companyName="user.company.name"
          :companyDesc="user.company.catchPhrase"
        ></tasker-profile-card>
      </div>
    </div>
  </div>
</template>

<script>
import StepIndicator from "../../components/StepIndicator.vue";
import axios from "axios";
import PaymentCardInput from "../../components/PaymentCardInput.vue";
export default {
  components: { StepIndicator, PaymentCardInput },
  data() {
    return {
      user: null,
      steps: ["Task", "Payment"],
      currentStep: "Task",
      location: "",
      taskDate: null,
      taskStep: 0,
      duration: null,
      description: "",
      durationOptions: [
        { text: "Small (~1hr)", value: 1 },
        { text: "Medium (~3hr)", value: 2 },
        { text: "Large (~5hr+)", value: 3 }
      ]
    };
  },
  beforeCreate() {
    axios
      .get("https://jsonplaceholder.typicode.com/users/" + this.$route.query.id)
      .then(result => {
        this.user = result.data;
      });
  },
  methods: {
    setTaskStep(step) {
      this.taskStep = step;
    }
  },
  computed: {
    currentStepIndex() {
      return this.steps.indexOf(this.currentStep);
    },
    locationState() {
      return this.location.length >= 3;
    },
    invalidFeedback() {
      if (this.location.length > 0) {
        return "Enter at least 3 characters.";
      }
      return "Please enter something.";
    },
    canSaveTask() {
      return (
        this.locationState && this.duration && this.taskDate && this.description
      );
    }
  }
};
</script>

<style scoped>
div.card-header {
  border-radius: 20px;
}
</style>
