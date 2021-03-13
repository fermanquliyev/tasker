<template>
  <div class="card">
    <img
      :src="'https://randomuser.me/api/portraits/men/' + id + '.jpg'"
      class="card-img-top"
      :alt="name"
    />
    <div class="card-body">
      <h5 class="card-title">
        <nuxt-link :to="'/taskers/about?id='+id">{{ name }}</nuxt-link>
        </h5>
      <p class="card-text">
        {{ companyName }} | {{ companyDesc }}
      </p>
      <p class="card-text">
        <small class="text-muted">{{ city }}</small>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    id:Number,
    name:String,
    companyName:String,
    companyDesc:String,
    city:String
  },
  setup() {

  },
}
</script>
