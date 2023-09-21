<template>
  <header>
    <div
      style="
        position: fixed;
        background-color: white;
        z-index: 1;
        width: 100%;
        height: 8em;
      "
      class="row cover-container d-flex p-3 mx-auto shadow-sm"
    >
      <image
        style="padding-left: 2em; padding-top: 1em"
        src="cropped-arena-logo.png"
        class="col-1 float-md-start mb-5"
      />
      <nav
        style="justify-content: center; font-size: 1.15em"
        class="col-11 nav"
      >
        <a
          style="color: black"
          class="nav-link fw-bold py-1 active"
          aria-current="page"
          href="/"
          >Home</a
        >
        <a style="color: black" class="nav-link fw-bold py-1" href="/locations"
          >Tiendas</a
        >
        <!--<a style="color:black;" class="nav-link fw-bold py-1" href="/change">Modificar datos</a>-->
      </nav>
    </div>
  </header>
  <router-view />
  <footer style="bottom: 0; width: 100%; margin-top: 6em">
    <section
      class="row"
      style="
        height: 20em;
        background-color: black;
        color: white;
        list-style: none;
      "
    >
      <div class="col-3"></div>
      <article style="margin-top: 6em" class="col-1">
        <a href="http://www.m-automocion.com." target="_blank">
          <img
            src="M-Automocion-blanco.png"
            title="M-Automocion-blanco"
            alt="M-Automocion-blanco"
            loading="lazy"
          />
        </a>
      </article>
      <article style="margin-top: 5em" class="col-1">
        <img
          src="arena-blanco.png"
          title="Motos eléctricas de ciudad Arena"
          alt="Motos eléctricas de ciudad Arena"
          loading="lazy"
        />
      </article>
      <article class="col-3">
        <nav style="text-align: left; margin-top: 2.5em">
          <a class="row" href="https://arenamotor.es/condiciones-generales/"
            >Condiciones generales</a
          >
          <a class="row" href="https://arenamotor.es/condiciones-generales/"
            >Cancelación de pedidos</a
          >
          <a class="row" href="https://arenamotor.es/condiciones-generales/"
            >Devolución y reembolso</a
          >
          <a class="row" href="https://arenamotor.es/condiciones-generales/"
            >Seguridad y Protección a compradores</a
          >
          <a class="row" href="https://arenamotor.es/condiciones-generales/"
            >Envíos</a
          >
          <a class="row" href="https://arenamotor.es/#FAQs">FAQs</a>
        </nav>
      </article>
      <article style="margin-top: 4em; text-align: left" class="col-2">
        <h5>CONTACTO</h5>
        <a
          style="text-decoration: none"
          class="row mb-1"
          href="https://goo.gl/maps/CfaBBSr9raGGYMabA"
          target="_blank"
        >
          <span style="color: white">Calle Aragón 499, Barcelona, 08013</span>
        </a>
        <a
          style="text-decoration: none"
          class="row mb-1"
          href="tel:%20+34%20938%2056%2077%2088"
        >
          <span style="color: white" class="elementor-icon-list-text"
            >+34 938 56 77 88</span
          >
        </a>
        <a
          style="text-decoration: none"
          class="row mb-1"
          href="mailto:%20info@arenamotor.es"
          target="_blank"
        >
          <span style="color: white">info@arenamotor.es</span>
        </a>
      </article>
      <div class="col"></div>
    </section>
  </footer>
</template>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  user-select: none;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: white;
  text-decoration: none;
}
nav a:hover {
  font-weight: bold;
  color: #bf9c58;
  transition-delay: 0.1s;
  transition-duration: 0.25s, 5s;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
