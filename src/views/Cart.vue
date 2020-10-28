/* eslint-disable no-trailing-spaces */
<template>
<div class="container">
    <div class="left_panel">
        <!--------Cart Section ------>
        <div class="small-container cart-page"  v-if="length > 0">
            <table>
                <tr>
                    <th>Products</th>
                    <th>participant</th>
                    <th>Price</th>
                </tr>
                <tr v-for="(booking, i) in bookings" :key="i">
                    <td>
                        <div class="cart-info">
                            <img :src="require(`../assets/planned/${booking.img}`)"/>
                            <div>
                                <p>{{booking.name}}</p>
                                <a>Remove</a>
                            </div>
                        </div>
                    </td>
                    <td><input type="number" value="1"> </td>
                    <td>{{booking.price.min_price}}</td>
                </tr>
            </table>
            <div class="total-price">
                <table>
                    <tr>
                        <td>Subtotal</td>
                        <td>{{Subtotal}}</td>
                    </tr>
                    <tr>
                        <td>Tax</td>
                        <td>{{tax}}</td>
                    </tr>
                    <tr>
                        <td>Total</td>
                        <td>{{total}}</td>
                    </tr>
                </table>
            </div>
        </div>
        <div class="empty" v-if="length === 0">Busket Is empty, Please make a booking</div>
    </div>
    <div class="right_panel" >
        <div v-if="length > 0">
        <h2>Payment Options</h2>
          <div >
            <div>
                <label for="M-pesa">Mpesa</label>
                <input type="radio" name="payment"/>
            </div>
            <div>
            <label for="M-pesa">Paypal</label>
            <input type="radio" name="payment"/>
            </div><div>
            <label for="M-pesa">Cash</label>
            <input type="radio" name="payment"/>
            </div>
          </div>
          <div>
              <button v-on:click="Processed()">Processed to Checkout</button>
          </div>
          </div>
    </div>
</div>
</template>

<script>
export default {
  name: 'Checkout',
  data () {
    return {
    }
  },
  created () {
    console.log(this.$store.getters.cart)
  },
  computed: {
    bookings () {
      // Get the cart from the store.
      const cart = this.$store.state.cart
      // extract the activy from the cart.
      const activies = []
      cart.forEach(list => {
        // push activy tot he activy array
        activies.push(list.activity)
      })

      return activies
    },
    length () {
      return this.bookings.length
    },
    Subtotal () {
      // Compit the price array.
      // Get the min price from the activity
      // eslint-disable-next-line arrow-spacing
      const minPrices = this.bookings.map((booking)=> {
        return booking.price.min_price
      })
      return minPrices.reduce((a, b) => {
        return a + b
      })
    },
    tax () {
      return 300
    },
    total () {
      return this.Subtotal + this.tax
    }
  },
  methods: {
    Processed () {
      alert('Service Under development')
    }
  }
}
</script>
<style scoped>
.container {
  position: relative;
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: 85% 15%;
  grid-template-rows: 5% 95%;
  grid-template-areas:
    "control right_panel"
    "left_panel right_panel" ;
  justify-content: space-between;
}
.container .left_panel {
  grid-area: left_panel;
  background: white;
  margin: 10px;
  overflow: scroll;
}
.container .right_panel {
    grid-area: right_panel;
    background: white;
    margin: 10px;
}
.cart-page{
    margin:5px;
}
table{
    width: 100%;
    border-collapse: collapse;
}
.cart-info{
    display: flex;
    flex-wrap: wrap;
}
th{
    text-align: left;
    padding: 5px;
    color: white;
    background: #ff523b;
}
td{
    padding: 10px 5px;
}
td input{
    width: 40px;
    height: 30px;
    padding: 5px;
}
td a{
    color: #ff523b;
    font-size: 12px;
}
td img{
    width: 80px;
    height: 80px;
    margin-right: 10px;
}
.total-price{
    display: flex;
    justify-content: flex-end;
}
.total-price table{
    border-top: 3px solid #ff523b;
    width: 100%;
    max-width: 350px;
}
td:last-child{
    text-align: right;
}
th:last-child{
    text-align: right;
}
</style>
