<script>
export default {
  data() {
    return {
      phone: '',
      name: '',
      paymentMethod: 'cash',
      prepareChange: false,
      changeAmount: '',
      deliveryMethod: 'courier',
      street: '',
      house: '',
      apartment: '',
      entrance: '',
      floor: '',
      code: '',
      deliveryTime: 'now',
      email: '',
      quantity: 10,
      promoCode: ''
    };
  },
  methods: {
    submitOrder() {
      console.log('Order submitted');
    },
    increaseQuantity() {
      this.quantity++;
    },
    decreaseQuantity() {
      if (this.quantity > 0) this.quantity--;
    }
  }
};
</script>

<template>
  <div class="order-form">
    <div class="header">
      <div class="phones">
        <p>Наш телефон</p>
        <p>+996 705 188 955</p>
        <p>+996 555 188 955</p>
        <p>работаем с 10:00 до 00:00</p>
      </div>
    </div>

    <form @submit.prevent="submitOrder">
      <div class="inputs">
        <div class="personal-info">
          <input type="text" placeholder="Телефон" v-model="phone" required />
          <input type="text" placeholder="Имя" v-model="name" required />
        </div>

        <div class="payment-method">
          <label>
            <input type="radio" v-model="paymentMethod" value="cash" />
            Наличными
          </label>
          <label>
            <input type="radio" v-model="paymentMethod" value="card" />
            Картой
          </label>
          <div v-if="paymentMethod === 'cash'">
            <label>
              <input type="checkbox" v-model="prepareChange" /> Подготовить сдачу с
            </label>
            <input type="text" v-model="changeAmount" placeholder="Сумма" />
          </div>
        </div>

        <div class="delivery-method">
          <label>
            <input type="radio" v-model="deliveryMethod" value="courier" />
            Курьером
          </label>
          <label>
            <input type="radio" v-model="deliveryMethod" value="pickup" />
            Самовывоз
          </label>
        </div>

        <div class="address" v-if="deliveryMethod === 'courier'">
          <input type="text" v-model="street" placeholder="Улица" required />
          <input type="text" v-model="house" placeholder="Дом" required />
          <input type="text" v-model="apartment" placeholder="Кв" />
          <input type="text" v-model="entrance" placeholder="Подъезд" />
          <input type="text" v-model="floor" placeholder="Этаж" />
          <input type="text" v-model="code" placeholder="Код" />
        </div>

        <div class="time">
          <label>
            <input type="radio" v-model="deliveryTime" value="now" />
            На сейчас
          </label>
          <label>
            <input type="radio" v-model="deliveryTime" value="later" />
            На время
          </label>
          <input type="email" v-model="email" placeholder="E-mail (необязательно)" />
        </div>

        <div class="order-details">
          <p>Палочки + соусник обычные</p>
          <button type="button" @click="increaseQuantity">+</button>
          <span>{{ quantity }}</span>
          <button type="button" @click="decreaseQuantity">-</button>
        </div>

        <input type="text" v-model="promoCode" placeholder="Введите промокод" />
      </div>

      <button type="submit" class="submit-btn">Оформить заказ</button>
    </form>
  </div>
</template>

<style lang="scss" scoped>
.order-form {
  .header {
    text-align: center;

    .phones {
      color: #ff7700;

      p {
        margin: 0;
      }
    }
  }

  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;

    .inputs {
      width: 100%;
      max-width: 500px;

      .personal-info,
      .payment-method,
      .delivery-method,
      .time {
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;

        input {
          flex: 1;
          margin: 0 10px;
          padding: 10px;
          border: 1px solid #ccc;
          border-radius: 5px;
        }
      }

      .payment-method {
        label {
          display: flex;
          align-items: center;

          input {
            margin-right: 5px;
          }
        }
      }

      .delivery-method,
      .time {
        label {
          margin-right: 15px;
        }
      }

      .address {
        input {
          margin: 5px 0;
        }
      }

      .order-details {
        display: flex;
        align-items: center;

        p {
          flex: 1;
        }

        button {
          padding: 5px 10px;
          border: none;
          background-color: #ff7700;
          color: #fff;
          border-radius: 5px;
        }
      }

      .submit-btn {
        width: 100%;
        padding: 15px;
        background-color: #ff7700;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;

        &:hover {
          background-color: #ff5500;
        }
      }
    }
  }
}
</style>