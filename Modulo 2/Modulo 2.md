# Módulo 2 – Fundamentos de JavaScript para Google Earth Engine

Este módulo ensina **exatamente o JavaScript necessário para trabalhar com o Google Earth Engine**, focando na lógica correta da plataforma, evitando erros comuns e preparando o aluno para scripts reais de análise espacial.

---

## Aula 2.1 – O JavaScript dentro do Google Earth Engine

### Objetivo da aula

Compreender o papel do JavaScript no GEE e como ele difere do JavaScript tradicional usado em navegadores.

### Conteúdo

* JavaScript como linguagem de controle no GEE
* Diferença entre JavaScript puro e JavaScript no GEE
* Introdução ao conceito de objetos do Earth Engine (`ee`)

### Exemplo prático

```javascript
// JavaScript comum
var numero = 10;
print(numero);

// Objeto do Earth Engine
var numeroEE = ee.Number(10);
print(numeroEE);
```

👉 Aqui já surge a primeira diferença importante: objetos `ee.*` são processados no **servidor**, não no navegador.

---

## Aula 2.2 – Variáveis, tipos de dados e objetos `ee`

### Objetivo da aula

Entender os principais tipos de dados usados no GEE.

### Conteúdo

* Variáveis (`var`, `let`, `const`)
* Tipos básicos: Number, String, Boolean
* Tipos do GEE: `ee.Number`, `ee.String`, `ee.List`, `ee.Dictionary`

### Exemplo prático

```javascript
var nome = 'Google Earth Engine';
var ano = ee.Number(2025);

print(nome);
print(ano);
```

⚠️ Nunca misture operações diretas entre tipos JavaScript e tipos `ee`.

---

## Aula 2.3 – Server-side vs Client-side (na prática)

### Objetivo da aula

Dominar o conceito mais importante do GEE.

### Conteúdo

* O que roda no servidor
* O que roda no cliente
* Função `print()` e `getInfo()`

### Exemplo prático

```javascript
var area = ee.Geometry.Point([-45, -12]).buffer(1000);

// Server-side
print('Área:', area.area());

// Client-side (não recomendado em loops grandes)
var areaValor = area.area().getInfo();
print('Área em metros:', areaValor);
```

👉 Regra de ouro: **use `getInfo()` apenas para testes pequenos**.

---

## Aula 2.4 – Listas e dicionários no GEE

### Objetivo da aula

Trabalhar com estruturas de dados no servidor.

### Conteúdo

* `ee.List`
* `ee.Dictionary`
* Acesso a elementos

### Exemplo prático

```javascript
var bandas = ee.List(['B2', 'B3', 'B4']);
print(bandas);

var info = ee.Dictionary({
  sensor: 'Sentinel-2',
  resolucao: 10
});

print(info.get('sensor'));
```

---

## Aula 2.5 – Funções no JavaScript aplicadas ao GEE

### Objetivo da aula

Criar funções reutilizáveis para processamento espacial.

### Conteúdo

* Funções anônimas
* Funções aplicadas a objetos `ee`

### Exemplo prático

```javascript
function calcularNDVI(imagem) {
  return imagem.normalizedDifference(['B8', 'B4'])
               .rename('NDVI');
}
```

---

## Aula 2.6 – Map() e iteração no servidor

### Objetivo da aula

Aprender a iterar corretamente sobre coleções.

### Conteúdo

* `map()` em `ImageCollection`
* Diferença entre `for` e `map()`

### Exemplo prático

```javascript
var colecao = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-01-01', '2023-12-31');

var ndviCol = colecao.map(function(img) {
  return img.normalizedDifference(['B8', 'B4'])
            .rename('NDVI');
});

print(ndviCol);
```

---

## Aula 2.7 – Condições e lógica (if, where, masks)

### Objetivo da aula

Aplicar lógica condicional no GEE.

### Conteúdo

* `ee.Algorithms.If`
* Máscaras

### Exemplo prático

```javascript
var img = ee.Image(0).where(ee.Image(1), 1);
print(img);
```

---

## Aula 2.8 – Boas práticas e erros comuns

### Objetivo da aula

Evitar erros clássicos e escrever código limpo.

### Conteúdo

* Evitar `for` em objetos `ee`
* Nomear variáveis corretamente
* Testar com áreas pequenas

### Checklist final

* ❌ Não usar `getInfo()` em grandes volumes
* ✅ Usar `map()`
* ✅ Pensar sempre em server-side

---

## Exercícios e Desafios do Módulo 2

A seguir, cada aula possui **exercícios práticos (fixação)** e um **desafio** para estimular o raciocínio e a autonomia no Google Earth Engine.

---

### Aula 2.1 – O JavaScript dentro do Google Earth Engine

**Exercícios**

1. Crie uma variável JavaScript comum e imprima no console.
2. Crie um objeto `ee.Number` e imprima no console.
3. Observe a diferença visual entre os dois resultados no painel Console.

**Desafio**

* Explique, em um comentário no código, por que o `ee.Number` não retorna um valor imediato.

---

### Aula 2.2 – Variáveis, tipos de dados e objetos `ee`

**Exercícios**

1. Crie uma string com o nome de um sensor.
2. Crie um `ee.Number` representando um ano.
3. Imprima ambos no console.

**Desafio**

* Tente somar um número JavaScript com um `ee.Number` e observe o erro. Depois, escreva um comentário explicando por que isso acontece.

---

### Aula 2.3 – Server-side vs Client-side

**Exercícios**

1. Crie uma geometria simples (Point ou Polygon).
2. Calcule a área da geometria usando `area()`.
3. Imprima o resultado diretamente com `print()`.

**Desafio**

* Use `getInfo()` para obter o valor da área e explique por que esse método deve ser evitado em grandes processamentos.

---

### Aula 2.4 – Listas e dicionários no GEE

**Exercícios**

1. Crie uma `ee.List` com nomes de bandas do Sentinel-2.
2. Crie um `ee.Dictionary` com informações do sensor.
3. Acesse um valor específico do dicionário usando `get()`.

**Desafio**

* Crie um dicionário contendo bandas e resoluções e imprima cada valor usando `map()`.

---

### Aula 2.5 – Funções no JavaScript aplicadas ao GEE

**Exercícios**

1. Crie uma função que receba uma imagem e calcule o NDVI.
2. Retorne a imagem com a banda NDVI adicionada.

**Desafio**

* Adapte a função para calcular outro índice de vegetação (ex: NDWI ou EVI).

---

### Aula 2.6 – Map() e iteração no servidor

**Exercícios**

1. Carregue uma `ImageCollection` Sentinel-2.
2. Use `map()` para aplicar uma função NDVI.
3. Imprima a coleção resultante.

**Desafio**

* Filtre a coleção por uma data específica antes de aplicar o `map()`.

---

### Aula 2.7 – Condições e lógica no GEE

**Exercícios**

1. Crie uma imagem constante.
2. Aplique uma condição usando `where()`.
3. Visualize o resultado no mapa.

**Desafio**

* Crie uma máscara que remova valores abaixo de um determinado limiar.

---

### Aula 2.8 – Boas práticas e erros comuns

**Exercícios**

1. Pegue um script anterior e reorganize os comentários.
2. Renomeie variáveis para deixá-las mais claras.

**Desafio**

* Identifique um erro comum de server-side em um script antigo e explique como corrigi-lo.

---
