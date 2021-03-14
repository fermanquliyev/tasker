<template>
  <div class="container mt-2">
    <div class="row">
      <div class="col-md-8">
        <b-skeleton-wrapper :loading="!user">
          <template #loading>
            <b-card>
              <b-skeleton width="85%"></b-skeleton>
              <b-skeleton width="55%"></b-skeleton>
              <b-skeleton width="70%"></b-skeleton>
            </b-card>
          </template>

          <b-card v-if="user">
            <h2>{{ user.name }} | {{ user.email }}</h2>
            <b-card-text>
              Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer
              vel faucibus felis. Maecenas in consectetur sem. Sed imperdiet
              vehicula risus, sed accumsan lectus dapibus sit amet. Morbi id
              risus in justo volutpat congue vitae non tortor. Curabitur tempus
              tincidunt tempus. Aliquam congue non ante ut imperdiet. Aliquam
              euismod elementum molestie. Fusce dictum eleifend purus, vel
              efficitur leo. Vivamus ultricies dolor eget purus ornare, sed
              hendrerit tellus egestas. Quisque interdum scelerisque libero
              vitae lobortis. Sed mollis in diam vel porttitor. Mauris sed
              lobortis lacus. Aenean in leo eu lectus iaculis malesuada semper
              vitae sem. Sed nulla tellus, vulputate id enim eu, dignissim
              faucibus erat. Curabitur ac lobortis sem. Vivamus id magna massa.
              In eu placerat libero. Donec elementum viverra libero a mattis. Ut
              scelerisque tempor lorem ut sagittis.
            </b-card-text>

            <nuxt-link :to="'/taskers/hire?id=' + user.id">
              <b-button variant="primary">Hire</b-button>
            </nuxt-link>
          </b-card>
        </b-skeleton-wrapper>
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
import axios from "axios";
import taskerProfileCard from "../../components/taskerProfileCard.vue";
export default {
  components: { taskerProfileCard },
  data() {
    return {
      user: null
    };
  },
  beforeCreate() {
    axios
      .get("https://jsonplaceholder.typicode.com/users/" + this.$route.query.id)
      .then(result => {
        this.user = result.data;
      });
  }
};
</script>
