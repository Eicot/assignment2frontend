<template>
  <div class="home">
    <!-- homepage -->
    <div>
      <!-- Navbar Div -->
      <nav class="mainbar navbar navbar-expand-md body-tertiary">
        <div class="container-fluid">
          <!-- Web Logo -->
          <a class="navbar-brand" href="toMain"
            ><img src="./assets/cyclelogo.jpg" width="120" height="100" />
          </a>
          <!-- Collapse Button for mobile responsive -->
          
          <button
            class="navbar-toggler justify-content-end"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#mainbar"
            aria-controls="mainbar"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <!-- Navbar -->
          <div
            class="collapse navbar-collapse justify-content-end"
            id="mainbar"
          >
            <ul class="nav nav-tabs">
              <!-- To homepage -->
              <li class="nav-item">
                <button
                  class="nav-link active"
                  v-on:click="toMain"
                  type="button"
                  data-bs-toggle="tab"
                >
                  Home
                </button>
              </li>
              <!-- To addcycle page -->
              <li class="nav-item">
                <button
                  class="nav-link"
                  v-on:click="toAddNew"
                  type="button"
                  data-bs-toggle="tab"
                >
                  Add New <font-awesome-icon icon="fa-solid fa-motorcycle" />
                  <i class="fa-solid fa-motorcycle"></i>
                </button>
              </li>
              <!-- To aboutus page -->
              <li class="nav-item">
                <button
                  class="nav-link"
                  v-on:click="toAboutUs"
                  type="button"
                  data-bs-toggle="tab"
                >
                  About Us
                </button>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </div>
    <!-- Creating alert message for Add, edit or delete motorcycle -->
    <div>
      <div class="alert alert-succcess notification" v-if="showAlert">
        <!-- if showAlert is true, the alertmessage will display -->
        {{ alertMessage }}
      </div>
      <div>
        <main>
          <HomePage v-if="page == 'mainPage'" v-on:view-cycle="toSpec" />
          <!-- if click for view-cycle event, activate toSepc function -->
        </main>
        <AddCycle v-if="page == 'addNewPage'" v-on:cycle-added="cycleAdded" />
        <SpecPage
          v-if="page == 'specPage'"
          v-bind:cycleId="viewSpec"
          v-on:edit-cycle="toEdit"
          v-on:remove-cycle="deleteCycle"
          v-on:review-added="reviewAdded"
        />
        <EditCycle
          v-if="page == 'editPage'"
          v-bind:cycleId="editSpec"
          v-on:cycle-updated="cycleUpdated"
        />
        <AboutUsPage v-if="page == 'aboutUs'" />
      </div>
    </div>
  </div>
</template>

<script>
// impporting components
import HomePage from "./components/HomePage";
import AddCycle from "./components/AddCycle";
import SpecPage from "./components/SpecPage";
import EditCycle from "./components/EditCycle";
import AboutUsPage from "./components/AboutUsPage";

export default {
  name: "App",
  components: {
    HomePage,
    AddCycle,
    SpecPage,
    EditCycle,
    AboutUsPage,
  },
  data: function () {
    return {
      page: "mainPage",
      viewSpec: 0,
      editSpec: 0,
      alertMessage: "",
      showAlert: false,
    };
  },
  methods: {
    toMain: function () {
      this.page = "mainPage";
      this.showAlert = false;
    },
    toAddNew: function () {
      this.page = "addNewPage";
      this.showAlert = false;
    },
    cycleAdded: function () {
      this.page = "mainPage";
      this.alertMessage = "A new cycle has been added";
      this.showAlert = true;
      setTimeout(() => {
        // to show alertMessage during the set time
        this.showAlert = false;
      }, 2000);
    },
    toSpec: function (cycleId) {
      this.page = "specPage";
      this.viewSpec = cycleId;
      this.showAlert = false;
    },
    toEdit: function (cycleId) {
      this.page = "editPage";
      this.editSpec = cycleId;
      this.showAlert = false;
    },
    cycleUpdated: function () {
      this.page = "specPage";
      this.alertMessage = "The cycle has been updated";
      this.showAlert = true;
      setTimeout(() => {
        this.showAlert = false;
      }, 2000);
    },
    deleteCycle: function () {
      this.page = "mainPage";
      this.alertMessage = "The cycle has been deleted";
      this.showAlert = true;
      setTimeout(() => {
        this.showAlert = false;
      }, 2000);
    },
    reviewAdded: function () {
      this.page = "specPage";
      this.alertMessage = "A review has been added";
      this.showAlert = true;
      setTimeout(() => {
        this.showAlert = false;
      }, 2000);
    },
    toAboutUs: function () {
      this.page = "aboutUs";
      this.showAlert = false;
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.cdnfonts.com/css/motorcycle");
.home {
  background-image: url(https://c4.wallpaperflare.com/wallpaper/612/547/823/wall-brick-texture-units-wallpaper-preview.jpg);
  font-family: Rockwell;
  font-size: 20px;
}
main {
  margin-top: 120px;
  margin-left: 3rem;
  margin-right: 3rem;
  padding: 2rem;
}

.notification {
  background-color: #000000;
  color: white;
  padding: 16px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translateX(-50%);
  z-index: 9999;
}

.nav-link {
  color: rgb(0, 0, 0);
}

.mainbar {
  overflow: hidden;
  position: fixed; /* Set the navbar to fixed position */
  top: 0; /* Position the navbar at the top of the page */
  width: 100%; /* Full width */
  background-image: url(https://c4.wallpaperflare.com/wallpaper/612/547/823/wall-brick-texture-units-wallpaper-preview.jpg);
  z-index: 9999;
}

/* Change background on mouse-over */
.mainbar li:hover {
  background: rgba(0, 0, 0, 0.411);
}
</style>
