# Módulo 3 – Trabalhando com Dados Espaciais no Google Earth Engine

**Objetivo do módulo:**
Capacitar o aluno a compreender e manipular dados espaciais vetoriais e raster no Google Earth Engine (GEE), utilizando corretamente os principais objetos da plataforma e aplicando filtros espaciais e temporais.

---

## Aula 3.1 – Conceito de Image e ImageCollection

### O que é uma Image?

No GEE, uma **Image** representa um raster geoespacial. Ela pode conter uma ou várias bandas (ex: RGB, índices espectrais, máscaras).

Exemplos de imagens:

* Uma cena Sentinel-2
* Uma imagem NDVI
* Um mapa de classificação

### Exemplo prático

```javascript
var image = ee.Image('COPERNICUS/S2_SR/20230101T131239_20230101T131237_T23LPL');
Map.centerObject(image, 8);
Map.addLayer(image, {bands: ['B4','B3','B2'], min: 0, max: 3000}, 'Sentinel-2 RGB');
```

### O que é uma ImageCollection?

Uma **ImageCollection** é um conjunto de imagens organizadas no tempo, geralmente provenientes de sensores orbitais.

Exemplos:

* Série temporal do Sentinel-2
* Série histórica do Landsat
* Produtos MODIS diários

### Exemplo prático

```javascript
var collection = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-01-01', '2023-01-31')
  .filterBounds(geometry);

print('Coleção:', collection);
```

### Exercícios

1. Carregue uma imagem Landsat 8 individual e visualize em RGB.
2. Crie uma ImageCollection do Sentinel-2 para um mês específico.

### Desafio prático

Calcule o NDVI médio de uma ImageCollection mensal.

---

## Aula 3.2 – Feature e FeatureCollection

### O que é uma Feature?

Uma **Feature** representa um objeto vetorial com:

* Geometria (ponto, linha ou polígono)
* Atributos (tabela)

### Exemplo de Feature

```javascript
var point = ee.Feature(
  ee.Geometry.Point([-49.25, -25.43]),
  {nome: 'Ponto de interesse'}
);

Map.addLayer(point, {}, 'Ponto');
```

### O que é uma FeatureCollection?

Uma **FeatureCollection** é um conjunto de Features, equivalente a um shapefile.

### Exemplo prático

```javascript
var municipios = ee.FeatureCollection('users/seu_usuario/BR_MUNICIPIOS_2024');
print(municipios);
```

### Exercícios

1. Crie uma Feature do tipo Point com um atributo.
2. Importe uma FeatureCollection e visualize no mapa.

### Desafio prático

Filtre uma FeatureCollection usando um atributo (ex: nome do município).

---

## Aula 3.3 – Importação de Assets no GEE

### O que são Assets?

Assets são dados armazenados na conta do usuário no GEE:

* Shapefiles vetoriais
* Imagens raster
* Tabelas

### Importando um asset vetorial

```javascript
var municipios = ee.FeatureCollection('users/seu_usuario/BR_MUNICIPIOS_2024');
```

### Importando um asset raster

```javascript
var imagem = ee.Image('users/seu_usuario/classificacao_milho');
```

### Exercícios

1. Importe um asset vetorial pessoal.
2. Verifique os atributos disponíveis usando `print()`.

### Desafio prático

Crie um script que selecione automaticamente um município a partir de um atributo.

---

## Aula 3.4 – Geometrias: Point, Polygon e MultiPolygon

### Tipos de Geometria

* **Point**: localização pontual
* **Polygon**: área delimitada
* **MultiPolygon**: conjunto de polígonos

### Exemplo – Polygon

```javascript
var polygon = ee.Geometry.Polygon([
  [[-49.3, -25.4], [-49.2, -25.4], [-49.2, -25.5], [-49.3, -25.5]]
]);

Map.addLayer(polygon, {color: 'red'}, 'Polígono');
```

### Exemplo – MultiPolygon

```javascript
var multi = ee.Geometry.MultiPolygon([
  [[[-49.3, -25.4], [-49.2, -25.4], [-49.2, -25.5], [-49.3, -25.5]]]
]);
```

### Exercícios

1. Crie um Polygon manualmente no código.
2. Converta uma Feature em Geometry.

### Desafio prático

Calcule a área (km²) de um polígono criado manualmente.

---

## Aula 3.5 – Filtros Espaciais e Temporais

### Filtro temporal

```javascript
var colecao = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-01-01', '2023-03-01');
```

### Filtro espacial

```javascript
var colecaoFiltrada = colecao.filterBounds(polygon);
```

### Filtro por atributo

```javascript
var municipio = municipios.filter(ee.Filter.eq('NM_MUN', 'Luís Eduardo Magalhães'));
```

### Exercícios

1. Filtre imagens por data e área.
2. Filtre municípios por nome.

### Desafio prático

Combine filtros espacial, temporal e por atributo em um único script.

---

## 📌 Projeto Prático do Módulo 3

### Tema: Seleção de Área de Estudo por Município

**Objetivo:**
Selecionar automaticamente um município brasileiro e utilizá-lo como área de estudo para análise de imagens de satélite.

**Etapas sugeridas:**

1. Importar FeatureCollection de municípios
2. Filtrar município pelo nome
3. Obter a geometria
4. Centralizar o mapa
5. Utilizar a geometria para filtrar uma ImageCollection Sentinel-2

```javascript
var municipio = municipios.filter(ee.Filter.eq('NM_MUN', 'Luís Eduardo Magalhães'));
var geom = municipio.geometry();

Map.centerObject(geom, 9);
Map.addLayer(geom, {color: 'blue'}, 'Município');
```

---