<template>
  
  <div id="app">
    <div class="container">
      <div class="text-center">
        <h2>{{ title }}</h2>
        <p class="text-muted">{{ subtitle }}</p>
      </div>
    </div>
    <div class="container">
      <h5>Input Data Warga</h5>
      <hr>
      <form v-on:submit.prevent>
        <div id="inputDataSiswa">
          <div class="row">
            <div class="col-lg-6 col-md-6 col-sd-6">
              <div class="form-group">
                <label>Nama <span class="text-danger">*</span></label>
                <input type="text" name="nama" class="form-control" v-model="dataMasuk.nama">
              </div>
              <div class="form-group">
                <label>NIK <span class="text-danger">*</span></label>
                <input type="number" name="nonik" class="form-control" v-model="dataMasuk.nonik">
              </div>
              <div class="form-group">
                <label>Nomor Kartu Keluarga <span class="text-danger">*</span></label>
                <input type="number" name="nokk" class="form-control" v-model="dataMasuk.nokk">
              </div>
              <div class="form-group">
                <label>Foto KTP <span class="text-danger">*</span></label>
                <input type="file" name="ktp" id="fotoKTP" class="form-control-file">
              </div>
              <div class="form-group">
                <label>Foto Kartu Keluarga <span class="text-danger">*</span></label>
                <input type="file" name="kk" id="fotoKK" class="form-control-file">
              </div>
              <div class="form-group">
                <label>Umur <span class="text-danger">*</span></label>
                <input type="number" name="usia" class="form-control" v-model="dataMasuk.usia">
              </div>            
              <div class="form-group">
                <label>Jenis Kelamin <span class="text-danger">*</span></label>
                <div class="form-inline">
                  <input type="radio" name="jk" value='1' v-model="dataMasuk.jk">
                  <label class="pl-2" >Laki-Laki</label>
                </div>
                <div class="form-inline">
                  <input type="radio" name="jk" value='0' v-model="dataMasuk.jk">
                  <label class="pl-2">Perempuan</label>
                </div>
              </div>
            </div>
            <div class="col-lg-6 col-md-6 col-sd-12">
              <div class="form-group">
                <label>Alamat <span class="text-danger">*</span></label>
                <textarea class="form-control" name="alamat" rows="5" id="comment" v-model="dataMasuk.alamat"></textarea>
              </div>
              <div class="form-group">
                <label>RT <span class="text-danger">*</span></label>
                <input type="number" name="rt" class="form-control" v-model="dataMasuk.rt">
              </div>
              <div class="form-group">
                <label>RW <span class="text-danger">*</span></label>
                <input type="number" name="rw" class="form-control" v-model="dataMasuk.rw">
              </div>
              <div class="form-group">
                <label>Penghasilan sebelum pandemi <span class="text-danger">*</span></label>
                <input type="number" name="incomeBefore" class="form-control" v-model="dataMasuk.incomeBefore">
              </div>
              <div class="form-group">
                <label>Penghasilan setelah pandemi <span class="text-danger">*</span></label>
                <input type="number" name="incomeAfter" class="form-control" v-model="dataMasuk.incomeAfter">
              </div>
              <div class="form-group">
                <label>Alasan Membutuhkan Bantuan <span class="text-danger">*</span></label>
                <textarea class="form-control" name="alasanBantuan" rows="5" id="comment" style="resize:none;" v-model="dataMasuk.alasanBantuan"></textarea>
              </div>
            </div>
          </div>
        </div>
        <div class="form-group">
          <div class="form-inline">
            <input type="checkbox" class="form-check-input" value="1" v-model="dataMasuk.term">
            <label class="pl-2 label-checkbox" value='1'>Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut.</label>
          </div>        
        </div>
        
        <div class="text-center mt-3">
          <button type="submit" class="btn btn-outline-success text-center" @click="masukanData">No Rekening</button>
        </div>
      </form>
      
    </div>   
  </div>
</template>


<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data: function(){
    return{
      title:'TaWarPagar',
      subtitle:'Data Warga Pagarsih',
      user:'Admin',
      dataWarga:[],
      dataMasuk:[]
    }
  },
  methods:{
    masukanData(){
      console.log(this.dataMasuk);
      axios
      .post("https://my-json-server.typicode.com/rafifauzi/dataWarga/inputWarga", this.dataMasuk)
      .then(() => {console.log("Data Masuk");})
      .catch(function (error) {
    // handle error
    console.log('gagal :', error);
  })
    }
  },
  mounted(){
    axios.get('https://my-json-server.typicode.com/rafifauzi/dataWarga/dtWarga')
    .then(response => {
      // JSON responses are automatically parsed.
      this.dataWarga = response.data
      console.log("Berhasil : ", response);
    })
  }
}
</script>

