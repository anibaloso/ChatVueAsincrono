<script>
import axios from 'axios'
import ChatComponent from '@/components/ChatComponent.vue'

export default {
    components:{
        ChatComponent
    },          
    data() {
        return {
            usuario1: {},
            usuario1Nombre: '',
            usuario2: {},
            color1: '',
            color2: '',
            msj: '',
            msj2: '',
            chat: []

        }
    },
    methods: {
        async personaRandom() {
            try {
                const url = 'https://randomuser.me/api/'
                const { data } = await axios.get(url)
                this.usuario1 = data.results[0]
                this.usuario1Nombre = `${this.usuario1.name?.title} ${this.usuario1.name?.first}`
            } catch (error) {
                console.error(error)
            }
        },
        async personaRandom2() {
            try {
                const url = 'https://randomuser.me/api/'
                const { data } = await axios.get(url)
                this.usuario2 = data.results[0]
            } catch (error) {
                console.error(error)
            }
        },
        enviarMensaje1() {
            const nuevoMensaje = {
                usuario: `${this.usuario1.name?.title} ${this.usuario1.name?.first}`,
                mensaje: this.msj
            }

            this.chat.push(nuevoMensaje)
            this.msj = ''
        },
        enviarMensaje2() {
            const nuevoMensaje = {
                usuario: `${this.usuario2.name?.title} ${this.usuario2.name?.first}`,
                mensaje: this.msj2
            }
            this.chat.push(nuevoMensaje)
            this.msj2 = ''
        }
    },
    mounted() {
        this.personaRandom()
        this.personaRandom2()
    }
}

</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col col-3">
                <div class="col-12">
                    <img :src="usuario1.picture?.large" alt="">
                    <!-- el ? usado en picture permite acceder alas propiedades de manera segura, esto evita que vue lance un error-->
                    <p>{{ usuario1.name?.title }} {{ usuario1.name?.first }}</p>
                    <input type="color" v-model="color1">
                    <textarea v-model="msj"></textarea>
                    <button @click="enviarMensaje1">enviar</button>
                </div>
            </div>
            <div class="col col-6 chat">

                <ChatComponent :mensajes="chat"
                    :usuario1Nombre="usuario1Nombre"
                    :color1="color1"
                    :color2="color2"
                />

            </div>
            <div class="col col-3">
                <div class="col-12">
                    <img :src="usuario2.picture?.large" alt="">
                    <!-- el ? usado en picture permite acceder alas propiedades de manera segura, esto evita que vue lance un error-->
                    <p>{{ usuario2.name?.title }} {{ usuario2.name?.first }}</p>
                    <input type="color" v-model="color2">
                    <textarea v-model="msj2"></textarea>
                    <button @click="enviarMensaje2">enviar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.chat {
    background-color: #efe6dd;
}

.col {
    border: 1px solid black;

}

textarea {
    width: 100%;
}

input {
    width: 100%;
}

button {
    width: 100%;
}

</style>