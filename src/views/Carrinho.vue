<template>
  <div>
    <div class="container-blur-carrinho" style="height:40%;  display:flex; align-items: center; justify-content: center">
            <div class="container-carrinho" style="height:100%">
                <div class="box-imagem imagem-1" style="background-size: cover;"></div>
                <div class="box-textos-carrinho">
                    <h1>GALÃO BODYBUILDING 1,3L</h1>
                    <div class="box-opcoes">
                        <router-link :to=" { path: '/registro', params:'provisorio'}" class="comprar" >Comprar Agora</router-link>
                    </div>
                </div>
            </div>
    </div>
  </div>
</template>

<script>
import * as firebase from '../plugins/firebase.js'

export default {
    data(){
        return{
            imagemGarrafa: ''
        }
    },
    mounted() {
        firebase.storage.ref(firebase.auth.currentUser.uid).getDownloadURL().then((url) => {
            this.imagemGarrafa = url
            const box = document.querySelector('.imagem-1')
            box.style.backgroundImage = 'url(' + this.imagemGarrafa + ')'
        })
        .catch((error) => {
            console.error(error)
        });
    }
}
</script>

<style>

</style>