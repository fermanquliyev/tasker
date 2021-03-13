<template>
  <div class="container mt-1">
    <div class="row">
      <div class="col-md-4 mb-2" v-for="user of users" :key="user.id">
        <tasker-profile-card
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
import * as axios from "axios";
import taskerProfileCard from "../../components/taskerProfileCard.vue";
export default {
  components: { taskerProfileCard },
  setup() {},
  data() {
    return {
      users: []
    };
  },
  created() {
    axios.default
      .get("https://jsonplaceholder.typicode.com/users")
      .then(result => {
        this.users = result.data;
      });
  }
};
</script>
