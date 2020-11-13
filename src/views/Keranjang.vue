<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjangs" />
    <div class="container">
      <div class="row">
        <div class="col-6 mt-3 mb-3">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="font-color">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="font-color">Cart</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Foods Order
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <table class=" table table-bordered ">
            <thead>
              <tr>
                <th>#</th>
                <th>Gambar</th>
                <th>Makanan</th>
                <th>Keterangan</th>
                <th>Jumlah</th>
                <th>Harga</th>
                <th>Total Harga</th>
                <th>Hapus</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
                <td>{{ index + 1 }}</td>
                <td>
                  <img
                    :src="'../assets/images/' + keranjang.products.gambar"
                    class="img-fluid"
                    alt=""
                    width="200"
                  />
                </td>
                <td>
                  <strong>{{ keranjang.products.nama }}</strong>
                </td>
                <td>{{ keranjang.keterangan ? keranjang.keterangan : "-" }}</td>
                <td>{{ keranjang.jumlah_pemesanan }}</td>
                <td>Rp. {{ keranjang.products.harga }}</td>
                <td>
                  Rp.{{ keranjang.products.harga * keranjang.jumlah_pemesanan }}
                </td>
                <td align="center" class="text-danger">
                  <b-icon-trash
                    @click="hapusKeranjang(keranjang.id)"
                  ></b-icon-trash>
                </td>
              </tr>
              <tr>
                <td colspan="6" align="right">Total Harga :</td>
                <td>
                  <strong>{{ totalHarga }}</strong>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- Form CheckOut -->
      <div class="row justify-content-end">
        <form v-on:submit.prevent>
          <div class="form-group">
            <label for="nama">Nama :</label>
            <input type="tezt" class="form-control" v-model="pesan.nama" />
          </div>
          <div class="form-group">
            <label for="noMeja">No Meja :</label>
            <input type="number" class="form-control" v-model="pesan.noMeja" />
          </div>
          <button type="submit" class="btn btn-success" @click="checkout">
            <b-icon-cart></b-icon-cart>Pesan
          </button>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";
export default {
  name: "Keranjang",
  components: {
    Navbar,
  },
  data() {
    return {
      keranjangs: [],
      pesan: {},
    };
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$toast.error("Pesanan Berhasil Di Hapus", {
            // optional options Object
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });
          axios
            .get("http://localhost:3000/keranjangs")
            .then((response) =>
              // handle success
              this.setKeranjangs(response.data)
            )
            .catch(function(error) {
              // handle error
              console.log(error);
            });
        })
        .catch((error) => console.log(error));
    },
    checkout() {
      if (this.pesan.nama && this.pesan.noMeja) {
        this.pesan.keranjangs = this.keranjangs;
        axios
          .post("http://localhost:3000/pesanans", this.pesan)
          .then(() => {
            // Hapus Semua Keranjang
            this.keranjangs.map(function (item) {
              return axios
              .delete("http://localhost:3000/keranjangs/" + item.id)
              .catch(function(error) {
              // handle error
              console.log(error);
            });
            });
            this.$router.push({path : "/pesanan-sukses" })
            this.$toast.success("Berhasil Di Pesan.", {
              // optional options Object
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log("data", err));
      } else {
        this.$toast.error("Nama Dan NoMeja Harus Diisi!!", {
          // optional options Object
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    // Make a request for a user with a given ID
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) =>
        // handle success
        this.setKeranjangs(response.data)
      )
      .catch(function(error) {
        // handle error
        console.log(error);
      });
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(function(items, data) {
        return items + data.products.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>
