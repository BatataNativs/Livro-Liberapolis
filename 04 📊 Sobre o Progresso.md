---
aliases:
  - Progresso
  - Guia de Progresso
  - Tutorial Dataview
tags:
  - projeto/literatura
  - liberápolis
  - tutorial
  - dataview
---

# 📊 Sobre o Progresso

> Guia de acompanhamento do desenvolvimento de **Liberápolis**.

---

## 🎯 Finalidade

O sistema de progresso serve para acompanhar a evolução real do projeto sem transformar toda tarefa pequena em uma falsa sensação de avanço.

A barra principal da [[00 🏠 HOME|Home]] mede apenas os **marcos estruturais** de *Liberápolis*: fundamentos, universo, personagens, trama e redação.

Ela **não** deve medir tarefas avulsas, rápidas ou temporárias, como “reler uma nota”, “corrigir uma frase” ou “pesquisar um nome”.

---

## 🧩 Como funciona

A barra da Home usa o plugin comunitário **Dataview**.

Ela procura, dentro da própria Home, todas as caixas de tarefa que contêm a tag `#projeto`.

Exemplo:

```md
- [ ] Premissa consolidada #projeto
- [x] Temas definidos #projeto
```

No exemplo acima:

- A primeira tarefa ainda está pendente.
- A segunda tarefa está concluída.
- As duas entram no cálculo da barra porque têm `#projeto`.
- Uma tarefa sem `#projeto` não altera o progresso do projeto.

> **Regra principal:** use `#projeto` somente para etapas relevantes e mensuráveis da construção do livro.

---

## ⚙️ Instalação do Dataview

O Dataview não vem ativado por padrão no Obsidian. É necessário instalá-lo uma vez.

### Instalar o plugin

1. Abra o Obsidian.
2. Clique em **Configurações**.
3. Abra **Plugins da comunidade**.
4. Desative o **Modo restrito**, se ele estiver ativo.
5. Clique em **Explorar**.
6. Pesquise por `Dataview`.
7. Instale o plugin chamado **Dataview**.
8. Clique em **Ativar**.

### Habilitar JavaScript

A barra da Home usa um bloco `dataviewjs`, isto é, uma consulta feita em JavaScript.

Depois de instalar:

1. Abra **Configurações**.
2. Vá até **Plugins da comunidade**.
3. Clique em **Dataview**.
4. Ative a opção **Enable JavaScript Queries**.

> ⚠️ **Segurança:** blocos `dataviewjs` executam código JavaScript no seu cofre. Use apenas códigos que você compreenda ou que tenha revisado antes de colar.

---

## 📈 A barra da Home

Este é o código que está na seção **📈 Progresso do projeto** da [[00 🏠 HOME|Home]]:

````md
```dataviewjs
const tarefas = dv.current().file.tasks
  .where(t => t.text.includes("#projeto"));

const total = tarefas.length;
const concluidas = tarefas.where(t => t.completed).length;
const percentual = total === 0 ? 0 : Math.round((concluidas / total) * 100);

dv.paragraph(`
<progress value="${percentual}" max="100" style="width: 100%; height: 24px;"></progress>

**${percentual}% concluído** — ${concluidas} de ${total} marcos estruturais finalizados
`);
```