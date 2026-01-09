### Módulo 9 – Classificação e Machine Learning

**Objetivo:** Aplicar técnicas de Machine Learning no Google Earth Engine para gerar mapas de uso e cobertura da terra, com foco em aplicações agrícolas.

---

## Aula 9.1 – Conceitos de classificação supervisionada

### Conteúdo

* O que é classificação de imagens
* Classificação supervisionada × não supervisionada
* Classes, rótulos e atributos espectrais

### Explicação

Na classificação supervisionada, o algoritmo aprende padrões espectrais a partir de amostras previamente rotuladas pelo usuário. No contexto agrícola, essas classes podem representar culturas (milho, soja, algodão), vegetação nativa, solo exposto ou água.

No GEE, a classificação é feita a partir de **Image + FeatureCollection (amostras)**, onde cada pixel recebe um rótulo com base em suas características espectrais.

---

## Aula 9.2 – Amostras de treinamento

### Conteúdo

* Criação de amostras no mapa
* FeatureCollection de treinamento
* Separação treino × validação

### Explicação

A qualidade da classificação depende diretamente das amostras. Elas devem ser:

* Representativas
* Bem distribuídas espacialmente
* Balanceadas entre classes

### Exemplo

```javascript
var samples = image.sampleRegions({
  collection: trainingSamples,
  properties: ['class'],
  scale: 10
});
```

### Exercícios

* Criar uma FeatureCollection de amostras com pelo menos 3 classes.

---

## Aula 9.3 – Random Forest no Google Earth Engine

### Conteúdo

* Conceito de Random Forest
* Parâmetros principais
* Treinamento do classificador

### Explicação

Random Forest é um algoritmo baseado em múltiplas árvores de decisão, muito robusto para dados espectrais. Ele lida bem com variabilidade, ruído e correlação entre bandas, sendo um dos modelos mais usados em mapeamento agrícola.

### Exemplo

```javascript
var classifier = ee.Classifier.smileRandomForest({
  numberOfTrees: 200
}).train({
  features: samples,
  classProperty: 'class',
  inputProperties: image.bandNames()
});
```

---

## Aula 9.4 – Aplicação do classificador e avaliação de acurácia

### Conteúdo

* Classificação da imagem
* Matriz de confusão
* Acurácia global e Kappa

### Exemplo

```javascript
var classified = image.classify(classifier);

Map.addLayer(classified, {
  min: 1,
  max: 4,
  palette: ['yellow','green','blue','brown']
}, 'Classificação');
```

### Avaliação

```javascript
var validation = classified.sampleRegions({
  collection: validationSamples,
  properties: ['class'],
  scale: 10
});

var errorMatrix = validation.errorMatrix('class', 'classification');
print('Matriz de confusão:', errorMatrix);
print('Acurácia global:', errorMatrix.accuracy());
```

### Exercícios

* Avaliar a acurácia de um mapa classificado.

---

## Aula 9.5 – Mapa final de uso e cobertura da terra

### Conteúdo

* Pós-processamento
* Aplicação de máscara
* Organização das classes

### Explicação

Após a classificação, é comum aplicar filtros espaciais, máscaras e ajustes visuais para gerar um mapa final limpo e pronto para uso técnico ou institucional.

### Exemplo

```javascript
var finalMap = classified.clip(geometry);
```

---

## 📌 Projeto Prático do Módulo 9 – Classificação agrícola com Sentinel-2

### Objetivo

Gerar um mapa de uso agrícola a partir de imagens Sentinel-2 utilizando Random Forest.

### Etapas

1. Selecionar área de estudo
2. Criar mosaico Sentinel-2
3. Calcular índices espectrais (NDVI, SAVI)
4. Criar amostras de treinamento
5. Treinar classificador Random Forest
6. Avaliar acurácia
7. Gerar mapa final

### Desafio extra

* Testar diferentes números de árvores
* Comparar classificação com e sem índices espectrais

---
