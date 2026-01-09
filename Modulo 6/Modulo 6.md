### Módulo 6 – Índices Espectrais

**Objetivo:** Extrair informações biofísicas a partir de imagens de satélite no Google Earth Engine, com foco em agricultura, vegetação e recursos hídricos.

---

## Aula 6.1 – Introdução aos índices espectrais

### Conteúdo

* O que são índices espectrais
* Relação entre bandas espectrais e propriedades biofísicas
* Vantagens do uso de índices

### Explicação

Índices espectrais são combinações matemáticas entre bandas do sensor que realçam características específicas da superfície, como vigor da vegetação, umidade ou presença de água. Eles reduzem efeitos de iluminação, topografia e variabilidade espectral bruta.

### Exemplo

```javascript
var image = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-01-01','2023-01-31')
  .filterBounds(geometry)
  .median();
```

---

## Aula 6.2 – NDVI, EVI e SAVI

### Conteúdo

* NDVI (Normalized Difference Vegetation Index)
* EVI (Enhanced Vegetation Index)
* SAVI (Soil Adjusted Vegetation Index)

### Explicação

* **NDVI:** índice mais utilizado para vigor vegetal.
* **EVI:** reduz influência atmosférica e saturação.
* **SAVI:** minimiza influência do solo exposto.

### Exemplos

```javascript
var ndvi = image.normalizedDifference(['B8','B4']).rename('NDVI');

var evi = image.expression(
  '2.5 * ((NIR - RED) / (NIR + 6 * RED - 7.5 * BLUE + 1))', {
    NIR: image.select('B8'),
    RED: image.select('B4'),
    BLUE: image.select('B2')
}).rename('EVI');

var savi = image.expression(
  '((NIR - RED) / (NIR + RED + 0.5)) * (1.5)', {
    NIR: image.select('B8'),
    RED: image.select('B4')
}).rename('SAVI');
```

### Exercícios

* Compare NDVI, EVI e SAVI para áreas agrícolas.

---

## Aula 6.3 – NDWI e índices hídricos

### Conteúdo

* NDWI (água superficial)
* MNDWI
* Interpretação hidrológica

### Exemplo

```javascript
var ndwi = image.normalizedDifference(['B3','B8']).rename('NDWI');

Map.addLayer(ndwi, {
  min: -1,
  max: 1,
  palette: ['brown','white','blue']
}, 'NDWI');
```

### Exercícios

* Identifique corpos d’água na área de estudo.

---

## Aula 6.4 – Índices espectrais aplicados à agricultura

### Conteúdo

* Vigor vegetal
* Estresse hídrico
* Monitoramento fenológico

### Explicação

Índices espectrais permitem acompanhar o desenvolvimento das culturas ao longo do tempo, identificar falhas de plantio, estresse e variabilidade espacial.

### Exemplo

```javascript
var stack = image.addBands([ndvi, evi, savi]);
```

---

## Aula 6.5 – Criação de funções reutilizáveis

### Conteúdo

* Funções em JavaScript
* Aplicação em ImageCollection
* Boas práticas

### Exemplo

```javascript
var addNDVI = function(img) {
  var ndvi = img.normalizedDifference(['B8','B4']).rename('NDVI');
  return img.addBands(ndvi);
};

var collectionNDVI = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-01-01','2023-12-31')
  .filterBounds(geometry)
  .map(addNDVI);
```

### Exercícios

* Crie uma função para calcular SAVI.

---

## 📌 Projeto Prático do Módulo 6 – Série temporal de NDVI

### Objetivo

Gerar uma série temporal de NDVI para uma área agrícola.

### Etapas

1. Selecionar área de estudo
2. Filtrar imagens Sentinel-2
3. Calcular NDVI por imagem
4. Criar gráfico temporal

### Exemplo

```javascript
var chart = ui.Chart.image.series({
  imageCollection: collectionNDVI.select('NDVI'),
  region: geometry,
  reducer: ee.Reducer.mean(),
  scale: 10
});

print(chart);
```

### Desafio extra

* Criar séries temporais para diferentes talhões
* Comparar NDVI entre culturas

---
