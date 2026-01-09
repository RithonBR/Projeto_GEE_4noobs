### Módulo 5 – Visualização e Composição de Imagens

**Objetivo:** Criar mapas profissionais no Google Earth Engine, com foco em visualização, composição temporal e comunicação cartográfica.

---

## Aula 5.1 – Conceitos de visualização de imagens no GEE

### Conteúdo

* Diferença entre dado e visualização
* Parâmetros do `Map.addLayer()`
* Bandas, min/max e gamma

### Explicação

No GEE, a visualização não altera os dados originais. Ela apenas define como os valores numéricos das bandas serão representados em cores na tela. Um mesmo raster pode gerar múltiplos mapas visuais diferentes.

### Exemplo de código

```javascript
var image = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-06-01', '2023-06-30')
  .filterBounds(geometry)
  .first();

Map.centerObject(geometry, 9);
Map.addLayer(image, {bands: ['B4','B3','B2'], min: 0, max: 3000}, 'RGB');
```

### Exercícios

1. Altere os valores de `min` e `max` e observe o impacto.
2. Teste diferentes combinações de bandas.

---

## Aula 5.2 – Visualização RGB e Falsa Cor

### Conteúdo

* Composição RGB verdadeira
* Falsa cor com infravermelho próximo
* Interpretação visual

### Exemplo

```javascript
Map.addLayer(image, {bands: ['B8','B4','B3'], min: 0, max: 3000}, 'Falsa Cor');
```

### Exercícios

* Compare áreas de vegetação e solo exposto nas duas composições.

---

## Aula 5.3 – Ajuste de contraste por percentis

### Conteúdo

* Problema de outliers
* Uso de `reduceRegion()`
* Percentis 2–98 e 5–95

### Exemplo

```javascript
var stats = image.reduceRegion({
  reducer: ee.Reducer.percentile([5, 95]),
  geometry: geometry,
  scale: 10,
  maxPixels: 1e9
});

var vis = {
  bands: ['B4','B3','B2'],
  min: stats.get('B4_p5'),
  max: stats.get('B4_p95')
};

Map.addLayer(image, vis, 'RGB Contrastado');
```

### Exercícios

* Teste percentis diferentes.

---

## Aula 5.4 – Criação de mosaicos

### Conteúdo

* `mosaic()`
* `median()`, `mean()` e `qualityMosaic()`
* Diferença entre mosaico espacial e temporal

### Exemplo

```javascript
var mosaic = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-01-01','2023-01-31')
  .filterBounds(geometry)
  .median();

Map.addLayer(mosaic, {bands: ['B4','B3','B2'], min: 0, max: 3000}, 'Mosaico Janeiro');
```

### Exercícios

* Compare mosaico `median` e `mean`.

---

## Aula 5.5 – Paletas de cores

### Conteúdo

* Paletas contínuas e categóricas
* Uso de `palette`
* Comunicação cartográfica

### Exemplo

```javascript
var ndvi = image.normalizedDifference(['B8','B4']);

Map.addLayer(ndvi, {
  min: -1,
  max: 1,
  palette: ['red','yellow','green']
}, 'NDVI');
```

### Exercícios

* Crie uma paleta personalizada.

---

## Aula 5.6 – Criação de mapas interativos

### Conteúdo

* Ativar/desativar camadas
* Organização de layers
* Introdução ao uso de UI (preview do próximo módulo)

### Exemplo

```javascript
Map.addLayer(image, {bands:['B4','B3','B2'], min:0, max:3000}, 'RGB', true);
Map.addLayer(ndvi, {min:-1, max:1, palette:['red','yellow','green']}, 'NDVI', false);
```

---

## 📌 Projeto Prático do Módulo 5 – Mosaico mensal contrastado

### Objetivo

Criar um mosaico mensal Sentinel-2 com ajuste automático de contraste por percentis.

### Etapas

1. Selecionar área de estudo
2. Filtrar imagens Sentinel-2 por mês
3. Criar mosaico (median)
4. Aplicar contraste por percentis
5. Visualizar em RGB e falsa cor

### Desafio extra

* Criar um loop mensal automático
* Gerar um mosaico para cada mês do ano

---
