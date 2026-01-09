# Módulo 4 – Imagens de Satélite no Google Earth Engine (GEE)

## Objetivo do módulo

Dominar o uso de **coleções de imagens de satélite no Google Earth Engine**, compreendendo as diferenças entre sensores, resoluções e aplicações, além de aprender a **filtrar, visualizar e baixar imagens**, com foco em Sentinel‑2.

---

## Aula 4.1 – O que são imagens de satélite no GEE

### Explicação

No GEE, imagens de satélite são representadas como objetos `ee.Image` organizados em **coleções temporais (`ee.ImageCollection`)**. Cada imagem é composta por pixels, bandas espectrais e metadados.

Diferente de um SIG tradicional, o GEE não trabalha com arquivos locais, mas com **catálogos globais prontos para uso**.

### Exemplo

```javascript
var imagem = ee.Image('CGIAR/SRTM90_V4');
print(imagem);
```

---

## Aula 4.2 – Principais sensores disponíveis no GEE

### Explicação

O GEE possui dezenas de sensores, mas alguns são fundamentais:

* **Sentinel‑2** → alta resolução espacial (10–20 m)
* **Landsat 5, 7, 8 e 9** → séries históricas desde 1984
* **MODIS** → alta resolução temporal (diária)

Cada sensor atende a um tipo de análise diferente.

---

## Aula 4.3 – Sentinel‑2 no GEE

### Explicação

O Sentinel‑2 é um dos sensores mais usados em agricultura e meio ambiente devido à sua alta resolução espacial e bandas no visível, infravermelho e red‑edge.

Principais características:

* Resolução: 10 m, 20 m e 60 m
* Revisita: ~5 dias

### Exemplo

```javascript
var s2 = ee.ImageCollection('COPERNICUS/S2_SR');
print(s2.first().bandNames());
```

---

## Aula 4.4 – Landsat 5, 7, 8 e 9

### Explicação

A série Landsat permite análises históricas de longo prazo.

* Landsat 5 → 1984–2013
* Landsat 7 → 1999–presente (com falhas após 2003)
* Landsat 8 e 9 → sensores mais recentes

### Exemplo

```javascript
var landsat8 = ee.ImageCollection('LANDSAT/LC08/C02/T1_L2');
print(landsat8.first().bandNames());
```

---

## Aula 4.5 – MODIS: alta resolução temporal

### Explicação

O MODIS é ideal para análises temporais contínuas (clima, vegetação, incêndios), sacrificando resolução espacial.

* Resolução espacial: 250 m a 1 km
* Resolução temporal: diária

### Exemplo

```javascript
var modis = ee.ImageCollection('MODIS/006/MOD13Q1');
print(modis.first());
```

---

## Aula 4.6 – Resolução espacial, temporal e espectral

### Explicação

Todo sensor é definido por três resoluções:

* **Espacial** → tamanho do pixel
* **Temporal** → frequência de revisita
* **Espectral** → número e posição das bandas

Compreender essas resoluções é essencial para escolher o sensor correto.

### Exemplo comparativo

```javascript
// Sentinel-2 (10 m)
// MODIS (250 m)
```

---

## Aula 4.7 – Filtragem de imagens

### Explicação

Antes de qualquer análise, é necessário filtrar as coleções:

* Por data (`filterDate`)
* Por área (`filterBounds`)
* Por metadados (ex: nuvem)

### Exemplo

```javascript
var s2Filtrado = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-01-01', '2023-03-31')
  .filterBounds(geometry);

print(s2Filtrado.size());
```

---

## Aula 4.8 – Filtro por nuvens

### Explicação

A presença de nuvens compromete análises. O Sentinel‑2 possui bandas QA específicas para identificar nuvens.

### Exemplo simplificado

```javascript
function maskClouds(image) {
  var qa = image.select('QA60');
  var mask = qa.eq(0);
  return image.updateMask(mask);
}
```

---

## Aula 4.9 – Visualização de imagens de satélite

### Explicação

A visualização correta depende da escolha das bandas e do ajuste de contraste.

### Exemplo – RGB Sentinel‑2

```javascript
var imagemRGB = s2Filtrado.first();
Map.addLayer(imagemRGB, {
  bands: ['B4', 'B3', 'B2'],
  min: 0,
  max: 3000
}, 'Sentinel‑2 RGB');
```

---

## Aula 4.10 – Projeto prático: Download e visualização de imagens Sentinel‑2

### Projeto guiado

O aluno deverá:

1. Definir uma área de estudo
2. Carregar a coleção Sentinel‑2
3. Filtrar por data e área
4. Aplicar filtro de nuvens
5. Visualizar a imagem RGB
6. Exportar a imagem para o Google Drive

### Exemplo de exportação

```javascript
Export.image.toDrive({
  image: imagemRGB,
  description: 'Sentinel2_RGB',
  scale: 10,
  region: geometry,
  maxPixels: 1e13
});
```

---
