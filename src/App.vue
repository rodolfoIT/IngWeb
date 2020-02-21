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
          <div class="col">Encendido <input v-model="nuevoEncendido" class="form-control"></div>
          <div class="col">
            <button class="btn btn-primary" v-on:click="agregarEstacion">Agregar</button>
          </div>
		</div>

			<div class="row">
				<div class="col">Index</div>
				<div class="col">Id </div>
				<div class="col">Estanque</div>
				<div class="col">Posicion</div>
				<div class="col">Encendida</div>
			</div>
			<div class="row" v-for="a in estaciones" v-bind:key="a.Index">
				<div class="col">{{a.Index}}</div>
				<div class="col">{{a.Id}}</div>
				<div class="col">{{a.Estanque}}</div>
				<div class="col">{{a.Posicion}}</div>
				<div class="col">{{a.Encendida}}     
          <button class="btn btn-danger" v-on:click="eliminarEstacion">Eliminar</button>
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
        estaciones : [
        {Index: '1', Id:'12345', Estanque:'10',Posicion:'Oeste', Encendida: 'On' },
        {Index: '2', Id:'15432', Estanque:'10',Posicion:'Este', Encendida: 'On' },
        {Index: '3', Id:'54321', Estanque:'11',Posicion:'Norte' , Encendida: 'On'},
        {Index: '4', Id:'51234', Estanque:'11',Posicion:'Sur' , Encendida: 'On'},
        {Index: '5', Id:'10000', Estanque:'15',Posicion:'Centro' , Encendida: 'On'}
        ],
        nuevoIndex:'',
        nuevoId:'',
        nuevoEstanque:'',
        nuevoPosicion:'',
        nuevoEncendido:''
      }
    },
    methods:{
      agregarEstacion(){
        if(this.nuevoIndex !==''){
        this.estaciones.push(
          {
            Index:this.nuevoIndex,
            Id:this.nuevoId,
            Estanque:this.nuevoEstanque,
            Posicion:this.nuevoPosicion,
            Encendida:this.nuevoEncendido
          }
        )
        this.nuevoIndex='';
        this.nuevoId='';
        this.nuevoEstanque='';
        this.nuevoPosicion='';
        this.nuevoEncendido='';

        }
      },
      eliminarEstacion(estacion){
        console.log("boton presionado", estacion);
        var indice=this.estaciones.indexOf(estacion);
        this.estaciones.splice(indice,1)
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