<template>
  <b-container fluid class="p-4">
     <b-row>

       <b-form-file v-model="file2" accept="image/*" class="mt-3" plain ref="myFiles" @change="onFileChange"></b-form-file>

      <div class="mt-3">Selected file: {{file2 && file2.name}}</div>
     </b-row>
    <b-row>
      <!-- the modal -->
      <b-modal id="myModal" title="Image">
        <img :src="srcImage" class="zoomodal img-fluid "  alt="">
      </b-modal>
      <div v-b-modal.myModal class="col-lg-3 col-md-4 col-xs-6 thumb" v-for="item in items">
         <a href="#" v-on:click="exibeImagem(item)" class="fancybox" rel="ligthbox">
         <b-img thumbnail fluid :src="item" class="zoom img-fluid "  alt=""/>
         </a>
      </div>
    </b-row>
  </b-container>
</template>
<script>
   export default {
     name: 'app',
     data () {
       return {
         file2 : null,
         files: [],
         dismissSecs: 10,
         dismissCountDown: 0,
         showDismissibleAlert: false,
         srcImage: '',
         items: []
       }
     },
     methods: {
       exibeImagem(e) {
         this.srcImage = e;
       },
       onFileChange(e) {
          
          const file = e.target.files[0];

          if(file!=null){
            this.items = [];  
            const url = URL.createObjectURL(file);
            for(var i=0; i<=9; i++){
              this.items.push(url);
            }
          }         
      }
     }
   }
</script>
<style lang="scss">
   body {
   background-color:#f1f1f1 !important;
   }
   #demo {
   height:100%;
   position:relative;
   overflow:hidden;
   }
   .green{
   background-color:#6fb936;
   }
   .thumb{
   margin-bottom: 30px;
   }
   .page-top{
   margin-top:85px;
   }
   img.zoom {
   width: 100%;
   height: 200px;
   border-radius:5px;
   object-fit:cover;
   -webkit-transition: all .3s ease-in-out;
   -moz-transition: all .3s ease-in-out;
   -o-transition: all .3s ease-in-out;
   -ms-transition: all .3s ease-in-out;
   }
   img.zoomodal {
   width: 100%;
   border-radius:2px;
   object-fit:cover;
   -webkit-transition: all .3s ease-in-out;
   -moz-transition: all .3s ease-in-out;
   -o-transition: all .3s ease-in-out;
   -ms-transition: all .3s ease-in-out;
   }
   .transition {
   -webkit-transform: scale(1.2); 
   -moz-transform: scale(1.2);
   -o-transform: scale(1.2);
   transform: scale(1.2);
   }
   .modal-header {
   border-bottom: none;
   }
   .modal-title {
   color:#000;
   }
   .modal-footer{
   display:none;  
   }
</style>