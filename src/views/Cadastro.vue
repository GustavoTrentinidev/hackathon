<template>
  <div class="container-Cadastro">
        <div class="box-login">
            <h2 class="texto-login">Cadastro</h2>
        </div>
        <input placeholder="Nome" class="input-login input-nome" type="text" v-model="user.nome">
        <input placeholder="Sobrenome" class="input-login input-nome" type="text" v-model="user.sobrenome">
        <input placeholder="Email" class="input-login" type="email" v-model="user.email">
        <input placeholder="Senha" class="input-login" type="password" v-model="user.senha" >
        <input placeholder="Confirmar Senha" class="input-login" type="password" v-model="user.confirmarSenha">
        <div class="box-login">
            <a href="Login.html" class="texto-preto btn-login" @click.stop.prevent="signUp">
                <p>Cadastrar</p>
            </a>
        </div>
        <div id="pergunta-cadastro">Já possui cadastro? <router-link to="/login" id="buttonzin"> Entre </router-link></div>
    </div>
</template>

<script>
import * as firebase from '../plugins/firebase.js'

export default {
    data() {
        return {
            user: {}
        }
    },
    methods: {
        async signUp() {
            try {
                if (this.user.senha == this.user.confirmarSenha) {
                    await firebase.auth.createUserWithEmailAndPassword(this.user.email, this.user.confirmarSenha)
                    this.createProfile()
                } else {
                    alert('Campo senha e Confirmar Senha diferentes')
                }
                this.$router.push('/')
            } catch (err) {
                console.error(err.code)
            }
        },
        async createProfile() {
            console.log('aqui dentro!')
            await firebase.profilesCollection.add({
                nomeCompleto: `${this.user.nome} ${this.user.sobrenome}`,
                owner: firebase.auth.currentUser.uid
            })
        }
    }
}
</script>

<style>

</style>