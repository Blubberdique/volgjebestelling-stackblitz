<template>
  <nav class="navbar navbar-dark bg-black">
    <div class="container-fluid d-flex justify-content-between">
      <div></div>
      <div class="image-container">
        <a class="text-center" href="/">
          <img
            class="centered-image"
            width="300px"
            height="94px"
            src="../images/mangohoutonline_logo.png"
            alt=""
          />
        </a>
      </div>
      <div>
        <a href="https://mangohoutonline.nl" class="btn btn-shop"
          >Terug naar de webshop</a
        >
      </div>
    </div>
  </nav>

  <!-- Banner -->

  <div class="background-image">
    <div class="overlay">
      <div class="centered-text">
        <h1>Volg je bestelling</h1>
      </div>
    </div>
  </div>
  <!-- Steps -->
  <div class="container col-md-12">
    <div class="form-body">
      <div class="inputs">
        <p>
          Vul je ordernummer en e-mail adres in en klik op de "Zoeken" knop om
          actuele bestelstatus te volgen. Het ordernummer kun je vinden op je
          ontvangstbewijs en in de bevestigings-e-mail.
        </p>
        <div class="row input-forms">
          <div class="col-md-5">
            <label for="order">Ordernummer</label>
            <input
              class="form-control"
              type="text"
              name="order"
              id="order"
              v-model="orderNumber"
              required
            />
          </div>
          <div class="col-md-5">
            <label for="email">E-mailadres</label>
            <input
              class="form-control"
              type="email"
              name="email"
              id="order_email"
              v-model="emailAddress"
              required
            />
          </div>
          <div class="col-md-1 button d-flex align-items-end">
            <button class="btn btn-search" @click="search">ZOEKEN</button>
          </div>
        </div>
      </div>

      <!-- Cards -->
      <div class="row row-cards">
        <div class="d-flex align-items-center">
          <div class="container container-cards col-md-4">
            <div class="container-inner">
              <div class="icon-box-content">
                <img
                  style="margin-left: 30px"
                  width="130px;"
                  height="130px"
                  src="../images/stap1.svg"
                />
              </div>
              <div class="info-box-content">
                <div class="step-header"><strong>STAP 1</strong></div>
                <div class="info-box-summary">
                  <h4>Vul je ordernummer in</h4>
                </div>
                <div class="info-box-subtitle">
                  <p>
                    Het ordernummer wordt in de mail van bestelling weergegeven.
                  </p>
                </div>
              </div>
            </div>
          </div>
          <div class="container container-cards col-md-4">
            <div class="container-inner">
              <div class="icon-box-content">
                <img width="130px;" height="130px" src="../images/stap2.svg" />
              </div>
              <div class="info-box-content">
                <div class="step-header"><strong>STAP 2</strong></div>
                <div class="info-box-summary">
                  <h4>Vul je e-mail adres in</h4>
                </div>
                <div class="info-box-subtitle">
                  <p>
                    Vul het e-mail adres in dat je gebruikt hebt voor de
                    bestelling.
                  </p>
                </div>
              </div>
            </div>
          </div>
          <div class="container container-cards col-md-4">
            <div class="container-inner">
              <div class="icon-box-content">
                <img width="130px;" height="130px" src="../images/stap3.svg" />
              </div>
              <div class="info-box-content">
                <div class="step-header"><strong>STAP 3</strong></div>
                <div class="info-box-summary"><h4>Druk op zoeken</h4></div>
                <div class="info-box-subtitle">
                  <p>Je bestelgegevens worden opgehaald.</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="footer border-top">
    <div class="text-center">
      <p>
        &copy; {{ new Date().getFullYear() }} Mangohoutonline<br />Aan de
        informatie op onze website kunnen geen rechten worden ontleend
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      order: '',
      email: '',
      isOrderInvalid: false,
      isEmailInvalid: false,
    };
  },
  methods: {
    handleOrderInvalid(event) {
      this.isOrderInvalid = true;
      event.target.setCustomValidity('Vul een ordernummer in');
    },
    handleOrderInput(event) {
      this.isOrderInvalid = false;
      event.target.setCustomValidity('');
    },
    handleEmailInvalid(event) {
      this.isEmailInvalid = true;
      event.target.setCustomValidity('Vul een e-mailadres in');
    },
    handleEmailInput(event) {
      this.isEmailInvalid = false;
      event.target.setCustomValidity('');
    },
    search() {
      // Check if the order number and email are entered
      if (this.order && this.email) {
        // Construct the API URL with the order number and email
        const apiUrl = `https://public.jongstratransport.nl/order_tracking?reference=${encodeURIComponent(
          this.order
        )}&email=${encodeURIComponent(this.email)}`;

        // Perform the API request
        fetch(apiUrl)
          .then((response) => response.json())
          .then((data) => {
            // Log the response data to the console
            console.log(data);

            // Further process the response data as needed (e.g., update the UI, store it in Vuex, etc.)
          })
          .catch((error) => {
            console.error('Error:', error);
            // Handle any errors that occur during the API request
          });
      } else {
        // Handle case where the order number and/or email are not entered
        console.log('Please enter the order number and email.');
      }
    },
  },
};
</script>

<style>
/* Navbar */
.navbar {
  height: 115px;
  z-index: 1;
  padding-top: 0 !important;
}

.image-container {
}

.btn {
  color: #fff;
}

.btn-shop {
  border-radius: 0 !important;
  position: fixed;
  right: 20px;
  transform: translateY(-50%);
  background-color: rgb(187, 137, 84);
}

.btn-shop:hover {
  color: #fff;
  background-color: rgb(183, 125, 81);
}

.header {
  padding-bottom: 20px;
  padding-left: 40px;
  background: black;
  position: relative;
}

/* Banner */
.background-image {
  height: 300px;
  position: relative;
  background-size: cover;
  background-image: url(../images/banner.jpg);
}

.background-image::before {
  content: '';
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url('../images/banner.jpg'); /* Replace with the actual image path */
  background-size: cover;
  background-position: center;
  z-index: -1;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(
    0,
    0,
    0,
    0.5
  ); /* Adjust the desired overlay color and opacity */
  display: flex;
  justify-content: center;
  align-items: center;
}

.centered-text {
  text-align: center;
  color: #ffffff; /* Adjust the desired text color */
  font-family: sans-serif;
  font-weight: bold;
}

.centered-image {
  max-width: 100%;
  max-height: 100%;
}

/* Body */

.form-body {
  margin-top: 50px;
}

/* Search forms */

.inputs {
  margin-bottom: 20px;
  font-size: 14px;
}

.inputs input:focus {
  outline: none;
  border-color: lightgrey;
  box-shadow: none;
}

.label {
  display: block;
}

.btn-search {
  background-color: rgb(187, 137, 84);
  border-radius: 5px;
  font-size: 13px;
}

.btn-search:hover {
  color: #fff;
  background-color: rgb(183, 125, 81);
}

/* Cards */

.row-cards {
  display: flex;
}

.container-cards {
  padding: 20px;
}

.icon-box-content {
  margin-bottom: 15px;
}

.step-header {
  color: #777;
  font-size: 14px;
}

.info-box-summary {
  font-size: 20px;
}

.info-box-subtitle {
  color: #777;
  font-size: 14px;
}
/* Footer */

.footer {
  font-size: 11px;
  font-family: sans-serif;
}
</style>
