<template>
    <div>
        <h1>Lista de contactos</h1>
        <div class="contenedorCard">
            <div class="card" v-for="(user,index) in listaUsuarios" :key="index" >
                <h2>{{user.usuario}}</h2>
                <p>{{user.cargo}}</p>
                <p>{{user.descripcion}}</p>
                <router-link :to="`/contacts/${user.id}`" >Ver más...</router-link>
                <div class="botns" >
                <button @click="deleteUsuarios(user.id)">Quitar</button>
                <button>Actualizar</button>
                </div>
        
            </div>
        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            listaUsuarios:[]
        }
    },
    methods: {
        async getUsuarios(){
            const dato= await fetch('http://localhost:3000/usuarios');
            const info = await dato.json();
            this.listaUsuarios=info;
            console.log(info);
            
        },
       async addUsuario(){
           const enviarData={

               method:'post',
               headers: { 'Content-Type': 'application/json' },
               body: JSON.stringify( 
                {   id:12,
                    nombre:"Marina",
                    apellido:"Cuevas" ,
                    dni:"89646755",
                    usuario:"marcue",
                    email:"marinacuevas@user.com"  
                })};
      
             const user= await fetch('http://localhost:3000/usuarios',enviarData)
             const info = await user.json();
    
            

        },
        async deleteUsuarios(id){
            
            const dato= await fetch(`http://localhost:3000/usuarios/${id}`,
            {method:'delete'}
            );
            

            this.getUsuarios();
        },
        updateUsuarios(){
            
        }

    },
    created() {
       this.getUsuarios()
    },
    
}
</script>
<style scoped>

.contenedorCard{
    width: 1000px;
    height: 100vh;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;
    justify-content:space-between;
    
}
.card{
    width: 300px;
    height: 350px;
    border: 1px solid black ;
    border-radius: 15px;
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    padding: .5em;
    margin-top: 1em;    
}
.botns{
    margin: 1em;
}


    
</style>