<template>
    <div class="pesanan-sukses">
        <Navbar />
        <div class="container">
            <div class="row justify-content-center mt-5">
                <div class="col text-center">
                    <img src="../assets/images/menunggu.png" alt="Menunggu" width="300">
                    <h2><strong>Suksess!!</strong></h2>
                    <h4>Pesanan Anda segera di proses <br> Selemat Menunggu</h4>
                </div>
            </div>
        </div>
       
    </div>
</template>
<script>
 import Navbar from "@/components/Navbar.vue";
export default {
    name: "PesananSukses",
    components : {
    Navbar,
    }
}
</script>