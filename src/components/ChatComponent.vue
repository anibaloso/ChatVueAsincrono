<script>
export default{
    props:{
        mensajes:{
            type:Array,
            required:true
        },
        usuario1Nombre:{
            type:String,
            required:true
        },
        color1:{
            type:String,
            required:'blue'
        }
        ,
        color2:{
            type:String,
            required:'green'
        }

    }
}
</script>

<template>
    <div v-for="mensaje in mensajes" :key="mensaje.id"
        :class="{ 'izquierda': mensaje.usuario === usuario1Nombre, 'derecha': mensaje.usuario !== usuario1Nombre }">
        <h5>{{ mensaje.usuario }} </h5>
        <p :style="{
            backgroundColor: mensaje.usuario === usuario1Nombre ? color1 : color2,
            borderRadius: '5px',
        }">
            {{ mensaje.mensaje }}</p>
    </div>

</template>

<style scoped>

.izquierda {
    text-align: left;
}

.derecha {
    text-align: right;
    align-items: flex-end;
}

h5 {
    font-size: 10px;

}
</style>
