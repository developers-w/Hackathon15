<template>
    <div class="user" >
         <h1>{{user.usuario}}</h1>
         <p><span>Nombre:</span> {{user.nombre}}</p>
         <p><span>Apellido:</span>{{user.apellido}}</p>
         <p><span>Dni:</span>{{user.dni}}</p>
         <p><span>Cargo:</span>{{user.cargo}}</p>
         <p><span>Email</span>{{user.email}}</p>
         <p><span>Descripcion:</span>{{user.descripcion}}</p>
         

    </div>
</template>
<script>
export default {
    data() {
        return {
            user:{}
            
        }
    },
       methods: {
        async getUsuarios(){
            const dato= await fetch(`http://localhost:3000/usuarios/${this.$route.params.id}`);
            const info = await dato.json();
            this.user=info;
            console.log(info);
        }
    },
    created() {
       this.getUsuarios()
    },
}
</script>
<style scoped>
    .user{
    width: 400px;
    margin: 0 auto;
    }
</style>