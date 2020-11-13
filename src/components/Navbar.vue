<template>
  <div>
      <b-navbar toggleable="lg" type="light">
        <div class="container">
          <b-navbar-brand href="/">Kuliner</b-navbar-brand>

          <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

          <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
              <li class="nav-item active">
                <router-link class="nav-link" to="/">Home</router-link>
              </li>
              <li class="nav-item">
                <router-link class="nav-link" to="/foods">Foods</router-link>
              </li>
            </b-navbar-nav>

            <!-- Right aligned nav items -->
            <b-navbar-nav class="ml-auto">
              <li>
                <router-link class="nav-link" to="/keranjang">
                  Keranjang
                  <b-icon-bag></b-icon-bag>
                  <span class="badge badge-success ml-2">{{
                    updateKeranjang
                      ? updateKeranjang.length
                      : jumlah_pesanans.length
                  }}</span>
                </router-link>
              </li>
            </b-navbar-nav>
          </b-collapse>
        </div>
      </b-navbar>
    </div>

    <!-- <nav class="navbar navbar-expand-lg navbar-light">
            <div class="container">
                <a class="navbar-brand" href="/">Kulineran</a>
                <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown"
                    aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarNavDropdown">
                    <ul class="navbar-nav">
                        <li class="nav-item active">
                            <router-link class="nav-link" to="/">Home</router-link>
                        </li>
                        <li class="nav-item">
                            <router-link class="nav-link" to="/foods">Foods</router-link>
                        </li>
                    </ul>
                    <ul class="navbar-nav ml-auto">
                        <li>
                            <router-link class="nav-link" to="/keranjang">
                                Keranjang
                                <b-icon-bag></b-icon-bag>
                                <span class="badge badge-success ml-2">{{ updateKeranjang ? updateKeranjang.length : jumlah_pesanans.length }}</span>
                            </router-link>
                        </li>
                    </ul>
                </div>
            </div>
        </nav> -->
</template>
<script>
import axios from "axios";
export default {
  name: "Navbar",
  data() {
    return {
      jumlah_pesanans: [],
    };
  },
  props: ["updateKeranjang"],
  methods: {
    setJumlah(data) {
      this.jumlah_pesanans = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((res) => this.setJumlah(res.data))
      .catch((err) => console.log(err));
  },
};
</script>
