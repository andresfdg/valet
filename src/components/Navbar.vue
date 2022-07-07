<template>
  <nav class="navbar navbar-expand-lg bg-light">
    <div class="container-fluid">
      <img src="../assets/logo-194.png" alt="" />
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarTogglerDemo02"
        aria-controls="navbarTogglerDemo02"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarTogglerDemo02">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link
              to="/"
              class="nav-link active btn btn-light"
              aria-current="page"
              ><h3>Home</h3></router-link
            >
          </li>
          <li class="nav-item">
            <router-link
              to="/about"
              class="nav-link active btn btn-warning"
              aria-current="page"
              ><h3>Calculate</h3>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {};
</script>

<style scoped>
.navbar {
  background-color: blueviolet;
  text-align: center;
}

h1 {
  font-size: 50px;
}
</style>
