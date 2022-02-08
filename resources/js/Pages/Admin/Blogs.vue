<template>
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Blogs
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">

                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="mt-2 py-2">
                        <form action="" @submit.prevent="storeArticulo" method="post" enctype="multipart/form-data" class="px-4 pt-6 mb-2 bg-white rounded">
                            <div class="mb-4 md:flex md:justify-between">
                                <div class="mb-4 md:mr-2 md:mb-0">
                                    <label class="block mb-2 text-sm font-bold text-gray-700" for="titulo">Titulo del Aticulo</label>
									<input v-model="form.titulo" class="w-full px-2 py-2 text-sm leading-tight text-gray-700 border rounded shadow appearance-none focus:outline-none focus:shadow-outline"
									id="titulo" name="titulo" type="text" placeholder="Titulo" maxlength="100" minlength="2"/>
                                </div>
                                <div class="md:ml-2">
                                    <label class="block mb-2 text-sm font-bold text-gray-700" for="lastName">Descripcion</label>
									<input v-model="form.descripcion" class="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded shadow appearance-none focus:outline-none focus:shadow-outline" 
                                    id="descripcion" name="descripcion" type="text" placeholder="Descripcion" maxlength="100" minlength="2"/>
                                </div>
                                <div class="md:ml-2">
                                    <label for="imagen" class="block mb-2 text-sm font-bold text-gray-700">Seleccione Imagen</label>
                                    <input type="file" name="image" id="image" class="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded shadow appearance-none focus:outline-none focus:shadow-outline"
                                    ref="fileInputEdit" @change="getImage" accept="image/jpeg">
                                </div>
                                <div class="md:ml-2">
                                    <button class="mt-6 w-full px-4 py-2 font-bold text-white bg-blue-500 rounded-full hover:bg-blue-700 focus:outline-none focus:shadow-outline" type="button">
                                        Crear Articulo
                                    </button>
                                </div>
                            </div>
                        </form>
                        <div class="px-4 pt-2 mb-4">
                            <div class="">
                                <div v-if="imagenMuestra === ''"></div>
                                <div v-else-if="imagenMuestra != ''">
                                    <figure class="figure">
                                        <img :src="imagenMuestra" alt="imagen de muestra" class="figure-img img-fluid rounded">
                                        <figcaption class="figure-caption">Dimenciones de imagen recomendada (480X360) o derivados</figcaption>
                                    </figure>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </app-layout>
</template>

<script>
import { defineComponent } from "@vue/runtime-core";
import AppLayout from '@/Layouts/AppLayout.vue'

export default  defineComponent({
    components: {
        AppLayout
    },
    data() {
        return {
            form: this.$inertia.form ({
                titulo: '',
                descripcion: '',
                image: null,
            }),
            imagenMuestra: '',
            listaArticulos: [],
        }
    },
    methods: {
        getImage(e) {
            const img = e.target.files[0]
            this.form.image = img
            let reader  = new FileReader();
            reader.addEventListener("load", function () {
                this.imagenMuestra = reader.result;
            }.bind(this), false);
            
            if( this.form.image ){
                if ( /\.(jpe?g|png)$/i.test( this.form.image.name ) ) {
                    reader.readAsDataURL( this.form.image );
                }
            }
        },
        storeArticulo() {},
    }
})
</script>

<style scoped>
.figure > img{
    width: 480px;
    height: 360px;
}
</style>