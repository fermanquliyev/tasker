<template>
  <div>
    <h3>Payment</h3>
    <label for="fname">Accepted Cards</label>
    <div class="icon-container">
      <i class="fa fa-cc-visa" style="color:navy;"></i>
      <i class="fa fa-cc-amex" style="color:blue;"></i>
      <i class="fa fa-cc-mastercard" style="color:red;"></i>
      <i class="fa fa-cc-discover" style="color:orange;"></i>
    </div>
    <label for="cname">Name on Card</label>
    <input type="text" id="cname" name="cardname" placeholder="John More Doe" maxlength="20"/>
    <label for="ccnum">Credit card number</label>
    <input
      v-model.trim="cardNumber"
      type="text"
      id="ccnum"
      name="cardnumber"
      maxlength="16"
      placeholder="1111-2222-3333-4444"
    />

    <div class="row">
      <div class="col-6">
        <label for="expmonth">Expire date</label>
        <input
          type="month"
          v-model="expDate"
          id="expDate"
          name="expDate"
          placeholder="Month Year"
        />
      </div>
      <div class="col-6">
        <label for="cvv">CVV</label>
        <input
          type="text"
          v-model.number="cvv"
          id="cvv"
          name="cvv"
          placeholder="352"
          maxlength="3"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cardNumber: "",
      expDate: "",
      cvv: null
    };
  },
  computed: {
    paymentData() {
      return {
        cardNumber: this.cardNumber,
        expDate: this.expDate,
        cvv: this.cvv
      };
    }
  },
  watch:{
    cardNumber(){
      this.$emit('change',this.paymentData);
    },
    expDate(){
      this.$emit('change',this.paymentData);
    },
    cvv(){
      this.$emit('change',this.paymentData);
    },
  }
};
</script>

<style scoped>
input[type="text"],
input[type="month"] {
  width: 100%;
  margin-bottom: 20px;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

label {
  margin-bottom: 10px;
  display: block;
}

.icon-container {
  margin-bottom: 20px;
  padding: 7px 0;
  font-size: 24px;
}
</style>
