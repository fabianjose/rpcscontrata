<template> 
  <div class="card card-primary filter-card mb-5 p-3" style="box-shadow: none;">
    <div class="card-body d-flex flex-column align-items-center   pt-4" style="box-shadow: none;">
      <div class="d-flex flex-column justify-content-between" style="width: 100%;">
      <!-- <div class="col-xl-2 col-lg-3 col-md-4 px-1" v-on:click="changeOrderPrice" style="cursor: pointer;">
            <div class="text-center p-2 offer-table-label w-100 text-white mx-auto bg-dark-blue rounded-pill p-1 text-wrap ">  <p class="text-tabla-detalles" >Precio <i class="fa fa-angle-down"></i></p> </div>
          </div> -->
      <h4  class="filter-card-title font-weight-bold text-center" style="align-self: center;" >
        <i class="fas fa-filter" style="color:#606060;display: inline-block;">    </i>
        Filtro de búsqueda</h4>
     </div>
         <br>

        <!--  <div class="form-group my-2 col-12 " v-if="orderBy" style="display: block;">
            <label for="sortBy" class="filter-card-label">Orden:</label>
            <select class="custom-select rounded-pill" id="sortBy" v-model="orderBySort">
              <option :value="'asc'" selected >Ascendente</option>
              <option :value="'desc'" >Descendente</option>
            </select>
          </div> -->
      <div class="form-horizontal my-2 col-12 flex-wrap" >
        <div  type="button" data-toggle="collapse" data-target="#collapseProveedor" aria-expanded="false" aria-controls="collapseProveedor" style="display:flex;justify-content: space-between;">
          <h4 class="btn-block" style="color:#616161; font-family:'Work Sans'; font-weight: 500;">  Proveedor   </h4> <span><i class="fas fa-angle-down" style="margin-left: auto; font-size: 33px;   color: #afaeb4;"></i></span>
        </div>
        <div class="collapse" id="collapseProveedor">
          <div class="card card-body" style="background-color: #f7f7f7;">
            <div v-for="(value) in providers">
              <input type="checkbox" :value="value.id" v-model="checked_providers">
              <label class="text-ws" style="color: #606060;"  >{{value.name}}</label>
            </div>
          </div>
        </div>
        <br>
      </div>
      <div class="form-horizontal my-2 col-12 flex-wrap">
        <div  type="button" data-toggle="collapse" data-target="#collapseTecnologia" aria-expanded="false" aria-controls="collapseTecnologia"  style="display:flex;justify-content: space-between;">
        <h4 class="btn-block" style="color:#616161; font-family:'Work Sans'; font-weight: 500;">  Tecnología   </h4> <span><i class="fas fa-angle-down" style="margin-left: auto; font-size: 33px;   color: #afaeb4;"></i></span>    
 
        </div>
        <div class="collapse" id="collapseTecnologia">
          <div class="card card-body" style="background-color: #f7f7f7;">
            <div v-for="(value) in technologies">
              <input type="checkbox" :value="value.type" v-model="checked_technologies">
               <label class="text-ws" style="color: #606060" v-if="value.type == 0 ">Fibra</label>
               <label class="text-ws" style="color: #606060"   v-if="value.type == 1 ">
           Satelital</label>
               <label class="text-ws" style="color: #606060"  v-if="value.type == 2 ">
          FTTH</label>
               <label class="text-ws" style="color: #606060"  v-if="value.type == 3 ">
            Cobre</label>
               <label class="text-ws" style="color: #606060"  v-if="value.type == 4 ">
           Radio</label>
            </div>
          </div>
        </div>
      </div><br>
      <div class="form-horizontal my-2 col-12 flex-wrap">
        <div type="button" data-toggle="collapse" data-target="#collapseVelocidad" aria-expanded="false" aria-controls="collapseVelocidad" style="display:flex;justify-content: space-between;">
          <h4 class="btn-block" style="color:#616161; font-family:'Work Sans'; font-weight: 500;">  Velocidad   </h4> <span><i class="fas fa-angle-down" style="margin-left: auto; font-size: 33px;   color: #afaeb4;"></i></span>
        </div>
<div class="collapse" id="collapseVelocidad">
  <div class="card card-body" style="background-color: #f7f7f7;">
    <vue-slider
      v-model="value"
      :order="true"
      :min="1"
      :max="500"
      :interval="1"
      :tooltip-formatter="formatter2"
    > </vue-slider>
       <div class="row">
     <div class="col text-left">
        <span>{{value[0].toString().replace(/(\d)(?:(?=\d+(?=[^\d.]))(?=(?:[0-9]{3})+\b)|(?=\d+(?=\.))(?=(?:[0-9]{3})+(?=\.)))/g, "$1,")}} Mbps</span>
     </div>
     <div class="col text-right">
       <span  >{{value[1].toString().replace(/(\d)(?:(?=\d+(?=[^\d.]))(?=(?:[0-9]{3})+\b)|(?=\d+(?=\.))(?=(?:[0-9]{3})+(?=\.)))/g, "$1,")}} Mbps</span> 
     </div>
   </div>
      
  </div>
</div><br>
</div>

<div class="form-horizontal my-2 col-12 flex-wrap" >
  <div  type="button" data-toggle="collapse" data-target="#collapsePrecio" aria-expanded="false" aria-controls="collapseExample" style="display:flex;justify-content: space-between;">
 <h4 class="btn-block" style="color:#616161">  Precio   </h4> <span><i class="fas fa-angle-down" style="margin-left: auto; font-size: 33px;   color: #afaeb4;"></i></span>

  </div>

<div class="collapse" id="collapsePrecio">
  <div class="card card-body" style="background-color: #f7f7f7;" v-if="orderBy">

            <input class="form-control" style="    border-radius: 9px;
" id="precio_bajo" v-model="fromPrice" placeholder=" $ Desde">
            <br>
            <input class="form-control" style="    border-radius: 9px;
" id="precio_bajo" v-model="toPrice" placeholder=" $ Hasta">
                
      
 
  </div>
</div>



    </div>

  </div>
    <div class="card-footer d-flex justify-content-center pb-4" style="background-color: #f7f7f7;">
      <div class="col-lg-8 col-md-10 col-sm-10">
        <i class="fa fa-search icon-btn"></i>
        <button @click="emitFilter" class="btn btn-block btn-dark-blue ">
          Buscar
        </button>
      </div>
    </div>
  </div>

</div>

</template>

<script>


import { EventBus } from '../../../EventBus.js'; 

export default {

  props:["fields","providers","max_price", "min_price","technologies","speeds","max_speed", "min_speed"],

  data(){
    return{
      orderBy:"tariff",
      fromPrice:null,
      toPrice:null,
      orderBySort:"desc",
      checked_speeds:[],
      checked_technologies:[],
      checked_providers:[],
      value: [1,500],
      // value: [this.min_speed,this.max_speed],
      patron:new RegExp(/\d{1,3}(?:,\d{3})*(?:\.\d+)?/),
      formatter2: v => `${('' + (v)).replace(/\B(?=(\d{3})+(?!\d))/g, ',')} Mbps`
    }
  },

  mounted(){
    EventBus.$on('getOrder',function Escucha(value) {
      this.getOrder();
    }.bind(this)); 
  },
  methods:{
    emitFilter(){
      //console.log(max_price);
     // return;
      let searchKey="";

      if(this.orderBy){
      // if(this.orderBySort){
        // alert(this.orderBySort);
        searchKey+="&sortBy="+this.orderBy;
        // searchKey+="&sortBy=tariff";
        if(this.orderBySort=="desc"){
          searchKey+="&sortByDesc=1";
        }
        else searchKey+="&sortByDesc=0";
      }


      // alert(this.orderBySort);
    /*  if(this.value[0]&&this.value[1]!=""){
        if(!isNaN(this.value[0])) searchKey+="&from="+parseFloat(this.value[0]);
        if(!isNaN(this.value[1])) searchKey+="&to="+parseFloat(this.value[1]);
    //    else return toastr.error("El campo 'Desde' es de valor numérico")
      }*/

     /* if(this.toPrice&&this.toPrice!=""){
        
        if(!isNaN(this.toPrice)) searchKey+="&to="+parseFloat(this.toPrice);

        else return toastr.error("El campo 'Hasta' es de valor numérico")
        
      }*/
      if(this.checked_technologies && this.checked_technologies.lenght != 0){
        searchKey+="&technologies="+this.checked_technologies;
      }
      else{
        searchKey+="&technologies=";
      }
      /*if(this.checked_speeds.lenght != 0){
        searchKey+="&speeds="+this.checked_speeds;
      }*/

      if(this.value && this.value.lenght != 0){
        searchKey+="&speeds="+this.value;
      }
      else{
        searchKey+="&speeds=1,500";
      }

      if(this.checked_technologies && this.checked_technologies.lenght != 0){
        searchKey+="&providers="+this.checked_providers;
      }
      else{
        searchKey+="&providers=";
      }

      console.log(searchKey);
      this.$emit("customFiltering", searchKey);


    },
    
    getOrder(){

      if(this.orderBySort == "desc")
          this.orderBySort = "asc";
      else this.orderBySort = "desc";

      this.orderBy = "tariff";
      this.emitFilter();

    },
    /*changeOrderPrice: function(){
     if(this.orderBySort == "desc")
            this.orderBySort = "asc";
        else this.orderBySort = "desc";

        this.orderBy = "tariff";

      this.emitFilter();
    },*/
  },

  computed:{
    compFields:{
      get(){
        return this.fields;
      }
    }
  }

}
</script>