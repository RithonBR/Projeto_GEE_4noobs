### Módulo 7 – Análises Temporais

**Objetivo:** Monitorar mudanças no tempo a partir de imagens de satélite no Google Earth Engine, com foco em agricultura, vegetação e análises ambientais.

---

## Aula 7.1 – Conceito de séries temporais no GEE

### Conteúdo

* O que é uma série temporal
* Séries temporais em sensoriamento remoto
* ImageCollection como base temporal

### Explicação

Uma série temporal é uma sequência de observações ao longo do tempo. No GEE, séries temporais são construídas a partir de `ImageCollection`, onde cada imagem representa um instante temporal. Essa abordagem permite analisar dinâmica de culturas, sazonalidade e eventos extremos.

### Exemplo

```javascript
var collection = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-01-01','2023-12-31')
  .filterBounds(geometry);
```

### Exercícios

* Altere o período temporal e observe a quantidade de imagens.

---

## Aula 7.2 – Reduções temporais (mean, median, max)

### Conteúdo

* Conceito de redução temporal
* Funções `mean()`, `median()`, `max()`
* Aplicações práticas

### Explicação

Reduções temporais resumem um período inteiro em uma única imagem, reduzindo ruído e destacando padrões dominantes. São muito usadas para gerar mapas mensais, sazonais ou anuais.

### Exemplo

```javascript
var medianImage = collection.median();

Map.addLayer(medianImage, {bands:['B4','B3','B2'], min:0, max:3000}, 'Mediana Anual');
```

### Exercícios

* Compare os resultados de `mean()` e `median()`.

---

## Aula 7.3 – Análise por período (quinzenal e mensal)

### Conteúdo

* Agrupamento temporal
* Uso de loops e listas de datas
* Criação de composições periódicas

### Exemplo

```javascript
var months = ee.List.sequence(1,12);

var monthly = ee.ImageCollection.fromImages(
  months.map(function(m) {
    var start = ee.Date.fromYMD(2023, m, 1);
    var end = start.advance(1, 'month');
    return collection.filterDate(start, end).median()
      .set('month', m);
  })
);
```

### Exercícios

* Modifique o código para criar períodos quinzenais.

---

## Aula 7.4 – Extração de estatísticas temporais

### Conteúdo

* `reduceRegion()` e `reduceRegions()`
* Estatísticas por polígono
* Exportação de tabelas

### Explicação

A extração de estatísticas temporais permite transformar dados espaciais em tabelas, fundamentais para análises agronômicas, relatórios e integração com outras ferramentas.

### Exemplo

```javascript
var stats = collection.select('B8').map(function(img) {
  var mean = img.reduceRegion({
    reducer: ee.Reducer.mean(),
    geometry: geometry,
    scale: 10,
    maxPixels: 1e9
  });
  return ee.Feature(null, mean)
    .set('date', img.date().format('YYYY-MM-dd'));
});

print(stats);
```

### Exercícios

* Extraia estatísticas para múltiplos polígonos.

---

## 📌 Projeto Prático do Módulo 7 – Monitoramento de culturas agrícolas

### Objetivo

Monitorar o desenvolvimento temporal de culturas agrícolas utilizando índices espectrais.

### Etapas

1. Selecionar área agrícola (município ou talhão)
2. Filtrar imagens Sentinel-2 por safra
3. Calcular NDVI
4. Gerar séries temporais quinzenais ou mensais
5. Extrair estatísticas e visualizar gráficos

### Exemplo

```javascript
var withNDVI = collection.map(function(img) {
  var ndvi = img.normalizedDifference(['B8','B4']).rename('NDVI');
  return img.addBands(ndvi);
});

var chart = ui.Chart.image.series({
  imageCollection: withNDVI.select('NDVI'),
  region: geometry,
  reducer: ee.Reducer.mean(),
  scale: 10
});

print(chart);
```

### Desafio extra

* Comparar séries temporais entre diferentes culturas
* Identificar datas de pico vegetativo

---
