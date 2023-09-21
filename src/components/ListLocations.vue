<template>
  <section style="background-color: #e4e4e4; width: 100%; padding-top: 15em">
    <!--wireframe: Encuentra tu tienda-->
    <article
      style="
        align-items: center;
        display: flex;
        margin-right: auto;
        margin-left: auto;
        position: relative;
      "
      class="row p-2 shadow-sm"
    >
      <div class="col-2" />
      <section style="text-align: left" class="col-4 p-4">
        <article>
          <h3 style="color: #6297b7" class="mb-3">
            <b>Encuentra tu tienda</b>
          </h3>
        </article>
        <article class="mb-4 text-body-secondary">
          <b>Localiza tu concesionario más cercano</b>
        </article>
        <article>
          <p class="card-text mb-4" style="color: #727272">
            Introduce tu dirección o, simplemente tu código postal, y encuentra
            tu concesionario más cercano.
          </p>
        </article>
        <article>
          <input
            v-on:keyup.enter="newsearch()"
            v-model="search"
            class="mb-3"
            style="
              margin-left: 0.01em;
              padding-left: 1em;
              width: 25em;
              border: 0.1em solid #6297b7;
              border-radius: 0.25em;
            "
          />
        </article>
        <article>
          <p class="card-text mb-4">
            <img
              style="width: 1em; margin-right: 0.2em"
              src="/ubicacion_Arena.svg"
            /><span style="border-bottom: 0.1em solid #6297b7"
              >Utilizar ubicación actual</span
            >
          </p>
        </article>
        <article v-show="noresults === true">
          <p>Lo sentimos no encontramos resultados.</p>
        </article>
        <a style="text-decoration: none; color: white" href="#"
          ><button
            @click="newsearch()"
            class="mb-5"
            style="
              width: 13em;
              background-color: #6297b7;
              color: white;
              font-size: 0.9em;
              border-radius: 0.25em;
              border: none;
              text-align: center;
              padding: 0.25em;
            "
          >
            <b>ENCUENTRA TU TIENDA</b>
          </button></a
        >
      </section>
      <section style="text-align: left" class="col-4 d-none d-lg-block">
        <img
          style="width: 75%"
          class="bd-placeholder-img"
          src="/imag_tiendas_ubi_2.png"
        />
      </section>
      <div class="col-2" />
    </article>
    <!--Fin de wireframe: Encuentra tu tienda-->
    <!--After the search wireframe-->
    <article
      v-show="findstore === false"
      style="
        background-color: #e4e4e4;
        align-items: center;
        display: flex;
        margin-right: auto;
        margin-left: auto;
        position: relative;
      "
      class="row roundedshadow-sm"
    >
      <div class="col-2" />
      <section style="text-align: left" class="col-5 p-4">
        <h4 style="color: #6297b7; width: 80%" class="mb-3">
          <b v-if="amountresults > 1"
            >Se han encontrado {{ amountresults }} concesionarios cerca de tu
            ubicación actual</b
          ><b v-if="amountresults === 1"
            >Se ha encontrado 1 concesionario cerca de tu ubicación actual</b
          >
        </h4>
        <div
          style="text-transform: capitalize"
          class="mb-4 text-body-secondary"
        >
          <b style="font-size: 0.8em">{{ search }}</b>
        </div>
        <div>
          <article v-for="stores in aftersearch" :key="stores.id">
            <section
              v-if="
                stores.Estado === 'ACTIVO' &&
                stores.Empresa.includes('ARENA') &&
                stores.Condición === 'Tienda'
              "
            >
              <a style="text-decoration: none; color: white" href="#">
                <button
                  class="row mb-4"
                  style="border: none; background: none; text-align: left"
                  @click="maprute(stores.Ubicación)"
                >
                  <article style="margin-top: 1em" class="col-1 fs-4">
                    <img style="width: 1em" src="/ubicacion_Arena.svg" />
                  </article>
                  <article style="width: 20em" class="col">
                    <div
                      style="font-size: 0.9em"
                      class="mb-1 text-body-secondary"
                    >
                      <b>{{ stores.Nombre_dealer }}</b>
                    </div>
                    <div
                      style="font-size: 0.9em"
                      class="mb-1 text-body-secondary"
                    >
                      {{ stores.Ubicación }}
                    </div>
                    <div style="font-size: 0.9em; color: #6297b7" class="mb-1">
                      {{ stores.Teléfono }}
                    </div>
                    <div class="dropdown-center mb-4">
                      <button
                        style="background: none; border: none"
                        class="text-body-secondary dropdown-toggle"
                        type="button"
                        data-bs-toggle="dropdown"
                        aria-expanded="false"
                      >
                        Horarios
                      </button>
                      <section
                        style="background: none; border: none"
                        class="dropdown-menu"
                      >
                        <article>
                          <div class="dropdown-item">{{ stores.Horarios }}</div>
                        </article>
                      </section>
                    </div>
                  </article>
                </button>
              </a>
            </section>
          </article>
        </div>
      </section>
      <section class="col-5">
        <article style="width: 80%">
          <iframe
            scrolling="no"
            marginheight="0"
            marginwidth="0"
            :src="
              'https://maps.google.com/maps?width=100%25&amp;height=400&amp;hl=es&amp;q=' +
              where +
              '&amp;t=&amp;z=14&amp;ie=UTF8&amp;iwloc=B&amp;output=embed'
            "
            width="100%"
            height="400"
            frameborder="0"
            ><a href="https://www.gps.ie/car-satnav-gps/"></a
          ></iframe>
        </article>
      </section>
      <div class="col-2" />
    </article>
    <!--Fin de wireframe: After the search-->
  </section>
</template>
<script>
// Se importan los tatos de forma local en caso de falla de la api o falla de la Base de Datos
import motorcycle from "@/data/motorcycle.json";
export default {
  setup() {
    return {
      stores: [],
      where: "",
      search: "",
      aftersearch: [],
      findstore: true,
      noresults: false,
      amountresults: null,
    };
  },
  created() {
    //  Se llama a la función getStores() para solicitar los datos legítimos de las tiendas de la base de datos
    this.getStores();
  },
  methods: {
    //  Función getStores(), solicita los datos a la API de todas las tiendas de la base de datos.
    getStores() {
      //  Se inicializa la variable 'stores' con una copia local de las tiendas de la base de datos, por si fallase en algún momento la conexión con la API o con la base de datos
      this.stores = motorcycle;
      fetch("http://localhost:8081/api/stores")
        .then((r) => r.json())
        .then((j) => {
          this.stores = [];
          this.stores = j;
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    //  Función newsearch(), recorrera en base a la búsqueda realizada, los datos 'stores' proporcionados por la api en busca de coincidencias en las columnas: Comunidad y Nombre_dealer...
    //  NOTA:('Se ha agregado la columna CP. Solo se ha agregado para poder realizar la búsqueda por Código Postal a modo extra, creía recomendable separar el CP en la base de datos y filtrar por CP')
    newsearch() {
      // Se reasigna search a search sustituyendo todo el contenido por mayusculas y se reinicializa la variable 'aftersearch' con un array vacio '[ ]'
      this.search = this.search.toUpperCase();
      this.aftersearch = [];
      //  Se recorre Stores
      for (let i = 0; i < this.stores.length; i++) {
        if (
          this.stores[i].Comunidad.toUpperCase().includes(this.search) ||
          this.stores[i].Nombre_dealer.toUpperCase().includes(this.search) ||
          this.stores[i].CP.toUpperCase().includes(this.search)
        ) {
          //  Se introduce en cada vuelta del for los datos de cada tienda que cumpla la anterior condición
          this.aftersearch.push(this.stores[i]);
        }
      }
      //  Si la cantidad de tiendas que alberga la búsqueda es menor a 1 se asigna true a la variable 'noresults', activar 'noresults' proporciona la ventaja de saber si hay o no resultados
      if (this.aftersearch.length < 1) {
        this.noresults = true;
      }
      //  De lo contrario se asigna false a la variable 'noresults', se guarda la cantidad de resultados en 'amountresults' y se asigna false a la variable 'findstore', para poder ocultar el banner de búsqueda.
      else {
        this.noresults = false;
        this.amountresults = this.aftersearch.length;
        this.findstore = false;
      }
    },
    //  Función maprute(), recibirá como parametro el contenido de la ubicación de la tienda que ha sido seleccionada y tratará dicha información para obtener como resultado la ruta dinámica a introducir en el iframe de GoogleMaps
    maprute(whereis) {
      //  Se vacia la variable 'where' y se crea una constante  'newreplace'  con un array vacio
      this.where = "";
      const newreplace = [];
      //  Se recorre la ubicación proporcionada con el motivo de encontrar los espacios del string y sustituirlos por '%20' y por cada vuelta se irá alojando en 'newreplace' el contenido a transformar a posterior
      for (let i = 0; i < whereis.length; i++) {
        newreplace.push(whereis[i].replace(" ", "%20"));
      }
      // Se transforma el array en un string con el uso de join: une todos los elementos de una matriz en una cadena de texto y devuelve esa cadena para asignarla a una variable a ser utilizada
      this.where = newreplace.join("");
    },
  },
};
</script>
<style scoped>
.dropdown-item {
  font-size: 1em;
  padding-left: 6em;
  margin-top: -1em;
  margin-bottom: 2em;
}
.dropdown-item:hover {
  background: none;
}
</style>
