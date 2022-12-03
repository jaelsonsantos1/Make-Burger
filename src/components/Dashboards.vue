<template>
    <div class="burguer-table">
        <Painel :valorPedidos="tot_pedidos" :valorPendentes="tot_pendentes" :valorConcluidos="tot_concluidos" />
        <Menssagem :msg="msg" v-show="msg" />
        <div>
            <div id="burguer-table-heading">
                <div class="order-id">Id</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>
            <div id="burguer-table-rows">
                <!-- Uma linha da tabela -->
                <div class="burguer-table-row" v-for="burger in burgers" :key="burger.id">
                    <div class="order-num">{{ burger.id }}</div>
                    <div>{{ burger.nome }}</div>
                    <div>{{ burger.carne }}</div>
                    <div>{{ burger.pao }}</div>
                    <div>
                        <ul>
                            <li v-for="(opcional, index) in burger.opcionais" :key="index">{{ opcional }}</li>
                        </ul>
                    </div>
                    <div>
                        <select name="status" id="status" @change="((updateBurger($event, burger.id)))">
                            <option v-for="tipo_status in status" :key="tipo_status.id" :value="tipo_status.tipo" :selected="burger.status == tipo_status.tipo">{{ tipo_status.tipo }}</option>
                        </select>
                        <button class="btn-delete" @click="deleteBurger(burger.id)">Cancelar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Painel from './Painel.vue'
import Menssagem from './Menssagem.vue'

export default {
    name: "Dashboard",
    data() {
        return {
            burgers: null,
            burger_id: null,
            tot_pedidos: null,
            tot_pendentes: null,
            tot_concluidos: null,
            status: [],
            msg: null
        }
    },
    methods: {
        async getPedidos() {

            const requests = await fetch("http://localhost:3000/burgers");

            const response = await requests.json();

            this.burgers = response
            this.info(response)

            // Resgatar os Status
            this.getStatus();
        },
        async getStatus() {
            const requests = await fetch("http://localhost:3000/status");

            const response = await requests.json();

            this.status = response;

        },
        async deleteBurger(id) {
            
            const requests = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE"
            });

            const response = await requests.json();

            // Mostrar uma menssagem do sistema
            this.msg = `Pedido removido com sucesso!`

            // Limpar A menssagem do sistema
            setTimeout(() => this.msg="", 3000);

            this.getPedidos();
        },
        async updateBurger(event,  id) {

            const option = event.target.value;
            
            const dataJson = JSON.stringify({
                status: option
            });

            const requests = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: {
                    "Content-Type": "application/json"
                },
                body: dataJson
            });

            const response = await requests.json();

            // Fazendo uma requisição novamente na api para buscar tudo
            const r = await fetch("http://localhost:3000/burgers");
            const d = await r.json();

            // Carregas dados do dashboard 
            this.info(d);
            
            // Mostrar uma menssagem do sistema
            this.msg = `Status do pedido N°${response.id} foi atualizado para ${response.status}!`

            // Limpar A menssagem do sistema
            setTimeout(() => this.msg="", 3000);
        },
        async info(lista_b) {
            // Fazer contagem
            this.tot_concluidos = 0;
            this.tot_pendentes = 0;
            this.tot_pedidos = lista_b.length;
            
            for (var obj in lista_b) {
                if (lista_b[obj].status == "Finalizado") {
                    this.tot_concluidos++;
                } else if (lista_b[obj].status == "Em produção") {
                    this.tot_pendentes++;
                }
            }
        }
    },
    mounted() {
        this.getPedidos()
    },
    components: {
        Painel,
        Menssagem
    }
}
</script>

<style scoped>
    .burguer-table {
        max-width: 1200px;
        margin: 0 auto;
    }

    #burguer-table-heading,
    #burguer-table-rows,
    .burguer-table-row {
        display: flex;
        flex-wrap: wrap;
    }
    
    #burguer-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 2px solid #333;
    }
    
    #burguer-table-heading div,
    .burguer-table-row div {
        width: 19%; 
    }

    .burguer-table-row {
        width: 100%;
        padding: 12px;
        border: 1px solid #CCC;
    }

    #burguer-table-heading .order-id,
    .burguer-table-row .order-num {
        width: 5%;
    }

    select {
        padding: 12px 6px;
        margin-right: 12px;
    }

    .btn-delete {
        background-color: #222;
        color: rgb(255, 179, 15);
        font-weight: bold;
        padding: 10px;
        border: 2px solid #333;
        cursor: pointer;
        font-size: 0.8em;
        margin: 0 auto;
        transition: .5s;
    }
    
    .btn-delete:hover {
        background-color: transparent;
        border: 2px solid rgb(255, 72, 72);
        color: rgb(255, 72, 72);
    }
</style>