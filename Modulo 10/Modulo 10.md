### Módulo 10 – Automação e Scripts Avançados

**Objetivo:** Escalar análises no Google Earth Engine por meio de automação, organização de código e boas práticas de performance, preparando o aluno para fluxos profissionais e projetos de grande escala.

---

## Aula 10.1 – Loops e funções avançadas no GEE

### Conteúdo

* Funções puras em JavaScript
* Uso de `map()` em ImageCollection e FeatureCollection
* Diferença entre `for` (client-side) e `map` (server-side)

### Explicação

No GEE, a automação eficiente depende do uso correto de funções server-side. Laços tradicionais (`for`) devem ser evitados para operações sobre grandes volumes de dados, dando preferência a `map()` e estruturas funcionais.

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

* Criar uma função que calcule dois índices espectrais e adicione como bandas.

---

## Aula 10.2 – Processamento por múltiplas áreas

### Conteúdo

* Uso de FeatureCollection como lista de áreas
* Processamento em lote
* Recorte e estatísticas por polígono

### Explicação

Projetos reais normalmente envolvem múltiplas áreas (municípios, talhões, tiles). O GEE permite escalar esse processamento utilizando FeatureCollection como base espacial.

### Exemplo

```javascript
var municipios = ee.FeatureCollection('users/seu_asset/municipios');

var results = municipios.map(function(feat) {
  var geom = feat.geometry();
  var meanNDVI = collectionNDVI.select('NDVI').mean()
    .reduceRegion({
      reducer: ee.Reducer.mean(),
      geometry: geom,
      scale: 10,
      maxPixels: 1e9
    });

  return feat.set(meanNDVI);
});

print(results);
```

### Exercícios

* Calcular NDVI médio para vários municípios.

---

## Aula 10.3 – Organização de pipelines de processamento

### Conteúdo

* Separação por etapas (input → processamento → output)
* Modularização de código
* Reutilização de funções

### Explicação

Pipelines organizados facilitam manutenção, escalabilidade e reaproveitamento de código. Um bom script deve ser legível, modular e documentado.

### Exemplo de estrutura

```javascript
// 1. Inputs
// 2. Funções
// 3. Processamento
// 4. Visualização
// 5. Exportação
```

### Exercícios

* Reorganizar um script antigo seguindo essa estrutura.

---

## Aula 10.4 – Boas práticas e otimização

### Conteúdo

* Redução de volume de dados
* Uso correto de escala
* Evitar `getInfo()`
* Controle de `maxPixels`

### Explicação

Scripts ineficientes podem falhar ou demorar excessivamente. A otimização garante performance, economia de recursos e maior confiabilidade dos resultados.

### Boas práticas

* Sempre filtrar espacial e temporalmente
* Trabalhar com bandas necessárias
* Preferir reducers simples

### Exercícios

* Otimizar um script lento fornecido.

---

## 📌 Projeto Prático do Módulo 10 – Pipeline automático de mapeamento

### Objetivo

Criar um pipeline automatizado de mapeamento agrícola capaz de processar múltiplas áreas e períodos de forma escalável.

### Etapas

1. Definir áreas de estudo (FeatureCollection)
2. Filtrar imagens Sentinel-2
3. Criar mosaicos periódicos
4. Calcular índices espectrais
5. Classificar imagens
6. Exportar resultados automaticamente

### Desafio extra

* Criar logs com propriedades
* Automatizar exportações por ano e município

---
