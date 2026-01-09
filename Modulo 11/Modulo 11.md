### Módulo 11 – Interface UI e Criação de Apps no GEE

**Objetivo:** Desenvolver aplicações interativas no Google Earth Engine, transformando scripts em produtos utilizáveis por usuários finais (pesquisadores, analistas, gestores e clientes).

Este módulo é um **divisor de águas** no curso: aqui o aluno deixa de apenas analisar dados e passa a **construir aplicações geoespaciais interativas**, prontas para uso e compartilhamento.

---

## 11.1 – Introdução ao módulo `ui`

O Google Earth Engine possui um módulo específico para criação de interfaces gráficas chamado **`ui`**. Ele permite construir painéis, botões, seletores e mapas interativos diretamente no Code Editor.

### Conceitos-chave

* O módulo `ui` roda no **client-side**
* Serve como ponte entre o usuário e as análises server-side
* Permite criar Apps sem necessidade de frameworks externos

### Exemplo básico

```javascript
var label = ui.Label('Meu primeiro App no GEE');
Map.add(label);
```

### Boas práticas

* Use `ui` apenas para interação e visualização
* Evite colocar lógica pesada dentro de eventos de UI

---

## 11.2 – Conceitos de UI no GEE (Panels, Widgets e Layouts)

A interface no GEE é construída a partir de **widgets**, organizados dentro de **panels**.

### Principais Widgets

* `ui.Label` – textos
* `ui.Button` – botões
* `ui.Select` – dropdowns
* `ui.Slider` – sliders
* `ui.Checkbox` – caixas de seleção

### Panels

Panels funcionam como containers visuais.

```javascript
var panel = ui.Panel({
  style: {width: '300px'}
});
panel.add(ui.Label('Painel lateral'));
ui.root.insert(0, panel);
```

### Layouts

* `flow('vertical')`
* `flow('horizontal')`

### Boas práticas

* Use painéis laterais para controles
* Deixe o mapa o mais limpo possível

---

## 11.3 – Criação de botões, sliders, dropdowns e checkboxes

### Botões

```javascript
var button = ui.Button({
  label: 'Executar análise',
  onClick: function() {
    print('Botão clicado');
  }
});
```

### Sliders

```javascript
var slider = ui.Slider({
  min: 0,
  max: 100,
  value: 50,
  onChange: function(value) {
    print('Valor:', value);
  }
});
```

### Dropdown (Select)

```javascript
var select = ui.Select({
  items: ['Sentinel-2', 'Landsat 8'],
  onChange: function(value) {
    print('Selecionado:', value);
  }
});
```

### Checkboxes

```javascript
var checkbox = ui.Checkbox('Mostrar NDVI', true);
```

### Boas práticas

* Use labels explicativos
* Evite sobrecarregar a interface

---

## 11.4 – Eventos e interatividade (onClick, onChange)

Eventos conectam a UI às análises.

### Exemplos

* `onClick`: executar ações
* `onChange`: atualizar mapas dinamicamente

```javascript
button.onClick(function() {
  Map.clear();
});
```

### Boas práticas

* Limpe camadas antes de adicionar novas
* Use funções reutilizáveis

---

## 11.5 – Controle de camadas e mapas dinâmicos

É possível adicionar e remover camadas dinamicamente.

```javascript
Map.addLayer(image, visParams, 'Imagem');
```

### Controle manual

* `Map.layers().reset()`
* `Map.clear()`

### Boas práticas

* Nomeie camadas corretamente
* Use transparência (`opacity`)

---

## 11.6 – Organização visual e boas práticas de UX

### Princípios de UX no GEE

* Simplicidade
* Clareza
* Consistência

### Recomendações

* Um objetivo por App
* Fluxo lógico de interação
* Feedback visual ao usuário

### Estrutura sugerida

* Painel lateral: controles
* Mapa: visualização
* Rodapé: créditos e instruções

---

## 11.7 – Publicação e compartilhamento de Apps

O GEE permite publicar Apps diretamente.

### Etapas

1. Clique em **Apps**
2. Configure nome e descrição
3. Defina permissões

### Tipos de compartilhamento

* Privado
* Público
* Link direto

### Boas práticas

* Descrição clara do App
* Créditos e fontes de dados
* Versão e data

---

## 📌 Projeto prático – App interativo para visualização temporal de imagens Sentinel-2

### Objetivo

Criar um App que permita:

* Selecionar município
* Escolher período
* Alternar entre RGB e NDVI

### Funcionalidades mínimas

* Dropdown de município
* Slider temporal
* Botão de atualização
* Mapa interativo

### Desafio extra 🚀

* Adicionar gráfico temporal
* Exportação sob demanda

---
