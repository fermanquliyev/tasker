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
    <input type="text" id="cname" name="cardname" placeholder="John More Doe" />
    <label for="ccnum">Credit card number</label>
    <input
      v-model.trim="cardNumber"
      type="text"
      id="ccnum"
      name="cardnumber"
      placeholder="1111-2222-3333-4444"
    />
    <label for="expmonth">Exp Month</label>
    <input
      type="month"
      v-model.trim="expMonth"
      id="expmonth"
      name="expmonth"
      placeholder="September"
    />

    <div class="row">
      <div class="col-6">
        <label for="expyear">Exp Year</label>
        <input
          type="text"
          v-model.number="expYear"
          id="expyear"
          name="expyear"
          placeholder="2018"
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
      expMonth: "",
      expYear: "",
      cvv: null
    };
  },
  computed: {
    paypentData() {
      return {
        cardNumber: this.cardNumber,
        expMonth: this.expMonth,
        expYear: this.expYear,
        cvv: this.cvv
      };
    }
  }
};
</script>

<style scoped>
input[type=text],input[type=month] {
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
