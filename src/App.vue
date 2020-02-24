<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h3 class ="bg-primary text-white text-center p-2">{{equipo}} <br/> {{nombre}}</h3>
    <div class="container-fluid p-4">
      <div class="row">
            <div class="col">Index <input v-model="nuevoIndex" class="form-control"></div>
            <div class="col">Id <input v-model="nuevoId" class="form-control"></div>
            <div class="col">Estanque <input v-model="nuevoEstanque" class="form-control"></div>
            <div class="col">Posicion <input v-model="nuevoPosicion" class="form-control"></div>
            <div class="col">Status <input v-model="nuevoStatus" class="form-control"></div>
            <div class="col"> <button class="btn btn-primary" v-on:click="agregarEstacion">Agregar</button> </div>
      </div>
			<div class="row">
				<div class="col">Index</div>
				<div class="col">Id </div>
				<div class="col">Estanque</div>
				<div class="col">Posicion</div>
				<div class="col">Status</div>
        <div class="col"></div>
        
			</div>
			<div class="row" v-for="a in estaciones" v-bind:key="a.Index">
				<div class="col">{{a.Index}}</div>
      
        <div class="col"> 
          <span v-if="formActualizar && indexActualizar == a.Index">
          <input v-model="idActualizar" type="text" class="form-control">
          </span>
          <span v-else>
            {{a.Id}}
          </span>
        </div>

        <div class="col"> 
          <span v-if="formActualizar && indexActualizar == a.Index">
            <input v-model="estanqueActualizar" type="text" class="form-control">
          </span>
          <span v-else>
            {{a.Estanque}}
          </span>
        </div>

        <div class="col">
          <span v-if="formActualizar && indexActualizar == a.Index">
            <input v-model="posicionActualizar" type="text" class="form-control">
          </span>
          <span v-else>
            {{a.Posicion}}
          </span>
        </div>
        
        <div class="col"> 
          <span v-if="formActualizar && indexActualizar == a.Index">
            <input v-model="statusActualizar" type="text" class="form-control">
          </span>
          <span v-else>
            {{a.Status}}
          </span>
        </div>

        <div class="col">
          <span v-if="formActualizar && indexActualizar == a.Index">
          <button @click="guardarEdit(a.Index)" class="btn btn-success">Guardar</button>
          </span>
          <span v-else>
            <button  v-on:click="editarEstacion(a.Index)"  class="btn btn-info">Editar</button>
              <button class="btn btn-danger" v-on:click="eliminarEstacion">Eliminar</button>
          </span>
        </div> 
        
 
			</div>

      






    </div>
  </div>
</template>

<script>
  export default{ 
    name:'app',
    data(){
      return{
        equipo: "Equipo 2",
        nombre: "Estaciones EMI-C",
        estaciones: [
        {Index: '1', Id:'12345', Estanque:'10',Posicion:'Oeste', Status: 'On' },
        {Index: '2', Id:'15432', Estanque:'10',Posicion:'Este', Status: 'On' },
        {Index: '3', Id:'54321', Estanque:'11',Posicion:'Norte' , Status: 'On'},
        {Index: '4', Id:'51234', Estanque:'11',Posicion:'Sur' , Status: 'On'},
        {Index: '5', Id:'10000', Estanque:'15',Posicion:'Centro' , Status: 'On'}
        ],
        nuevoIndex:'',
        nuevoId:'',
        nuevoEstanque:'',
        nuevoPosicion:'',
        nuevoStatus:'',
        formActualizar: false,
        indexActualizar:0,
        idActualizar:'',
        estanqueActualizar:'',
        posicionActualizar:'',
        statusActualizar:''

      }
    },
    methods:{
      agregarEstacion(){
        console.log("boton agregar presionado");
        if(this.nuevoIndex !==''){
          this.estaciones.push(
          { 
            Index:this.nuevoIndex,
            Id:this.nuevoId,
            Estanque:this.nuevoEstanque,
            Posicion:this.nuevoPosicion,
            Status:this.nuevoStatus
          }
          );
          this.guardar();
          this.nuevoIndex='';
          this.nuevoId='';
          this.nuevoEstanque='';
          this.nuevoPosicion='';
          this.nuevoStatus='';
        }
      },
      eliminarEstacion(estacion){
        console.log("boton presionado", estacion);
        var indice=this.estaciones.indexOf(estacion);
        this.estaciones.splice(indice,1)
        this.guardar();
      },
      editarEstacion(index) {
        console.log(index);
        this.indexActualizar=index;
        this.idActualizar = this.estaciones[index-1].Id;
        this.estanqueActualizar = this.estaciones[index-1].Estanque;
        this.posicionActualizar = this.estaciones[index-1].Posicion;
        this.statusActualizar = this.estaciones[index-1].Status;
        this.formActualizar = true;
        this.guardar();
      },   
      guardarEdit(index) {
        console.log(index);
        this.formActualizar = false;
        this.estaciones[index-1].Id = this.idActualizar;
        this.estaciones[index-1].Estanque = this.estanqueActualizar;
        this.estaciones[index-1].Posicion = this.posicionActualizar;
        this.estaciones[index-1].Status = this.statusActualizar;
        this.guardar();
      }, 
      guardar(){
        localStorage.setItem("estaciones",JSON.stringify(this.estaciones));
      }
    },
    created(){
        let data =localStorage.getItem("estaciones");
        if(data!=null){
          this.estaciones =JSON.parse(data); 
        }
    }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>