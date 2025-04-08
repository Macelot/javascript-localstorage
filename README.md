
# 📦 Tutorial Completo: localStorage em JavaScript

O `localStorage` permite armazenar dados no navegador de forma **persistente** (mesmo após fechar o navegador) e **sem expiração**. Ele é útil para preferências de usuário, configurações e pequenas aplicações.

---

## ✅ Operações básicas

### `setItem(chave, valor)`
Armazena um valor com uma chave:

```js
localStorage.setItem('nome', 'João');
```

---

### `getItem(chave)`
Recupera o valor associado à chave:

```js
const nome = localStorage.getItem('nome');
console.log(nome); // "João"
```

---

### `removeItem(chave)`
Remove a chave e seu valor:

```js
localStorage.removeItem('nome');
```

---

### `clear()`
Remove todos os dados armazenados:

```js
localStorage.clear();
```

---

### 💡 Dica: armazenar objetos
Como o `localStorage` armazena apenas strings, use `JSON.stringify()` para salvar objetos e `JSON.parse()` para recuperá-los:

```js
const usuario = { nome: 'Ana', idade: 30 };

localStorage.setItem('usuario', JSON.stringify(usuario));

const dados = JSON.parse(localStorage.getItem('usuario'));
console.log(dados.nome); // "Ana"
```

---

## 🛠️ Exemplo completo: CRUD de Tarefas com localStorage

### HTML + JavaScript (sem frameworks):

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>CRUD com localStorage</title>
</head>
<body>
  <h2>Lista de Tarefas</h2>
  <input type="text" id="tarefaInput" placeholder="Nova tarefa">
  <button onclick="adicionarTarefa()">Adicionar</button>
  <ul id="listaTarefas"></ul>

  <script>
    function obterTarefas() {
      return JSON.parse(localStorage.getItem('tarefas')) || [];
    }

    function salvarTarefas(tarefas) {
      localStorage.setItem('tarefas', JSON.stringify(tarefas));
    }

    function renderizarTarefas() {
      const lista = document.getElementById('listaTarefas');
      lista.innerHTML = '';
      const tarefas = obterTarefas();

      tarefas.forEach((tarefa, index) => {
        const li = document.createElement('li');
        li.textContent = tarefa;

        const btnEditar = document.createElement('button');
        btnEditar.textContent = '✏️';
        btnEditar.onclick = () => editarTarefa(index);

        const btnRemover = document.createElement('button');
        btnRemover.textContent = '🗑️';
        btnRemover.onclick = () => removerTarefa(index);

        li.appendChild(btnEditar);
        li.appendChild(btnRemover);
        lista.appendChild(li);
      });
    }

    function adicionarTarefa() {
      const input = document.getElementById('tarefaInput');
      const novaTarefa = input.value.trim();

      if (novaTarefa !== '') {
        const tarefas = obterTarefas();
        tarefas.push(novaTarefa);
        salvarTarefas(tarefas);
        input.value = '';
        renderizarTarefas();
      }
    }

    function editarTarefa(index) {
      const nova = prompt('Editar tarefa:');
      if (nova !== null && nova.trim() !== '') {
        const tarefas = obterTarefas();
        tarefas[index] = nova;
        salvarTarefas(tarefas);
        renderizarTarefas();
      }
    }

    function removerTarefa(index) {
      const tarefas = obterTarefas();
      tarefas.splice(index, 1);
      salvarTarefas(tarefas);
      renderizarTarefas();
    }

    renderizarTarefas(); // inicializa ao abrir
  </script>
</body>
</html>
```

---

## 📚 Conclusão

- `localStorage` armazena dados em pares **chave/valor**, sempre como **strings**.
- Permite criar **pequenos bancos de dados locais** em aplicações web.
- É útil para temas, sessões, rascunhos e listas simples.
- Ideal para projetos educacionais e protótipos offline.

---

## 🧠 Desafio

Crie uma versão que também permita marcar tarefas como **concluídas**, armazenando isso no `localStorage`. Use um `checkbox` ou um botão de "concluir".

---
