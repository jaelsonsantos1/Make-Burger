<template>
    <!-- <p>Burguer for components</p> -->
    <div>
        <Menssagem :msg="msg" v-show="msg" />
        <div>
            <form id="burguer-form" @submit="createBurguer">
                <!-- Nome do cliente -->
                <div class="input-container">
                    <label for="nome">Nome do cliente: </label>
                    <input type="text" name="nome" v-model="nome" placeholder="Digite o seu nome..." minlength="5" required>
                </div>
                
                <!-- Tipo de pão -->
                <div class="input-container">
                    <label for="pao">Escolha o tipo de pão no hamburguer</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>
                
                <!-- Tipo de carne -->
                <div class="input-container">
                    <label for="carne">Escolha qual carne você deseja no seu Burguer:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione o tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>
                </div>
                
                <!-- Opicionais -->
                <div class="input-container" id="opicionais-container">
                    <label id="opcionais-title" for="opcional">Selecione os opicionais:</label>
                    <div v-for="op in opcionaisdata" :key="op.id" class="checkbox-container">
                        <input type="checkbox" name="opcional" v-model="opcionais" :value="op.tipo">
                        <span>{{ op.tipo }}</span>
                    </div>
                </div>
        
                <!-- Enviar -->
                <div class="input-container">
                    <input type="submit" class="btn-subimit" value="Fazer pedido">
                </div>
            </form>
        </div>

    </div>
</template>
 
<script>
import Menssagem from "./Menssagem.vue";

export default {

    name: "BurguerForm",
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            msg: null
        }
    },
    methods: {
        async getIngredientes() {

        const request = await fetch("http://localhost:3000/ingredientes");
        const response = await request.json();

        this.paes = response.paes;
        this.carnes = response.carnes;
        this.opcionaisdata = response.opcionais;

        },
        async createBurguer(e) {
            e.preventDefault();
            
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }

            const dataJson = JSON.stringify(data);

            const requests = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: dataJson
            })

            const response = await requests.json();
            
            // Mostrar uma menssagem do sistema
            this.msg = `Pedido N°${response.id} realizado com sucesso!`

            // Limpar A menssagem do sistema
            setTimeout(() => this.msg="", 3000);
            
            // Limpar os campos
            this.nome = "";
            this.carne = "";
            this.pao = "";
            this.opcionais = "";

        }
    },
    mounted() {
        this.getIngredientes();
    },
    components: {
        Menssagem
    }
}
</script>

<style scoped>
    #burguer-form {
        border-radius: 10px;
        
        padding: 20px;
        max-width: 400px;
        width: 85%;
        margin: 0 auto;
        background-color: #fffdf5;
        box-shadow: 0 0 15px 5px #dfdada;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid yellow;;
    }

    input, select {
        padding: 5px 10px;
        width: 300px;
    }

    #opicionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }
    
    #opcionais-title {
        width: 100%;
    }
    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }
    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .btn-subimit {
        background-color: #222;
        color: rgb(255, 179, 0);
        font-weight: bold;
        border: 2px solid rgba(34, 34, 34, 0.789);
        font-size: 0.9em;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }
    .btn-subimit:hover {
        background-color: transparent;
        color: #222;
    }


</style>
