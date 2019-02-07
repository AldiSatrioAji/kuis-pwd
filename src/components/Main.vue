<template>
  <div class="hello">
    <h1><b>Selamat Mengerjakan</b></h1>
    <h1>Skor : {{skor}}</h1>
    <template v-if="isMessageEnabled">
      <h1 v-if="skor > 70">Kamu lulus!</h1>
      <h1 v-else>Ayo Semangat!</h1>
    </template>
    <div v-for="(item, index) in soal" :key="index">
      <h2>
        {{ item.index }}.
        {{ item.pertanyaan }}
      </h2>
      <li v-for="(opsi, index2) in item.list_jawaban" :key="index2">
        <input type="radio" :name="index" @click="addScore(index, index2)" :value="opsi"> {{ opsi.jawaban }}
      </li>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      skor : 0,
      isMessageEnabled: false,
      jawabanBenar: [],
      soal : [
        {
          index : 1,
          pertanyaan : 'Presiden pertama Indonesia ? ',
          list_jawaban : [
            {jawaban : 'Soekarno', benar: true},
            {jawaban : 'Soeharto'},
            {jawaban : 'Soegiman'},
            {jawaban : 'R.A Kartini'},
          ]
        },{
          index : 2,
          pertanyaan : 'Apa itu SIUP ? ',
          list_jawaban : [
            {jawaban : 'Surat Izin Usaha Perdagangan', benar: true},
            {jawaban : 'Surat Izin Tempat Usaha'},
            {jawaban : 'Surat Tanah'},
            {jawaban : 'Surat Hak Milik'},
          ]
        },{
          index : 3,
          pertanyaan : '20 + 7 = ? ',
          list_jawaban : [
            {jawaban : '32'},
            {jawaban : '27', benar: true},
            {jawaban : '55'},
            {jawaban : '66'},
          ]
        },{
          index : 4,
          pertanyaan : 'Apa warna bendera Indonesia ? ',
          list_jawaban : [
            {jawaban : 'Merah dan Putih', benar: true},
            {jawaban : 'Hitam dan Putih'},
            {jawaban : 'Biru dan Hijau'},
            {jawaban : 'Merah dan Hitam'},
          ]
        },{
          index : 5,
          pertanyaan : 'Yerusalem adalah Ibu kota dari Negara ? ',
          list_jawaban : [
            {jawaban : 'Amerika'},
            {jawaban : 'India'},
            {jawaban : 'Palestina', benar: true},
            {jawaban : 'Somalia'},
          ]
        },{
          index : 6,
          pertanyaan : 'Indonesia merdeka pada tahun ? ',
          list_jawaban : [
            {jawaban : '2027'},
            {jawaban : '1914'},
            {jawaban : '1927'},
            {jawaban : '1945', benar: true},
          ]
        },{
          index : 7,
          pertanyaan : 'Apa ideologi yang dianut Indonesia ? ',
          list_jawaban : [
            {jawaban : 'Komunis'},
            {jawaban : 'Pancasila', benar: true},
            {jawaban : 'Kapitalis'},
            {jawaban : 'Liberal'},
          ]
        },{
          index : 8,
          pertanyaan : '9 * 3 = ? ',
          list_jawaban : [
            {jawaban : '25'},
            {jawaban : '52'},
            {jawaban : '27', benar: true},
            {jawaban : '58'},
          ]
        },{
          index : 9,
          pertanyaan : 'Berapa pecahan 7/9 ? ',
          list_jawaban : [
            {jawaban : '0,78', benar: true},
            {jawaban : '1,88'},
            {jawaban : '0,99'},
            {jawaban : '0,75'},
          ]
        },{
          index : 10,
          pertanyaan : 'Benda yang menghantarkan listrik adalah ? ',
          list_jawaban : [
            {jawaban : 'Isolator'},
            {jawaban : 'Kalkulator'},
            {jawaban : 'Konduktor', benar: true},
            {jawaban : 'Detonator'},
          ]
        }
      ]
    }
  },
  methods : {
    pertanyaanNumber: function(index) {
      return index + 1;
    },
    addJawabanBenar: function(list) {
      this.jawabanBenar.push(list);
    },
    addScore: function(indexsoal, indexpilihan){
      this.isMessageEnabled = true;
      if(this.soal[indexsoal].list_jawaban[indexpilihan]['benar']){
        if(this.jawabanBenar.indexOf(indexsoal) == -1 ){
          this.jawabanBenar.push(indexsoal);
          this.skor+=10;
        }
      }else{
        if(this.jawabanBenar.indexOf(indexsoal) != -1 ){
          this.jawabanBenar.splice(this.jawabanBenar.indexOf(indexsoal), 1);
          this.skor-=10;
        }
      }
    }
  },
  computed: {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
