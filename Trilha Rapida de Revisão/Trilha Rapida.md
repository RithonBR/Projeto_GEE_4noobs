# 🚀 Trilha Rápida de Revisão – Google Earth Engine

Esta trilha foi pensada como **material de consulta rápida**, ideal para revisões antes de projetos, provas, entrevistas ou desenvolvimento de Apps no GEE.

---

## 1️⃣ Server-side vs Client-side

### 🔹 Conceito

No GEE, quase tudo roda **no servidor do Google** (server-side). O código JavaScript que você escreve é apenas uma *descrição* do processamento.

| Tipo        | Onde roda    | Exemplos                                                 |
| ----------- | ------------ | -------------------------------------------------------- |
| Client-side | Navegador    | `print()`, `Map.addLayer()`, `ui.*`                      |
| Server-side | Servidor GEE | `ee.Image`, `ee.ImageCollection`, `ee.FeatureCollection` |

### 🔹 Regra de ouro

👉 **Nunca misture diretamente valores client-side com objetos `ee.*`**

### ❌ Exemplo errado

```javascript
var year = 2023;
var img = ee.ImageCollection('COPERNICUS/S2')
  .filter(ee.Filter.calendarRange(year, year, 'year'));
```

### ✅ Exemplo correto

```javascript
var year = ee.Number(2023);
var img = ee.ImageCollection('COPERNICUS/S2')
  .filter(ee.Filter.calendarRange(year, year, 'year'));
```

### 🔹 Converter server → client

```javascript
image.getInfo();      // cuidado: pesado
value.evaluate(fn);   // forma recomendada
```

📌 **Boa prática:** mantenha tudo server-side até o último momento.

---

## 2️⃣ Variáveis no GEE

### 🔹 Tipos mais comuns

```javascript
ee.Image()
ee.ImageCollection()
ee.Feature()
ee.FeatureCollection()
ee.Geometry()
ee.Number()
ee.String()
```

### 🔹 Encadeamento (chaining)

```javascript
var s2 = ee.ImageCollection('COPERNICUS/S2')
  .filterDate('2023-01-01', '2023-12-31')
  .filterBounds(aoi)
  .map(maskClouds);
```

📌 **Boa prática:** código fluido e sem variáveis desnecessárias.

---

## 3️⃣ Funções no GEE

### 🔹 Funções simples

```javascript
function addNDVI(image) {
  var ndvi = image.normalizedDifference(['B8', 'B4'])
    .rename('NDVI');
  return image.addBands(ndvi);
}
```

### 🔹 Uso com `.map()`

```javascript
var withNDVI = s2.map(addNDVI);
```

📌 **Boa prática:**

* Funções devem **retornar** um objeto `ee.*`
* Nunca usar `print()` dentro de `.map()`

---

## 4️⃣ ImageCollection

### 🔹 Conceito

Conjunto temporal de imagens raster.

### 🔹 Principais filtros

```javascript
.filterDate('2023-01-01', '2023-12-31')
.filterBounds(aoi)
.filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 10))
.filterMetadata('MGRS_TILE', 'equals', '23LMG')
```

### 🔹 Reduções temporais

```javascript
var median = s2.median();
var mosaic = s2.mosaic();
```

📌 **Boa prática:** sempre filtre **data + área + nuvem**.

---

## 5️⃣ FeatureCollection

### 🔹 Conceito

Conjunto de vetores (pontos, linhas, polígonos).

### 🔹 Filtros

```javascript
.filterBounds(aoi)
.filter(ee.Filter.eq('NM_MUN', 'Luís Eduardo Magalhães'))
```

### 🔹 Selecionar geometria

```javascript
var geom = feature.geometry();
```

📌 **Boa prática:** use atributos para seleção, não coordenadas fixas.

---

## 6️⃣ Geometria como AOI

### 🔹 AOI manual

```javascript
var aoi = ee.Geometry.Polygon([...]);
```

### 🔹 AOI via FeatureCollection

```javascript
var aoi = municipios
  .filter(ee.Filter.eq('NM_MUN', 'Luís Eduardo Magalhães'))
  .geometry();
```

📌 **Boa prática:** sempre trabalhe com `.geometry()` ao usar como AOI.

---

## 7️⃣ Clip (Raster e Vetor)

### 🔹 Clip raster

```javascript
var clipped = image.clip(aoi);
```

### 🔹 Clip vetorial

```javascript
var clippedFC = fc.filterBounds(aoi);
```

📌 **Boa prática:**

* Prefira **clip no final** do processamento
* Evite clip dentro de `.map()` quando possível

---

## 8️⃣ Composições de Imagem

### 🔹 RGB

```javascript
Map.addLayer(image, {bands:['B4','B3','B2'], min:0, max:3000});
```

### 🔹 Falsa cor

```javascript
Map.addLayer(image, {bands:['B8','B11','B4'], min:0, max:3000});
```

### 🔹 Com NDVI

```javascript
Map.addLayer(image.select('NDVI'), {min:0, max:1, palette:['red','yellow','green']});
```

📌 **Boa prática:** ajuste visual ≠ dados reais.

---

## 9️⃣ Exportação de Dados

### 🔹 Exportar imagem

```javascript
Export.image.toDrive({
  image: image,
  description: 'S2_Export',
  region: aoi,
  scale: 10,
  maxPixels: 1e13
});
```

### 🔹 Exportar tabela

```javascript
Export.table.toDrive({
  collection: samples,
  description: 'Amostras'
});
```

📌 **Boa prática:** nomeie arquivos com **data, área e sensor**.

---

## 🔟 UI – Componentes Principais

### 🔹 Textos e labels

```javascript
ui.Label('Título do App');
```

### 🔹 Botões

```javascript
ui.Button({label:'Rodar', onClick: run});
```

### 🔹 Select (dropdown)

```javascript
ui.Select({items:['2022','2023'], onChange: update});
```

### 🔹 Slider

```javascript
ui.Slider({min:0, max:100, step:5});
```

---

## 1️⃣1️⃣ UI Panel – Estrutura

```javascript
var panel = ui.Panel({
  widgets: [title, button],
  layout: ui.Panel.Layout.flow('vertical'),
  style: {width: '300px'}
});

Map.add(panel);
```

📌 **Boa prática UX:**

* Painel à esquerda
* Poucos controles
* Feedback visual ao usuário

---

## 1️⃣2️⃣ Pipeline Mental do GEE

1. Definir AOI
2. Filtrar coleção
3. Processar imagens
4. Visualizar
5. Exportar
6. (Opcional) Criar UI

---
