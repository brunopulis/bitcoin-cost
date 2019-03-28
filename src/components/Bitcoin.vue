<template>
  <div class="bitcoin-card">
    <h1 class="bitcoin-card__title">Preços do Bitcoin</h1>

    <section v-if="errored">
      <p>Pedimos desculpas, não estamos conseguindo recuperar as informações no momento. Por favor, tente novamente mais tarde.</p>
    </section>

    <section v-else>
      <div v-if="loading">Carregando...</div>

      <div v-else v-for="currency in info" class="bitcoin-card__currency">
        {{ currency.description }}
        <span class="lighten">
          <span class="bitcoin-card__symbol" v-html="currency.symbol"></span>
          <span class="bitcoin-card__price">{{ currency.rate_float | currencydecimal }}</span>
        </span>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data() {
    return {
      info: null,
      loading: true,
      errored: false,
    }
  },

  filters: {
    currencydecimal(value) {
      return value.toFixed(2)
    },
  },
  mounted() {
    axios
      .get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then(response => (this.info = response.data.bpi))
      .catch(error => {
        this.errored = true
      })
      .finally(() => (this.loading = false))
  },
}
</script>

<style scoped>
.bitcoin-card {
  background: #2f242c;
  border-radius: 5px;
  color: #b3bfb8;
  margin-top: 20px;
  padding: 0 40px 40px;
  width: 300px;
}

.bitcoin-card__title {
  color: #fff;
}

.bitcoin-card__symbol {
  color: #fff;
  padding: 0 5px;
}
.bitcoin-card__price {
  color: #fff;
}
</style>
