<template>
    <button 
      style = "position: relative; right: 600px;" 
      class = "btn btn-primary"
      @click="agregar=true"
    >
      Nuevo Influencer <i class="fas fa-plus"></i>
    </button>
    <div class="container-form" v-if="agregar">
        <form action="">
            <div class="title"><label for="">Nuevo Influencer</label></div>
            <input type="text" class="form-control mb-2" placeholder="Username" v-model="influencer.username"><br>
            <input type="text" class="form-control mb-2" placeholder="Nombre Completo" v-model="influencer.full_name"><br>
            <input type="text" class="form-control mb-2" placeholder="Telefono" v-model="influencer.phone"><br>
            <input type="text" class="form-control mb-2" placeholder="E-mail" v-model="influencer.email"><br>
            <form class="form-inline">
                <div class="form-group mb-2">
                    <input type="text" class="form-control mb-2" placeholder="Seguidores?" v-model="influencer.followers_count">
                </div>
                <div class="form-group mx-sm-3 mb-2">
                    <input type="text" class="form-control mb-2" placeholder="Seguidos?" v-model="influencer.following_count">
                </div>
            </form>
            <form class="form-inline">
                <div class="form-group mb-2">
                    <label for="">Categoria:</label>
                    <select class="form-control" name="" id="" v-model="influencer.category_id">
                        <categories />
                    </select>
                </div>
                <div class="form-group mx-sm-3 mb-2">
                    <label for="">Red Social:</label>
                    <select class="form-control" name="" id="" v-model="influencer.social_network_id">
                        <social-networks />
                    </select>
                </div>
            </form>
            <br>
            <button style="position: relative; left: 120px;" class="btn btn-light" @click="cancelarAgregar">Cancelar</button>
            <button style="position: relative; left: 140px;" class="btn btn-primary" @click="agregarDatos">Guardar</button>
        </form>
    </div>

    <div class="container-form" v-if="editar">
        <form action="">
            <div class="title"><label for="">Editar Influencer</label></div>
            <input type="text" class="form-control mb-2" placeholder="Username" v-model="influencer.username"><br>
            <input type="text" class="form-control mb-2" placeholder="Nombre Completo" v-model="influencer.full_name"><br>
            <input type="text" class="form-control mb-2" placeholder="Telefono" v-model="influencer.phone"><br>
            <input type="text" class="form-control mb-2" placeholder="E-mail" v-model="influencer.email"><br>
            <form class="form-inline">
                <div class="form-group mb-2">
                    <input type="text" class="form-control mb-2" placeholder="Seguidores?" v-model="influencer.followers_count">
                </div>
                <div class="form-group mx-sm-3 mb-2">
                    <input type="text" class="form-control mb-2" placeholder="Seguidos?" v-model="influencer.following_count">
                </div>
            </form>
            <form class="form-inline">
                <div class="form-group mb-2">
                    <label for="">Categoria:</label>
                    <select class="form-control" name="" id="" v-model="influencer.category_id">
                        <categories />
                    </select>
                </div>
                <div class="form-group mx-sm-3 mb-2">
                    <label for="">Red Social:</label>
                    <select class="form-control" name="" id="" v-model="influencer.social_network_id">
                        <social-networks />
                    </select>
                </div>
            </form>
            <button style="position: relative; left: 120px;" class="btn btn-light" @click="cancelarEditar">Cancelar</button>
            <button style="position: relative; left: 140px;" class="btn btn-primary" @click="editarDatos(item)">Guardar</button>
        </form>
    </div>

    <div class="col-lg-12 control-section avatar-card">
        
        <div class="container" v-for="item in datos" :key="item.id">
            <div class="sample_container">
                <div class="e-card e-custom-card">
                    <div class="e-card-header">
                        <div class="e-avatar e-avatar-circle e-avatar-xlarge">
                            <img src="">
                        </div>
                        
                    </div>
                    <div class="e-card-header">
                        <div class="e-card-header-caption center">
                            <div class="e-card-header-title name">{{ item.name }}</div>
                            <div class="e-card-sub-title">
                                <span v-if="item.category_id === 1" class="badge categoria">Foodie</span>
                                <span v-if="item.category_id === 2" class="badge categoria">Telecomuncations</span>
                                <span v-if="item.category_id === 3" class="badge categoria">Applications</span>
                                <span v-if="item.category_id === 4" class="badge categoria">Travel</span>
                                <span v-if="item.category_id === 5" class="badge categoria">Entertainment</span>
                                <span v-if="item.category_id === 6" class="badge categoria">Cinema and TV</span>
                            </div>
                        </div>
                    </div>
                    <div class="e-card-content">
                        <p class="avatar-content">
                            Nombre: {{ item.full_name }} <br>
                            Red Social:
                                <span v-if="item.social_network_id === 1" class="badge facebook-category">Facebook</span> <br>
                                <span v-if="item.social_network_id === 2" class="badge instagram-category">Instagram</span> <br>
                                <span v-if="item.social_network_id === 3" class="badge tiktok-category">TikTok</span> <br>
                                <span v-if="item.social_network_id === 4" class="badge youtube-category">Youtube</span> <br>
                            Telefono: 961 234 5678 <br>
                            Email: correo@gmail.com
                        </p>
                        <div class="dropdown">
                            <button class="btn btn-light dropbtn"><i class="fas fa-ellipsis-v"></i></button>
                            <div class="dropdown-content">
                                <p>
                                    <button class="btn btn-warning btn-circle" @click="editarInfluencer(item)">
                                        <i class="fas fa-pencil-alt"></i>
                                    </button>
                                </p>
                                <p>
                                    <button class="btn btn-danger btn-circle" @click="eliminarDato(item)">
                                        <i class="fas fa-trash"></i>
                                    </button>
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import Swal from 'sweetalert2'
import Categories from './Categories.vue'
import SocialNetworks from './SocialNetworks.vue'

export default {
    name: 'Card',
    components: {
        Categories,
        SocialNetworks
    },
    data() {
        return {
            agregar: false,
            editar: false,
            datos: [],
            influencer: {
                username: '',
                full_name: '',
                phone: '',
                email: '',
                followers_count: '',
                following_count: '',
                category_id: '',
                social_network_id: ''
            },
        }
    },
    created() {
       axios.get('https://pokeapi.co/api/v2/pokemon')
            .then((resp)=>{
            this.datos = resp.data;
        })
    },
    methods: {
        agregarDatos() {
            if(this.influencer.username.trim() === '' || this.influencer.full_name.trim() === '' || this.influencer.phone.trim() === '' || this.influencer.email.trim() === '' || this.influencer.followers_count.trim() === '' || this.influencer.following_count.trim() === '' || this.influencer.category_id.trim() === '' || this.influencer.social_network_id.trim() === '') {
                Swal.fire('Faltan Campos por llenar','','error');
            }
            const nuevoInfluencer = this.influencer;
            this.influencer = {
                username: '',
                full_name: '',
                phone: '',
                email: '',
                followers_count: '',
                following_count: '',
                category_id: '',
                social_network: ''
            };
            axios.post('/api/influencer/create', nuevoInfluencer)
                .then((resp) => {
                    const influencerServidor = resp.data;
                    this.datos.push(influencerServidor);
                    Swal.fire('Agregado!','','success');
            })
        },
        editarInfluencer(item){
            this.influencer.username = item.username;
            this.influencer.full_name = item.full_name;
            this.influencer.phone = item.phone;
            this.influencer.email = item.email;
            this.influencer.followers_count = item.followers_count;
            this.influencer.following_count = item.following_count;
            this.influencer.category_id = item.category_id;
            this.influencer.social_network = item.social_network;
            this.influencer.id = item.id;
            this.editar = true;
            this.agregar = false;
        },
        editarDatos(item) {
            const params = {};
            axios.put(`/influencer/${influencer.id}/edit`, params)
                .then(resp=>{
                    this.editar = false;
                    const index = this.datos.findIndex(item => item.id === influencer.id);
                    this.influencer[index] = resp.data;
                    Swal.fire('Actualizado!','','success');
                })
        },
        eliminar(item){
            Swal.fire({
                title: '¿Seguro quieres eliminar este dato?',
                showDenyButton: true,
                confirmButtonText: 'Seguro',
                denyButtonText: 'No Elminar',
            }).then((result) => {
                if (result.isConfirmed) {
                    axios.delete('influencer/${influencer.id}')
                        .then(() => {
                            this.getDatos()
                            Swal.fire('Eliminado!','','success');
                        })
                        .catch(e => {
                            Swal.fire('No se logro eliminar!','${e}','error');
                        })
                }else if (result.isDenied) {
                    Swal.fire('Cancelado','','info');
                }
            });
        },
        cancelarAgregar() {
            this.agregar = false;
            this.influencer = {
                username: '',
                full_name: '',
                phone: '',
                email: '',
                followers_count: '',
                following_count: '',
                category_id: '',
                social_network: ''
            };
        },
        cancelarEditar() {
            this.editar = false;
            this.influencer = {
                username: '',
                full_name: '',
                phone: '',
                email: '',
                followers_count: '',
                following_count: '',
                category_id: '',
                social_network: ''
            };
        }
    },
}

</script>

<style>
.container{
    display: flex;
    flex-wrap: wrap;
    height: 290px;
    align-content: space-between;
}

.container-form{
    display: flex;
    flex-wrap: wrap;
    height: 290px;
    position: absolute;
    left: 20px;
    top: 140px;
}

.title {
    text-align: left;
    text-transform: capitalize;
    font-family: "Lucida Console", "Courier New", monospace;
}

.dropdown {
    position: relative;
    left: 90px;
    display: inline-block;
}

.dropdown-content {
    display: none;
    position: absolute;
    min-width: 10px;
    box-shadow: px 8px 16px 0px rgba(0,0,0,0.2);
    padding: 12px 16px;
    z-index: 1;
}

.dropdown:hover .dropdown-content {
    display: block;
}

.dropdown:hover .dropbtn {
  background-color: white;
}

.categoria{
    background: salmon;
}

.tiktok-category {
    background: black;
}

.youtube-category {
    background: red;
}

.facebook-category {
    background: dodgerblue;
}

.instagram-category {
    background: radial-gradient(circle at 30% 107%, #fdf497 0%, #fdf497 5%, #fd5949 45%, #d6249f 60%, #285AEB 90%);
    color: black;
}

.btn-circle {
    border-radius: 50%;
}

.avatar-card .sample_container {
    max-width: 300px;
    margin: auto;
    min-height: 400px;
}

.avatar-card .e-custom-card {
    position: relative;
    margin-top: 100px;
    overflow: visible;
    border-radius: 15px;
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
    transition: 0.2s;
    border-width: 1px;
    padding: 10px;
}

.avatar-card .e-custom-card.e-card:hover {
    border-width: 1px;
    padding: 1px;
}

.avatar-card .e-custom-card :nth-child(2) .e-card-header-title.name {
    margin-top: 20px;
}

.avatar-card p.avatar-content {
    line-height: 20px;
    font-family: inherit;
}

.avatar-card .e-custom-card .e-card-header {
    text-align: center;
}

.avatar-card .e-custom-card .e-avatar {
    font-size: 40px;
    position: absolute;
    top: calc(0% - 1.5em);
    left: calc(50% - 1.5em);
    box-shadow: 0 16px 28px -8px rgba(0, 0, 0, .36), 0 4px 15px 0 rgba(0, 0, 0, .12), 0 8px 10px -5px rgba(0, 0, 0, .2);
}

.avatar-card .e-card.e-custom-card :nth-child(3) {
    padding: 12px 0px 20px 0px;
    height: 130px;
}

.avatar-card .e-custom-card.e-card .e-card-header .e-card-header-caption .e-card-header-title {
    font-size: 24px;
    font-weight: 500;
    line-height: normal;
    color: rgba(83, 101, 132, 0.65);
    text-shadow: 0 0 0.1px;
}

.avatar-card .e-custom-card.e-card .e-card-header .e-card-header-caption .e-card-sub-title {
    font-size: 12px;
    font-weight: 500;
    line-height: normal;
    color: rgba(86, 90, 97, 0.65);
    text-shadow: 0 0 0.1px;
}

.avatar-card .e-custom-card.e-card .e-card-content {
    overflow: visible;
    width: auto;
    margin: -5px 20px 0 20px;
    word-spacing: 1px;
}

.avatar-card .avatar-content {
    color: rgba(250, 200, 130, 0.6);
    margin: 0 auto;
    text-align: center;
    color: rgb(94, 94, 94);
    border: none;
    padding: 0;
    font-size: 14px;
}

.avatar-card .avatar-content {
    margin-bottom: 0;
}

.avatar-card .sample_container .name {
    margin-top: 10px;
}

.highcontrast .avatar-card .e-custom-card.e-card .avatar-content {
    color: rgba(255, 255, 255, 0.84);
}

.highcontrast .avatar-card .e-custom-card.e-card .e-card-header .e-card-header-caption .e-card-sub-title {
    color: rgba(255, 255, 255, 0.45);
}

.highcontrast .avatar-card .e-custom-card.e-card .e-card-header .e-card-header-caption .e-card-header-title {
    color: rgba(255, 255, 255, 0.84);
}
</style>

   