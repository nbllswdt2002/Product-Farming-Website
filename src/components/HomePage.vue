<template>
  <div class="container-fluid m-0 p-0">
    <div id="home-page" class="full-height p-4">
      <div class="container pt-3">
        <div class="row pb-5">
          <div class="col-lg-6 pt-4 my-auto">
            <img id="iphone-img" src="../assets/logo/RESTOE BUMI (11).png" class="img-fluig">
          </div>
          <div class="col-lg-6 pt-4 my-auto">
            <div class="text-center mb-3 d-none d-lg-block">
              <h1 class="display-3">{{title}}</h1>
              <h3>Dapatkan Sayuran Hidroponik Sekarang Juga!</h3>
            </div>
          </div>
          <div class="border p-3 p-md-5 bg-white rounded shadow">
            <h2>Coming Soon!</h2>
            <form @submit.prevent="addEmail(email)">
              <div class="form-group">
                <label for="emailSignup">Punya Akun? Daftarkan Sekarang Juga</label>
                  <input v-model="email" type="email" id="emailSignup" placeholder="Masukkan Email" class="form-control">
                  <small id="emailHelp" class="form-text text-muted">Tidak Pernah Membagikan Alamat Email</small>
                <button type="submit" class="btn btn-success mt-3">Bergabung</button>
                  <div class="mt-4">
                    <p class="m-0">{{message}}</p>
                  </div>
              </div>
            </form>
          </div>
          <div id="available" class="p-2">
            <h4 class="text-center mb-2 mt-3 text-light">
              Available On:
            </h4>
            <div class="row">
              <div class="col my-auto">
                <img src="../assets/google_play.png" class="float-right img-fluid app_store_img">
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div id="about" class="bg-light p-3 p-md-5">
      <div class="row">
        <div class="col-lg">
          <img src="../assets/icons/makanan_sayur.png" height="120" class="m-4">
          <h5>Sehat Tentang Sayuran</h5>
          <h5 class="ml-md-4 mr-md-4">
            Sehat Tentang Sayuran membahas tentang kesehatan yang ada di kandungan sayuran serta memberikan manfaat-manfaat.
          </h5>
        </div>
        <div class="col-lg">
          <img src="../assets/icons/galeri_logo.png" height="110" class="m-4">
          <h5>Galeri Sayuran</h5>
          <h5 class="ml-md-4 mr-md-4">
          Galeri Sayuran berisi tentang produk yang dihasilkan dari restoe bumi.
          </h5>
        </div>
      </div>
    </div>

    <div id="contact" class=" p-4">
      <div class="row justify-content-center mt-3 mb-3">
        <div class="col-lg-4">
          <h2>Punya Pertanyaan?</h2>
          <p>Tanyakan Seputar Tentang Produk dari RestoeBumi</p>
            <form>
              <div class="form-group text-left">
                <input type="email" class="form-control" placeholder="Masukkan Alamat Email">
                <textarea class="form-control mt-3" placeholder="Masukkan Pesan Anda" rows="5">
                </textarea>
              </div>
                <button type="submit" class="btn btn-primary">
                  Kirim Pesan
                </button>
            </form>
        </div>
      </div>
    </div>

    <div id="footer" class=" p-4">
      <footer>
        <!-- <a href="#" target="_blank" class="text-warning">Build This App</a> |-->
        <a href="#" class="text-warning">Privacy Policy</a>
        <br>
        <small>&copy; 2020, RestoeBumi.app</small>
      </footer>
    </div>

  </div>
</template>

<script>
import {Auth} from '@/firebase/auth.js'
export default {
  data () {
    return {
        count: 0,
        title: 'Sayuran Hidroponik',
        email: '',
        message: ''
      }
  },
    methods: {
      async addEmail(email) {
        var noticeMessage = "Akun Kamu Telah Didapatkan"
        await Auth.createUserWithEmailAndPassword(email, this.randomPassword(20)).catch(function(error){
          if (error.code != "auth/email-already-in-use"){
            noticeMessage = error.message;
          }
        });
          this.message = noticeMessage;
          this.email = '';
        // await this.randomPassword(10);
      },

        randomPassword(length){
          var chars = "abcdefghijklmnopqrstuvwxyz!@#$%^&*()-+<>ABCDEFGHIJKLMNOP1234567890";
          var password = "";
          for(var x = 0; x < length; x++){
            var i = (Math.floor(Math.random() * chars.length));
            password += chars.charAt(i);
          }
            return password;
            // console.log(password);
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#home-page{
  background-color: #7FFF00;
  background: url('../assets/alam_hijau.png') no-repeat center center;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

#iphone-img{
  max-height: 30vh;
}

#about{
  min-height: 40vh;
}

#contact{
  background-color: #57AEAF;
}

#footer{
  background-color: #252223;
}

.app_store_img{
  max-height: 80px;
}
</style>
