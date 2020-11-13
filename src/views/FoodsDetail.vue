<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="font-color">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="font-color">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Foods Order
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col-md-6">
          <img :src="'../assets/images/' + product.gambar" class="img-fluid" alt="">
        </div>
        <div class="col-md-6">
          <h2><strong>{{product.nama}}</strong></h2>
          <hr>
          <h4>Harga: <strong>Rp</strong> {{product.harga}}</h4>
          <!-- Fungsi Prevent Adalah Untuk Menhilangkan load pada website -->
          <form v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah_pesanan">Jumlah Pesanan</label>
              <input type="number" class="form-control" v-model="pesan.jumlah_pemesanan" />
            </div>
            <div class="form-group">
              <label for="keterangan">Keterangan</label>
              <textarea v-model="pesan.keterangan" class="form-control"
                placeholder="Keteranagan Seperti :Pedas, Nasi Setengah .."></textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart>Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import Navbar from "@/components/Navbar.vue";
  import axios from "axios";
  export default {
    name: "FoodsDetail",
    components: {
      Navbar,
    },
    data() {
      return {
        product: {},
        pesan: {}
      }
    },
    methods: {
      setProduct(data) {
        this.product = data
      },
      pemesanan() {
        if (this.pesan.jumlah_pemesanan) {
          this.pesan.products = this.product;
          axios
            .post("http://localhost:3000/keranjangs", this.pesan)
            .then(() => {
              this.$router.push({
                path: '/keranjang'
              })
              this.$toast.success('Sukses Masuk Keranjang.', {
                // optional options Object
                type: 'success',
                position: 'top-right',
                duration: 3000,
                dismissible: true
              })
            })
            .catch((err) => console.log("data", err))
        } else {
          this.$toast.error('Jumlah Pesanan Harus Diisi Terlebih Dahulu', {
            // optional options Object
            type: 'error',
            position: 'top-right',
            duration: 3000,
            dismissible: true
          })
        }
      }
    },
    mounted() {

      // Make a request for a user with a given ID
      axios.get("http://localhost:3000/products/" + this.$route.params.id)
        .then((response) =>
          // handle success
          this.setProduct(response.data))
        .catch(function (error) {
          // handle error
          console.log("data", error);
        })
    },
  };
</script>