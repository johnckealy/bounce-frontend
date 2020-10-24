<template>
  <div class="section has-background-info">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <nuxt-link class="navbar-item" to="/"><strong>BOUNCE</strong></nuxt-link>
        <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbarBasic">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div id="navbarBasic" class="navbar-menu">
        <div class="navbar-end">
          <div class="navbar-item">
            <a class="button is-primary" href="https://github.com/cfahlgren1/Bounce" target="_blank" style="padding-left: 2.5rem;">
              <span class="icon has-text-dark" >
                <fa class="fa-icon" :icon="['fab', 'github']"/>
              </span>
              Contribute
            </a>
          </div>
          <div class="navbar-item">
            <div class="buttons">
              <nuxt-link class="button is-info"  to="/courts" >
                <strong>View Courts</strong>
              </nuxt-link>
            </div>
          </div>
        </div>
      </div>
    </nav>
  </div>
</template>


<script>

export default {

  name: 'Navbar', 

}

</script>


<style>
.fa-icon {
  margin-right: 2.5rem;
  font-size: 1.4rem;
}
</style>
