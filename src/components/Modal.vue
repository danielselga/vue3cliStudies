<template>
    <div class="backdrop" @click.self="closeModal">
        <!-- o self é um prevent default que limita o click apenas em cima da tag que ele está declarado. -->
        <div class="modal" :class="{sale: theme === 'sale'}">
            <!-- se a propos theme for igual a sale a classe da tag vai receber sale, a chamada na tag deve ser por theme="sale" -->
            <h1>{{header}}</h1>
            <p>{{text}}</p>
            <slot>default contet</slot>
            <!-- esse default content só aprecerá se não declarar nada no elemento pai dentro da tag slot. -->
            <!-- A tag slot é um 'local reservado' no componente filho para receber tags declaradas no componente pai. -->
            <slot name="links"></slot>
            <!-- slots especificos recebem o atributo name com um idetificador e dem ser chamados no elemento pai com a tag slot seguido de v-slot:'identificador' -->
        </div>
    </div>
</template>

<script>
export default {
    props: ['header', 'text', 'theme'],
    methods: {
        closeModal(){
            //custom events podem ser disparados por um componente e escutado por um componente parente.
            //usamos o $emit('nome do evendo que vai ser emitido') para fazer a emissão desse evento customizado que será disparado do filho (modal.vue) para o pai (app.vue)
            this.$emit('close')
            //no componente pai chamamos ele como @close, que é um @click que fará alguma coisa nessa div que o declaramos, o metodo que será chamado já é 
            //declarado no componente pai.
        }
    }
}
</script>



<style scoped> 
/* O scoped limita o css no componente que ele está sendo declarado criando um data aleatorio para os elementos do componente. */
    .modal {
        width: 400px;
        padding: 20px;
        margin: 100px auto;
        background: white;
        border-radius: 10px;
    }

    .backdrop {
        top: 0;
        position: fixed;
        background: rgba(0, 0, 0, 0.5);
        width: 100%;
        height: 100%;
    }

    h1 {
        color: green;
    }

    .modal.sale {
        background: crimson;
        color: white;
    } 
    .modal.sale h1{
        color: white;
    }
</style>