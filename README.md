# Ujian App

![](https://cdn.shopify.com/s/files/1/0533/2089/files/vuejs-tutorial_2d2a853c-aa2f-44b0-80df-933b495f77f8.png?v=1509478492)

User akan mengisi 10 pertanyaan ujian dengan materi yang berbeda-beda. Dalam projek ini kita dapat melihat penggunaan **v-for**, event **@click**, **v-if** dan method **push**.

## Komponen yang digunakan
- [vue-webpack](https://github.com/vuejs-templates/webpack "Informasi tentang Webpack")

## Instalasi Webpack

``` bash
$ npm install -g vue-cli
$ vue init webpack my-project
$ cd my-project
$ npm install
```
Menjalankan projek :

```bash
$ npm run dev
```

## Bedah kode
#### Menampilkan skor
Untuk menampilkan jumlah skor yang didapat, panggil nama variabel nya di dalam **double kurung kurawal** :
```html
<h1>Skor : {{ skor }}</h1>
```
Inisialisasikan variabel skor di **script** :
```javascript
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      skor : 0,
	  .......
}
  }
 </script>
```

#### Menampilkan keterangan
Jika nilai/skor lebih dari **70** maka akan menampilkan keterangan **Kamu Lulus** sebaliknya maka akan menampilkan keterangan **Ayo Semangat!**. variabel **isMessageEnabled** berperan untuk menampilkan **keterangan** apabila user meng-klik pertama kali jawabannya. Hal ini untuk mencegah user melihat keterangannya terlebih dahulu sebelum memilih jawaban pertamanya  :
```html
<template v-if="isMessageEnabled">
	<h1 v-if="skor > 70">Kamu lulus!</h1>
	<h1 v-else>Ayo Semangat!</h1>
</template>
```
Inisialisasikan variabel **isMessageEnabled** di **script** :
```javascript
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      skor : 0,
	  isMessageEnabled: false,
	}
  }
 </script>
```
#### Menampilkan pertanyaan
***Mapping*** pertanyaan menggunakan **v-for** :
```html
<div v-for="(item, index) in soal" :key="index">
      <h2>
        {{ item.index }}.
        {{ item.pertanyaan }}
      </h2>
      <li v-for="(opsi, index2) in item.list_jawaban" :key="index2">
        <input type="radio" :name="index" @click="addScore(index, index2)" :value="opsi"> {{ opsi.jawaban }}
      </li>
</div>
```
***Resource* pertanyaan dan jawaban**. Untuk mengecek benar atau salahnya suatu jawaban, ditambahkan variabel **benar** dengan nilai **true**
```javascript
soal : [
        {
          index : 1
          pertanyaan : 'Presiden pertama Indonesia ? ',
          list_jawaban : [
            {jawaban : 'Soekarno', benar: true},
            {jawaban : 'Soeharto'},
            {jawaban : 'Soegiman'},
            {jawaban : 'R.A Kartini'},
          ]
        }, ....
]
```

nilai **item** merujuk ke sebuah **objek** **pertanyaan**, sedangkan **index** merujuk ke urutan/nomer **objek** :
```html
<div v-for="(item, index) in soal" :key="index">
```
Menampilkan **nomor** beserta **pertanyaan** : 
```html
<h2>
	{{ item.index }}.
	{{ item.pertanyaan }}
</h2>
```
***Mapping*** jawaban. Event **@click** untuk menerapkan aksi klik pada radio button dan akan memanggil sekaligus mem-***passing***  data **index** dan **index2** ke method **addScore()** yang nantinya akan men-**set** nilai variabel **skor**.
```javascript
<li v-for="(opsi, index2) in item.list_jawaban" :key="index2">
<input type="radio" :name="index" @click="addScore(index, index2)" :value="opsi"> {{ opsi.jawaban }}
</li>
```


#### 
pada **line** ke-3,  akan mencek apakah jawaban benar. Jika iya, maka akan menambahkan data yang benar ke **array** jawabanBenar dengan method **push** dan menambahkan skor/nilai sebesar 10. Jika salah, maka akan me-**remove** data dengan menggunakan method **splice**.
```javascript
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
```
