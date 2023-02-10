<template>

	<div>
    <div class="row text-center mb-1">
      <div class="col">
        <textarea v-model="text" class="form-control shadow-none h-100" rows="6" placeholder="Çevirmek istediğiniz cümleyi yada kelimeyi yazın."></textarea>
      </div>
    </div>
    <div class="row text-center mb-3">
      <div class="col">
        <select v-model="source" class="custom-select shadow-none">
          <option v-for="lg in languages" :value="lg.code">{{lg.name}}</option>
        </select>
      </div>
   <i @click="changeLang" class="fa-solid fa-repeat" style="margin-top: 9px; font-size: 18px;"></i>
    <div class="col">
      <select v-model="target" class="custom-select shadow-none">
        <option v-for="lg in languages" :value="lg.code">{{lg.name}}</option>
      </select>
    </div>
  </div>
  <div class="row text-center mb-3">
    <div class="col">
      <button @click="translate()" class="btn btn-info w-100">Çevir</button>
    </div>
  </div>
  <div class="row text-center">
    <div  v-for="(r,index) in results"  class="col-12">
      <span class="custom-span font-weight-bold text-success ">{{index+1}}) {{r.translation}}</span>
    </div>
    <!--<div v-if="results.length>0" class="col-12">
      <span class="custom-span font-weight-bold text-success ">{{results[0].translation}}</span>
    </div>-->

  </div>
</div>

</template>
<script>

  import axios from "axios"
  export default{
    data(){
      return {
        languages:[
        {name:"English",code:"en"},
        {name:"Spanish",code:"es"},
        {name:"French",code:"fr"},
        {name:"Japanese",code:"ja"},
        {name:"Italian",code:"it"},
        {name:"Portuguese",code:"pt"},
        {name:"Russian",code:"ru"},
        {name:"Turkish",code:"tr"},
        {name:"Ukrainian",code:"uk"},
        {name:"Chinese",code:"zh"},
        {name:"Swedish",code:"sv"},
        {name:"Slovak",code:"sk"},
        {name:"Romanian",code:"ro"},
        {name:"Dutch",code:"nl"},
        {name:"Latvian",code:"lv"},
        {name:"Korean",code:"ko"},
        {name:"Kannada",code:"kn"},
        {name:"Armenian",code:"hy"},
        {name:"Croatian",code:"hr"},
        {name:"Hungarian",code:"hu"},
        {name:"Greek",code:"el"},
        {name:"German",code:"de"},
        {name:"Czech",code:"cs"},
        {name:"Bulgarian",code:"bg"},
        {name:"Azeri",code:"az"},
        {name:"Arabic",code:"ar"},
        ],
        text:"",
        source:"tr",
        target:"en",
        results:[],
        RapidAPIKey:'rapidapi key gir',
        RapidAPIHost:'rapidapi host gir'
      }
    },
    methods:{
      changeLang(){
        const s = this.source
        const t = this.target
        this.source = t
        this.target = s
      },
      translate(){
        axios.get("https://translated-mymemory---translation-memory.p.rapidapi.com/get",{
          params:{langpair: this.source+'|'+this.target, q: this.text, mt: '1', onlyprivate: '0', de: 'a@b.c'},
          headers: {
            'X-RapidAPI-Key': this.RapidAPIKey,
            'X-RapidAPI-Host': this.RapidAPIHost
          }
        }).then((res)=>{
          //console.log(res.data.matches)
          this.results=res.data.matches
        })
      }
    }
  }
</script>
<style>
	.fa-repeat:hover{
    cursor: pointer;
    color: #28a745;
    transition: color .3s;
  }
</style>