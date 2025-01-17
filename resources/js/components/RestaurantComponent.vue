<template>
  <div class="restaurant">
    <div class="title-profile">
      <h2>
        Benvenuto nella tua sezione del ristorante: <br />
        Da qui puoi accedere alla lista dei piatti, crearne di nuovi e
        modificarli.
      </h2>
      <hr class="line-profile" />
    </div>

    <div class="profile-container">
      <div class="restaurant-profile">
        <h1>{{ restaurants.restaurant_name }}</h1>
        <img
          class="restaurant-image"
          :src="'/storage/images/' + restaurants.image"
          alt=""
        />
      </div>

      <div class="manage-restaurant">
        <p>
          <strong>Nome titolare:</strong>
          {{ restaurants.owner_name }}
        </p>
        <p>
          <strong>Partita IVA:</strong>
          {{ restaurants.p_iva }}
        </p>
        <p class="mt-4">
          <strong>Indirizzo:</strong> {{ restaurants.address }}
        </p>
        <p><strong>Email:</strong> {{ restaurants.email }}</p>
        <p><strong>Telefono:</strong> {{ restaurants.restaurant_phone }}</p>
        <div>
          <button class="register-button" @click="getDishes(user_id)">
            Lista piatti
          </button>
        </div>
      </div>
    </div>

    <!-- sezione statistiche-->

    <div class="restaurant-info">
      <hr class="line-profile" />
      <h1>Visualizza i tuoi ordini</h1>

      <button class="drop-down-btn" @click.prevent="getOrders(user_id)">
        <p>Statistiche del tuo ristorante.</p>
      </button>
    </div>

    <!-- sezione cards attività -->

    <!-- card 1 -->
    <div class="card-service">
      <h1>Altri modi per far crescere la tua attivi&agrave;</h1>
      <p>Prodotti e servizi per un successo garantito</p>

      <div class="cards-restaurant">
        <div>
          <img src="/storage/images/consegna-domicilio.jpg" alt="" />
        </div>
        <div>
          <h3>Solo consegna a domicilio</h3>
          <p>
            Dalla gestione del locale a quella del personale, le nostre guide ti
            aiuteranno ad aprire un ristorante dedicato alle consegne a
            domicilio.
          </p>
        </div>
      </div>

      <!-- card 2 -->
      <div class="cards-restaurant">
        <div>
          <img src="/storage/images/Helpcenter.jpg" alt="" />
        </div>
        <div>
          <h3>Sicurezza e igene</h3>
          <p>
            Qualche accorgimento per tutelare la tua sicurezza e quella di rider
            e clienti in risposta all'emergenza COVID-19.
          </p>
        </div>
      </div>

      <!-- card 3 -->
      <div class="cards-restaurant">
        <div>
          <img src="/storage/images/Holding-Phone.jpg" alt="" />
        </div>
        <div>
          <h3>Il nostro hub COVID-19</h3>
          <p>
            Consigli per i ristoranti partner, aggiornamenti su come stiamo
            rispondendo all'emergenza e raccomandazioni del governo.
          </p>
        </div>
      </div>

      <!-- card 4 -->
      <div class="cards-restaurant">
        <div>
          <img src="/storage/images/Packaging.jpg" alt="" />
        </div>
        <div>
          <h3>Packaging</h3>
          <p>
            Confezioni personalizzate per ogni tipo di cucina; le riceverai con
            consegna gratuita entro il giorno successivo.
          </p>
        </div>
      </div>

      <!-- card 5 -->
      <div class="cards-restaurant">
        <div>
          <img src="/storage/images/Marketer.jpg" alt="" />
        </div>
        <div>
          <h3>Marketer</h3>
          <p>
            Fatti conoscere da nuovi clienti con gli strumenti promozionali
            dell'app: basta qualche passaggio per aumentare gli ordini fino al
            60%.
          </p>
        </div>
      </div>

      <!-- card 6 -->
      <div class="cards-restaurant">
        <div>
          <img src="/storage/images/kitchen-deliveroo.jpg" alt="" />
        </div>
        <div>
          <h3>Integrazione del Sistema di Cassa</h3>
          <p>
            Collega il tuo sistema alla nostra API per tenere d'occhio le
            vendite e le scorte in tempo reale.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      restaurants: [],
      dishes: [],
    };
  },

  props: {
    user_id: String,
  },

  mounted() {
    axios
      .get("/restaurant/info/" + this.user_id)
      .then((r) => (this.restaurants = r.data))
      .catch((e) => console.error(e));
  },

  methods: {
    // Metodo per ritornare la pagina blade contenente tutti i piatti del ristorante!
    getDishes(id) {
      window.location.href = `/dishes/list/${id}`;
    },

    getOrders(id) {
      window.location.href = `/order/statistics/${id}`;
    },
  },
};
</script>

<style scoped lang="scss">
.restaurant {
  background-color: #fbfbfb;
}

.title-profile {
  padding-top: 75px;
  width: 70%;
  margin-left: 15%;
}

.profile-container {
  display: flex;
  justify-content: left;
  flex-wrap: wrap;
  width: 70%;
  margin-left: 15%;
}

.restaurant-profile {
  width: 35%;

  h1 {
    margin-bottom: 25px;
    font-size: 32px;
    font-weight: 600;
  }

  img {
    width: 80%;
    min-width: 80%;
    max-width: 80%;
    -moz-box-shadow: 0 0 3px rgb(182, 179, 179);
    -webkit-box-shadow: 0 0 3px rgb(182, 179, 179);
    box-shadow: 0 0 14px rgb(10, 9, 9);
  }
}

.line-profile {
  width: 100%;
  margin: 50px 0;
}

.manage-restaurant {
  margin-top: 62px;

  button {
    border-style: none;
  }

  p {
    font-size: 17px;
  }
}

.register-button {
  font-size: 15px;
  font-weight: 600;
  text-shadow: 1px 1px 1px #000;
}

// sezione info bottoni

.restaurant-info {
  width: 70%;
  margin-left: 15%;
  text-align: center;

  h1 {
    margin-bottom: 70px;
  }
}

.drop-down-btn {
  width: 40%;
  background-color: #fff;
  border: #cdcdcd 1px solid;
  background-color: #ffffff;
  cursor: pointer;
  padding: 20px 20px;
  margin-bottom: 150px;
  border-radius: 10px;

  &:hover {
    box-shadow: 0 5px 5px 0 #cdcdcd, 0 5px 5px 0 #cdcdcd;
  }

  p {
    text-align: center;
    cursor: pointer;
    padding-top: 5px;
    font-size: 18px;
  }
}

// sezione card

.card-service {
  width: 70%;
  margin-left: 15%;
  text-align: center;
  margin-top: 150px;
  margin: 0 auto 40px auto;
  grid-gap: 1rem;
}

.cards-restaurant {
  width: 280px;
  display: inline-block;
  text-decoration: none;
  color: inherit;
  margin: 24px 10px 0 10px;
  background-color: #fff;
  box-shadow: 0px 0px 6px rgb(0 0 0 / 10%);
  border-radius: 3px;
  overflow: hidden;
  position: relative;
  height: 500px;

  div:nth-child(2) {
    padding: 0 12px;
  }

  &:hover {
    box-shadow: 0 5px 5px 0 #cdcdcd, 0 5px 5px 0 #cdcdcd;
  }

  h3 {
    margin: 15px 0;
    font-size: 24px;
  }

  p {
    font-size: 17px;
    color: #3e3e3e;
  }

  img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }
}

@media all and (max-width: 1200px) {
  .restaurant-profile {
    h1 {
      font-size: 28px;
    }

    img {
      width: 90%;
    }
  }
}

@media all and (max-width: 733px) {
  .restaurant-profile {
    img {
      width: 190px;
    }
  }
}
</style>
