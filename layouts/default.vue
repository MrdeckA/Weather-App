<template>
  <div>
    <!--Main Part of My Layout-->
    <div>
      <!--My Navbar-->
      <div>
        <div id="mynavbar">
          <nav
            class="navbar navbar-expand-sm navbar-dark bg-dark pt-0 pt-md-3"
            aria-label="Third navbar example"
          >
            <div class="col-1"></div>
            <div class="container-fluid">
              <div class="">
                <a class="navbar-brand fw-bold display-1 fs-2 pt-0" href="#"
                  >Weather'App</a
                >
              </div>
              <button
                class="navbar-toggler"
                type="button"
                data-bs-toggle="collapse"
                data-bs-target="#navbarsExample03"
                aria-controls="navbarsExample03"
                aria-expanded="false"
                aria-label="Toggle navigation"
              >
                <span class="navbar-toggler-icon"></span>
              </button>

              <div
                id="navbarsExample03"
                class="col-md-4 collapse navbar-collapse text-center pt-0"
              >
                <a class="btn btn-outline-secondary me-3 text-white" href="#">
                  Acceuil
                </a>
                <a class="btn btn-primary me-3 text-white" href="#foot">
                  A propos
                </a>
              </div>
            </div>
          </nav>
        </div>
      </div>

      <!--My Spinner / Loader -->
      <center v-if="spin" style="margin-top: 30vh">
        <div class="flower-spinner">
          <div class="dots-container">
            <div class="bigger-dot">
              <div class="smaller-dot"></div>
            </div>
          </div>
        </div>
        <div class="mt-5 display-1">
          <h4>Weather'App</h4>
        </div>
        <div class="mt-5 display-1 forme">
          <h4>by Mrdeck...</h4>
        </div>
        <div class="mt-5 display-1">
          <h4>Veuillez Patienter Quelques secondes !</h4>
        </div>
      </center>
    </div>

    <!--Body of my Layout-->
    <div v-if="!spin">
      <Nuxt />
    </div>

    <!--Footer-->
    <myFooter v-if="!spin" id="foot" class="mt-5" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      spin: true,
    }
  },
  beforeMount() {
    setTimeout(() => {
      this.spin = false
    }, 3000)
  },
}
</script>

<style scoped>
.forme {
  font-family: 'Comic Sans MS', 'Segoe UI', Tahoma, sans-serif;
}

.flower-spinner,
.flower-spinner * {
  box-sizing: border-box;
}

.flower-spinner {
  height: 70px;
  width: 70px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

.flower-spinner .dots-container {
  height: calc(70px / 7);
  width: calc(70px / 7);
}

.flower-spinner .smaller-dot {
  background: #ff1d5e;
  height: 100%;
  width: 100%;
  border-radius: 50%;
  animation: flower-spinner-smaller-dot-animation 2.5s 0s infinite both;
}

.flower-spinner .bigger-dot {
  background: #ff1d5e;
  height: 100%;
  width: 100%;
  padding: 10%;
  border-radius: 50%;
  animation: flower-spinner-bigger-dot-animation 2.5s 0s infinite both;
}

@keyframes flower-spinner-bigger-dot-animation {
  0%,
  100% {
    box-shadow: rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px;
  }

  50% {
    transform: rotate(180deg);
  }

  25%,
  75% {
    box-shadow: rgb(255, 29, 94) 26px 0px 0px, rgb(255, 29, 94) -26px 0px 0px,
      rgb(255, 29, 94) 0px 26px 0px, rgb(255, 29, 94) 0px -26px 0px,
      rgb(255, 29, 94) 19px -19px 0px, rgb(255, 29, 94) 19px 19px 0px,
      rgb(255, 29, 94) -19px -19px 0px, rgb(255, 29, 94) -19px 19px 0px;
  }

  100% {
    transform: rotate(360deg);
    box-shadow: rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px;
  }
}

@keyframes flower-spinner-smaller-dot-animation {
  0%,
  100% {
    box-shadow: rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px;
  }

  25%,
  75% {
    box-shadow: rgb(255, 29, 94) 14px 0px 0px, rgb(255, 29, 94) -14px 0px 0px,
      rgb(255, 29, 94) 0px 14px 0px, rgb(255, 29, 94) 0px -14px 0px,
      rgb(255, 29, 94) 10px -10px 0px, rgb(255, 29, 94) 10px 10px 0px,
      rgb(255, 29, 94) -10px -10px 0px, rgb(255, 29, 94) -10px 10px 0px;
  }

  100% {
    box-shadow: rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px,
      rgb(255, 29, 94) 0px 0px 0px, rgb(255, 29, 94) 0px 0px 0px;
  }
}
</style>