<template >

    <div class="container">

        <div class="row g-4">
            <div class="row row-cols-1 row-cols-md-4 g-4">

                <div v-for="dataServicio in dataServicios" :key="dataServicio.idServicio">
                    <div class="card h-100 border-0 shadow">

                        <div class="carousel-item active">
                            <img class="mx-auto d-block card-img-top" src="@/assets/img/publicaciones/default.jpg"
                                alt="First slide">
                        </div>
                        <div class="card-body">
                            <h2> {{ dataServicio.nombre }} </h2>

                            <div v-for="dataAnfitrion in dataAnfitriones" :key="dataAnfitrion.idAnfitrion">
                                <h5 v-if="dataServicio.idAnfitrion === dataAnfitrion.idAnfitrion">@{{
                                dataAnfitrion.descripcion
                                }}</h5>
                            </div>

                            <p> {{ dataServicio.descripcion }}</p>

                            <div v-for="dataMunicipio in dataMunicipios" :key="dataMunicipio.idMunicipio">
                                <p v-if="dataServicio.idMunicipio === dataMunicipio.idMunicipio">Municipio: {{
                                dataMunicipio.municipio
                                }}</p>
                            </div>
                            <p> Publicada: {{ dataServicio.date_update }}</p>

                            <button v-if="dataServicio.disponibilidad == 0" class="btn btn-primary"
                                @click.prevent="reservar(dataServicio.idServicio)">Reservar</button>
                            <button class="btn btn-primary" @click="showModal(dataServicio.idServicio)">Ver</button>
                        </div>
                    </div>

                    <!--Inicia el modal-->
                    <div v-bind:id="dataServicio.idServicio" class="modal" tabindex="-1" role="dialog"
                        aria-labelledby="myLargeModalLabel">
                        <div class="modal-dialog modal-lg">
                            <div class="modal-content">

                                <div class="modal-header">
                                    <h3 class="title">{{ dataServicio.nombre }}</h3>
                                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                                        <span aria-hidden="true">&times;</span>
                                    </button>
                                </div>
                                <div class="modal-body">
                                    <form class="row g-4" action="#" method="POST">
                                        <div class="form-group col-md-12">
                                            <img class="mx-auto d-block" src="@/assets/img/publicaciones/default.jpg"
                                                alt="First slide">
                                        </div>

                                        <div class="form-group col-md-4">
                                            <label class="label has-text-centered">Tarifa/Noche</label>
                                            <div v-for="dataTarifa in dataTarifas" :key="dataTarifa.idTarifa">
                                                <h6 class="subtitle is-6 has-text-centered"
                                                    v-if="dataServicio.idTarifa === dataTarifa.idTarifa">
                                                    ${{ dataTarifa.precio }}</h6>
                                            </div>
                                        </div>

                                        <div class="form-group col-md-4">
                                            <label class="label has-text-centered">Tipo de Hospedaje</label>
                                            <div v-for="dataTipoHospedaje in dataTipoHospedajes"
                                                :key="dataTipoHospedaje.idTipoHospedaje">
                                                <h6 class="subtitle is-6 has-text-centered"
                                                    v-if="dataServicio.idTipoHospedaje === dataTipoHospedaje.idTipoHospedaje">
                                                    {{ dataTipoHospedaje.tipoHospedaje }}</h6>
                                            </div>
                                        </div>

                                        <div class="form-group col-md-4">
                                            <label class="label has-text-centered">Disponibilidad</label>

                                            <div v-if="dataServicio.disponibilidad == 0">
                                                <h6 class="subtitle is-6 has-text-centered">Sin reservar</h6>
                                            </div>
                                            <div v-if="dataServicio.disponibilidad == 1">
                                                <h6 class="subtitle is-6 has-text-centered">Reservado</h6>
                                            </div>

                                        </div>

                                        <div class="form-group col-md-4">
                                            <label class="label has-text-centered">Municipio</label>
                                            <div v-for="dataMunicipio in dataMunicipios"
                                                :key="dataMunicipio.idMunicipio">
                                                <h6 class="subtitle is-6 has-text-centered"
                                                    v-if="dataServicio.idMunicipio === dataMunicipio.idMunicipio">
                                                    {{ dataMunicipio.municipio }}</h6>
                                            </div>
                                        </div>

                                        <div class="form-group col-md-6">
                                            <label class="label has-text-centered">Direccion</label>
                                            <h6 class="subtitle is-6 has-text-centered">{{ dataServicio.direccion }}
                                            </h6>
                                        </div>

                                        <div class="form-group col-md-6">
                                            <label class="label has-text-centered">Descripci??n del hospedaje</label>
                                            <h6 class="subtitle is-6 has-text-centered">{{ dataServicio.descripcion }}
                                            </h6>
                                        </div>

                                        <div class="form-group col-md-3">
                                            <label class="label has-text-centered">Publicada por</label>
                                            <div v-for="dataAnfitrion in dataAnfitriones"
                                                :key="dataAnfitrion.idAnfitrion">
                                                <h6 v-if="dataServicio.idAnfitrion === dataAnfitrion.idAnfitrion">@{{
                                                dataAnfitrion.descripcion
                                                }}</h6>
                                            </div>
                                        </div>

                                        <div class="form-group col-md-3">
                                            <label class="label has-text-centered">Publicada</label>
                                            <h6 class="subtitle is-6 has-text-centered">{{ dataServicio.date_update }}
                                            </h6>
                                        </div>
                                    </form>

                                </div>
                                <div class="modal-footer">
                                    <button type="button" class="btn btn-secondary" aria-label="Close"
                                        data-dismiss="modal">Cerrar</button>
                                </div>
                            </div>

                        </div>
                    </div>

                </div>
            </div>
        </div>

    </div><br><br><br>

</template>
  
<script>


export default {


    name: 'Alojamiento',

    data: () => ({
        dataServicios: null,
        dataAnfitriones: null,
        dataMunicipios: null,
        dataTarifas: null,
        dataTipoHospedajes: null,
        rutaFotos: null,
        fotos: null

    }),
    created() {

        /*data servicios
        axios.get('http://api_airbnb.test/servicios').then(response =>
            console.log(response.data.clients))*/

        /*data anfitriones
        axios.get('http://api_airbnb.test/anfitriones').then(response =>
            console.log(response.data.clients))*/

        /*data municipios
        axios.get('http://api_airbnb.test/anfitriones').then(response =>
            console.log(response.data.clients))*/


        axios.get('http://api_airbnb.test/servicios').then(result => {
            this.dataServicios = result.data.clients
            //   console.log(result.data.clients)

            const datos = result.data.clients

            for (let i = 0; i < datos.length; i++) {
                //  console.log(datos[i].foto)
                this.rutaFotos = datos[i].foto

                //se imprime la ruta de todas publicaciones registradas e la BD
                console.log(this.rutaFotos)

                const pruebafiles = this.rutaFotos

            }

        })

        axios.get('http://api_airbnb.test/anfitriones').then(result => {
            this.dataAnfitriones = result.data.clients
        })

        axios.get('http://api_airbnb.test/municipioss').then(result => {
            this.dataMunicipios = result.data.clients
        })

        axios.get('http://api_airbnb.test/tarifas').then(result => {
            this.dataTarifas = result.data.clients
        })

        axios.get('http://api_airbnb.test/tipoHospedajes').then(result => {
            this.dataTipoHospedajes = result.data.clients
        })

        //Lee el directorio 
        const resultado = require.context(
            '@/assets/img/publicaciones/1/2766/',
            true,
            /^.*\.jpg$/
        )

        const resultadoFiles = resultado.keys()

        //ciclo for para imprimir uno por uno todos los archivos que esten en ese directorio
        for (let i = 0; i < resultadoFiles.length; i++) {
            //  console.log(partido[i].slice(2))               
            this.fotos = resultadoFiles[i].slice(2)
            console.log(this.fotos)
        }
    },
    methods: {
        showModal(id) {
            $("#" + id).modal('show');
        },

        reservar(idServicio) {
            this.$router.push('/reservar/' + idServicio)
        },

    }
};


</script>

<style scoped>
.container {
    margin-top: 10vh;
}
</style>