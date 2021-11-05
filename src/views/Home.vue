<template>
  <div class="container">
    <div class="load" v-if="results == null">
      <img class="img-temp" src="img/load.svg" alt="" />
    </div>
    <div class="row row-cols-1 row-cols-md-3 g-4">
      <div v-for="(result, index) in results" :key="index" class="col">
        <div class="card h-100">
          <div class="card-body">
            <div class="row">
              <div class="col col-nav">
                <h1>{{ result.CAPITAL }}</h1>
                <p class="date">
                  <i class="far fa-calendar-alt"></i> {{ date }}
                </p>
              </div>
            </div>

            <div class="row">
              <div class="col col-content">
                <img class="img-temp" src="img/max-temp.png" alt="" />
                <div class="title">Max</div>
                <div class="temp">{{ result.TMAX18 }}</div>
              </div>
              <div class="col col-content">
                <img class="img-temp" src="img/min-temp.png" alt="" />
                <div class="title">Min</div>
                <div class="temp">{{ result.TMIN18 }}</div>
              </div>
            </div>

            <div class="row">
              <div class="col col-content">
                <img class="img-temp" src="img/umi.png" alt="" />
                <div class="title">Max</div>
                <div class="temp">{{ result.PMAX12 }}</div>
              </div>
              <div class="col col-content">
                <img class="img-temp" src="img/umi.png" alt="" />
                <div class="title">Min</div>
                <div class="temp">{{ result.UMIN18 }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

  <script>
export default {
  name: "Home",
  data() {
    return {
      results: null,
      date: null,
    };
  },

  methods: {
    async getClima() {
      const url = "https://apitempo.inmet.gov.br/condicao/capitais/";
      const todayDate = new Date();
      const date_format = todayDate.toISOString().slice(0, 10);
      const url_date = `${url}${date_format}`;

      const req = await fetch(url_date);
      const data = await req.json();

      this.results = data;
      this.date = date_format;
    },
  },

  mounted() {
    this.getClima();
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Nunito:wght@200;300;400;600;700;800&display=swap");
* {
  font-family: "Nunito", sans-serif;
}

.card {
  background-color: rgb(113, 89, 193, 0.6);
  border-radius: 1rem;
  border-color: transparent;
}

.col-nav {
  margin: 0.4rem;
}
.col-content {
  background-color: #ffff;
  color: #34495e;
  margin: 0.4rem;
  height: 10rem;
  border-radius: 1rem;
  border-left: 4px solid #7159c1;
}
.img-temp {
  margin: 0.4rem;
  max-width: 4rem;
  max-height: 4rem;
}

.title {
  font-size: 1.2rem;
  font-weight: 600;
}
.temp {
  font-size: 2rem;
  font-weight: 600;
}

h1 {
  font-size: 1.6rem;
  color: #ffff;
  font-weight: bold;
}

.date {
  color: #ffff;
}

@media only screen and (max-width: 386px) {
  h1 {
    font-size: 1.6rem;
  }
}
</style>