<template>
  <div class="container">
    <h1>🦁 Mural de Lágrimas rubro-negras</h1>

    <div class="input-area">
      <input type="text" v-model="novoPost" placeholder="Chore aqui, rubro-negro..." />
      <button @click="adicionarPost">Postar</button>
    </div>

    <p v-if="mensagem" :class="['mensagem', tipoMensagem]">{{ mensagem }}</p>

    <p v-if="posts.length > 0" class="contador">
      Total de posts: {{ posts.length }}
    </p>

    <p v-if="posts.length === 0" class="mensagem-vazia">
      Nenhum post ainda. Seja o primeiro a chorar!⚽
    </p>

    <ul v-else>
      <li v-for="(post, index) in posts" :key="index" class="post-card">
        <span>{{ post }}</span>
        <button @click="excluirPost(index)" class="btn-excluir">❌</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const novoPost = ref('')
    const posts = ref([])
    const mensagem = ref('')
    const tipoMensagem = ref('')

    function mostrarMensagem(texto, tipo) {
      mensagem.value = texto
      tipoMensagem.value = tipo
      setTimeout(() => {
        mensagem.value = ''
      }, 3000)
    }

    function adicionarPost() {
      if (novoPost.value.trim() === '') {
        mostrarMensagem('O post não pode estar vazio!', 'erro')
        return
      }
      posts.value.push(novoPost.value)
      novoPost.value = ''
      mostrarMensagem('Post adicionado com sucesso!', 'sucesso')
    }

    function excluirPost(index) {
      posts.value.splice(index, 1)
      mostrarMensagem('Post excluído!', 'erro')
    }

    return { novoPost, posts, mensagem, tipoMensagem, adicionarPost, excluirPost }
  }
}
</script>

<style>
body {
  margin: 0;
  font-family: "Inter", Arial, sans-serif;
  background: linear-gradient(135deg, #ff0000, #000);
  color: #fff;
}

.container {
  max-width: 600px;
  margin: 40px auto;
  background: #1a1a1a;
  padding: 30px;
  border-radius: 20px;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

h1 {
  color: #ffd700;
  text-shadow: 1px 1px 4px #000;
  margin-bottom: 25px;
}

.input-area {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
}

input {
  flex: 1;
  padding: 12px 14px;
  border-radius: 12px;
  border: 2px solid #ffd700;
  background: #000;
  color: #fff;
  outline: none;
  transition: border 0.3s, box-shadow 0.3s;
}

input::placeholder {
  color: #ffd700;
}

input:focus {
  border-color: #ff0000;
  box-shadow: 0 0 6px rgba(255, 0, 0, 0.5);
}

button {
  padding: 12px 18px;
  border: none;
  border-radius: 12px;
  background: #ff0000;
  color: #ffd700;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s, transform 0.2s;
}

button:hover {
  background: #cc0000;
  transform: translateY(-2px);
}

.mensagem {
  margin: 12px 0;
  padding: 12px;
  border-radius: 10px;
  font-size: 14px;
}

.erro {
  background: #330000;
  color: #ffd700;
  border: 1px solid #ff0000;
}

.sucesso {
  background: #003300;
  color: #ffd700;
  border: 1px solid #00ff00;
}

.contador {
  margin: 10px 0 20px;
  font-weight: 500;
  color: #ffd700;
}

ul {
  list-style: none;
  padding: 0;
}

.post-card {
  background: #330000;
  margin: 12px 0;
  padding: 14px 18px;
  border-radius: 14px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.4);
  transition: transform 0.2s, background 0.3s;
  color: #ffd700;
}

.post-card:hover {
  transform: scale(1.02);
  background: #660000;
}

.btn-excluir {
  background: #ff0000;
  color: #ffd700;
  border: none;
  padding: 6px 12px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 14px;
  transition: background 0.3s, transform 0.2s;
}

.btn-excluir:hover {
  background: #cc0000;
  transform: scale(1.1);
}

.mensagem-vazia {
  margin-top: 20px;
  font-style: italic;
  color: #ffd700;
}
</style>
