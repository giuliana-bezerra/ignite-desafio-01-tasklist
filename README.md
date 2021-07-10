<h1 align="center">
  <img alt="letmeask" title="todo" src=".github/logo.svg" />
</h1>

<p align="center">
  <a href="#-tecnologias">Tecnologias</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-projeto">Projeto</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-layout">Layout</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-como-executar">Como executar</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-licença">Licença</a>
</p>

<p align="center">
  <img alt="License" src="https://img.shields.io/static/v1?label=license&message=MIT&color=8257E5&labelColor=000000">

 <img src="https://img.shields.io/static/v1?label=Ignite&message=Desafio-01&color=8257E5&labelColor=000000" alt="Desafio-01" />
</p>

<br>

<img alt="letmeask" src=".github/todo.gif" width="100%">

## ✨ Tecnologias

Esse projeto foi desenvolvido com as seguintes tecnologias:

- [ReactJS](https://reactjs.org)
- [TypeScript](https://www.typescriptlang.org/)

## 💻 Projeto

O Todo é é uma pequena aplicação de atividades a fazer, para treinar um pouco mais sobre manipulação do estado no React.

## 🔖 Solução

Esse desafio foi resolvido da seguinte forma:

* Criação de novas tarefas: A primeira coisa a fazer é validar se a tarefa possui um título válido:
    ```ts
    if (!newTaskTitle.trim()) return;
    ```
    O trim se encarrega de checar também espaços em brancos, para maior segurança.
    O próximo passo é criar a nova tarefa a ser adicionada:
    ```ts
    const newTask: Task = {
      id: Math.random(),
      title: newTaskTitle.trim(),
      isComplete: false,
    };
    ```
    Como o id não é fornecido pelo usuário, foi necessário gerar um aleatório com a função Math.random.
    Finalmente, podemos adicionar a nova tarefa criada à lista de tarefas. Aqui entra um detalhe importante, o React trabalha com o conceito de imutabilidade do estado dos componentes. Isso significa que eu não posso simplesmente adicionar a nova tarefa à lista que existe no estado. Eu preciso criar um novo array que acomode essa mudança como feito abaixo:
    ```ts
    setTasks([...tasks, newTask]);
    ```
    Feito isso está pronta a funcionalidade de criação de novas tarefas.
* Marcar/Desmarcar tarefas como completas: Agora existe um cenário em que precisamos mudar uma tarefa em particular dentro da lista. Para manter a imutabilidade, foi criada uma cópia do array de tarefas:
    ```ts
    const newTasks = [...tasks];
    ```
    Essa cópia poderá ser modificada para marcar ou desmarcar a tarefa como completa. Para isso, primeiro é necessário procurar a tarefa pelo id dentro da lista e só então alterar a propriedade isComplete:
    ```ts
    newTasks.forEach((task) => {
      if (task.id === id) task.isComplete = !task.isComplete;
    });
    ```
    Feito isso, como foi criado um novo array de tarefas, falta apenas atribuí-lo ao estado do componente React:
    ```ts
    setTasks(newTasks);
    ```
* Remover tarefa: A remoção é similar à atualização. É necessário remover uma tarefa da lista de tarefas sem modificar o estado diretamente. Para isso, foi criada uma cópia do array de tarefas:
    ```ts
    let newTasks = [...tasks];
    ```
    Agora será possível filtrar as tarefas excluindo apenas a que possui o id informado para a remoção:
    ```ts
    newTasks = newTasks.filter((task) => task.id !== id);
    ```
    Com o array atualizado, basta colocá-lo no estado para persistir a mudança na lista de tarefas:
    ```ts
    setTasks(newTasks);
    ```

## 🚀 Como executar

- Clone o repositório
- Instale as dependências com `yarn`
- Inicie o servidor com `yarn dev`

Agora você pode acessar [`localhost:8080`](http://localhost:8080) do seu navegador.

## 📄 Licença

Esse projeto está sob a licença MIT.

---
