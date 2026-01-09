# 📘 Trilha Rápida GEE – Snippets Essenciais (Copy & Paste)

Este arquivo reúne **snippets prontos do Google Earth Engine**, organizados por tópico, com **explicação clara do que cada trecho faz, quando usar e boas práticas**.

👉 Ideal para revisão rápida, aulas e desenvolvimento de Apps.

---

## 1️⃣ Server-side vs Client-side

### 🔹 Server-side (ee.)

Executa no servidor do Google. Escala grande, lazy evaluation.

```javascript
var col = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterDate('2023-01-01', '2023-12-31');

var size = col.size(); // server-side
```

✅ Use para cálculos, filtros, mapas, reducers.
❌ Não use para lógica JS (if, for, console.log).

---

### 🔹 Client-side (.getInfo, .evaluate)

Executa no navegador.

```javascript
size.evaluate(function(n) {
  print('Total de imagens:', n);
});
```

⚠️ Use apenas para:

* UI
* Debug
* Listas pequenas

---

## 2️⃣ Variáveis e Tipos Comuns

```javascript
var num = ee.Number(10);
var txt = ee.String('Sentinel-2');
var geom = ee.Geometry.Point([-45, -15]);
var img = ee.Image('COPERNICUS/S2_SR/20230101T130321');
```

💡 Regra de ouro: se vem do GEE → use ee.

---

## 3️⃣ Funções Reutilizáveis

### 🔹 Função para máscara de nuvem (Sentinel-2)

```javascript
function maskClouds(img) {
  var scl = img.select('SCL');
  var mask = scl.neq(3).and(scl.neq(8)).and(scl.neq(9));
  return img.updateMask(mask);
}
```

✅ Sempre retorne `img`
✅ Use `.map()` para aplicar

---

## 4️⃣ ImageCollection – Uso Essencial

### 🔹 Filtros principais

```javascript
var col = ee.ImageCollection('COPERNICUS/S2_SR')
  .filterBounds(AOI)
  .filterDate(start, end)
  .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 10));
```

Filtros comuns:

* `filterBounds()` → AOI
* `filterDate()` → tempo
* `filter()` → metadata

---

### 🔹 Ordenar e pegar imagem específica

```javascript
var img = col.sort('system:time_start').first();
```

---

## 5️⃣ FeatureCollection – Uso Essencial

```javascript
var municipios = ee.FeatureCollection('users/asset/municipios');

var mun = municipios
  .filter(ee.Filter.eq('NM_MUN', 'Luís Eduardo Magalhães'));
```

💡 Muito usado para recortes administrativos.

---

## 6️⃣ AOI – Receber Geometria Externa (GeoJSON)

```javascript
var geojson = JSON.parse(textbox.getValue());
var AOI = ee.Geometry(geojson);
```

✅ Ideal para Apps
✅ Funciona com Polygon e MultiPolygon

---

## 7️⃣ Clip – Raster e Vetor

### 🔹 Clip raster

```javascript
var clipped = img.clip(AOI);
```

### 🔹 Interseção vetorial

```javascript
var inter = feat.geometry().intersection(AOI, 1);
```

---

## 8️⃣ Composições

### 🔹 Mediana

```javascript
var median = col.median();
```

### 🔹 Mosaico

```javascript
var mosaic = col.mosaic();
```

💡 `median` reduz ruído | `mosaic` prioriza ordem

---

## 9️⃣ Visualização

```javascript
Map.addLayer(img, {
  bands: ['B4', 'B3', 'B2'],
  min: 0,
  max: 3000,
  gamma: 1.4
}, 'RGB');
```

---

## 🔟 Stretch por Percentis

```javascript
var p = img.reduceRegion({
  reducer: ee.Reducer.percentile([5, 98]),
  geometry: AOI,
  scale: 20,
  bestEffort: true
});
```

💡 Muito usado para melhorar contraste.

---

## 1️⃣1️⃣ Exportação

### 🔹 Exportar imagem

```javascript
Export.image.toDrive({
  image: img.clip(AOI),
  description: 'sentinel_clip',
  scale: 10,
  region: AOI,
  maxPixels: 1e13
});
```

---

## 1️⃣2️⃣ UI – Componentes Essenciais

### 🔹 Label

```javascript
ui.Label('Título', {fontWeight: 'bold'});
```

### 🔹 Botão

```javascript
ui.Button({
  label: 'Executar',
  onClick: function() {
    print('Rodando');
  }
});
```

### 🔹 Panel

```javascript
var panel = ui.Panel({
  layout: ui.Panel.Layout.flow('vertical'),
  style: {width: '300px'}
});
```

---

## 1️⃣3️⃣ Boas Práticas (Checklist)

* ✅ Evite `.getInfo()` em grandes objetos
* ✅ Use funções reutilizáveis
* ✅ Separe lógica e UI
* ✅ Use nomes claros
* ❌ Evite loops JS em ImageCollection

---

📌 **Sugestão:** Use este arquivo como base para criar sua própria biblioteca pessoal de snippets.

Por exemplo : 
```javascript
function getBestSentinel2(aoi, startDate, endDate, maxCloud) {
  return ee.ImageCollection('COPERNICUS/S2_SR_HARMONIZED')
    .filterBounds(aoi)
    .filterDate(startDate, endDate)
    .filter(ee.Filter.lte('CLOUDY_PIXEL_PERCENTAGE', maxCloud))
    .sort('CLOUDY_PIXEL_PERCENTAGE')
    .first();
}
```
pega a melhor imagem sentinel 2 de acordo com intervalo de tempo e nuvens