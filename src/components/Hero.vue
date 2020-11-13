<template>
    <div class="hero">
        <!-- Dekstop -->
         <!-- Untuk menyembunyikan jika sedang di versi Mobile -->
        <div class="d-none d-md-block">
            <div class="row mt-3">
                <div class="col-md-6">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2><strong>Delicious Food Menu, </strong><br>in Your Gadget</h2>
                            <p>Ayo segera pilih dan pesan makanan favorit anda</p>
                            <router-link class="btn btn-sm btn-success" to="/foods">
                                <b-icon-arrow-right></b-icon-arrow-right>Pesan
                            </router-link>
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <img src="../assets/images/Hero.png" width="100%" />
                </div>
            </div>
        </div>

        <!-- Mobile -->
        <!-- Untuk menyembunyikan jika sedang di versi Dekstop -->
        <div class="d-sm-block d-md-none">
            <div class="row mt-4">
                <div class="col-md-6 mb-2">
                    <img src="../assets/images/Hero.png" width="100%" />
                </div>
                <div class="col-md-6">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2><strong>Delicious Food Menu, </strong><br>in Your Gadget</h2>
                            <p>Ayo segera pilih dan pesan makanan favorit anda</p>
                            <button class="btn btn-sm btn-success">
                                <b-icon-arrow-right></b-icon-arrow-right>Pesan
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- /Hero -->
    </div>


</template>
<script>
    export default {
        name: 'Hero'
    }
</script>