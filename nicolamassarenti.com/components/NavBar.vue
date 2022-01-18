<template>
  <div>
    <!-- As a heading -->
    <b-navbar variant="faded" type="light">
    <b-navbar-toggle target="nav-text-collapse"></b-navbar-toggle>
      <b-navbar-brand tag="h1" class="mb-0" to="/">NM</b-navbar-brand>

        <b-navbar-nav class="ml-auto">
            <b-nav-text>Navbar text</b-nav-text>
            <b-nav-text>Navbar text</b-nav-text>
            <b-nav-text>Navbar text</b-nav-text>
        </b-navbar-nav>

      <b-collapse id="nav-text-collapse" is-nav>
        <b-navbar-nav right>
          <b-nav-text>Navbar text</b-nav-text>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>


<style>
.nuxt-logo {
  height: 180px;
}
</style>
