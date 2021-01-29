<template>
<nav class="navbar navbar-expand-lg navbar-dark bg-dark mt-5">
  <router-link class="navbar-brand" to="/"
        ><i class="fas fa-virus text-danger"></i> Live COVID-19 Vaccination
        Tracker</router-link
      >
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <router-link class="nav-link active" aria-current="page" to="/about"
        >About</router-link
      >
    </ul>
  </div>
</nav>
</template>
<script>
export default {};
</script>
<style lang=""></style>
