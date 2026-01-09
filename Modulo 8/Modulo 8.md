### Módulo 8 – Exportação de Dados

**Objetivo:** Levar resultados do Google Earth Engine para fora da plataforma de forma organizada, automatizada e profissional.

---

## Aula 8.1 – Conceitos de exportação no GEE

### Conteúdo

* Por que exportar dados
* Tipos de exportação disponíveis
* Limitações e boas práticas

### Explicação

O Google Earth Engine é uma plataforma de processamento e análise. Para uso externo (relatórios, SIG desktop, ML, bancos de dados), é necessário exportar os resultados. As exportações são feitas de forma assíncrona e devem ser bem planejadas para evitar erros e desperdício de recursos.

### Tipos de exportação

* Exportação de imagens raster
* Exportação de tabelas (vetores e estatísticas)
* Exportação para Google Drive
* Exportação para Assets

---

## Aula 8.2 – Exportação de imagens

### Conteúdo

* `Export.image.toDrive()`
* `Export.image.toAsset()`
* Parâmetros essenciais

### Exemplo

```javascript
Export.image.toDrive({
  image: image,
  description: 'Sentinel2_RGB_Jan_2023',
  folder: 'GEE_Exports',
  fileNamePrefix: 'S2_RGB_JAN_2023',
  region: geometry,
  scale: 10,
  crs: 'EPSG:4326',
  maxPixels: 1e13
});
```

### Boas práticas

* Definir corretamente a geometria
* Ajustar `scale` conforme o sensor
* Controlar `maxPixels`

### Exercícios

* Exporte uma imagem RGB e uma falsa cor.

---

## Aula 8.3 – Exportação de tabelas

### Conteúdo

* `Export.table.toDrive()`
* Exportação de FeatureCollection
* Formatos CSV e SHP

### Exemplo

```javascript
Export.table.toDrive({
  collection: stats,
  description: 'NDVI_TimeSeries',
  fileFormat: 'CSV'
});
```

### Exercícios

* Exporte estatísticas temporais em CSV.

---

## Aula 8.4 – Organização de nomes e metadados

### Conteúdo

* Padronização de nomes
* Uso de propriedades (`set()`)
* Metadados temporais e espaciais

### Explicação

Uma boa organização de nomes e metadados facilita automação, versionamento e rastreabilidade dos produtos gerados.

### Exemplo

```javascript
var img = image
  .set('municipio', 'Luis_Eduardo_Magalhaes')
  .set('data_inicio', '2023-01-01')
  .set('data_fim', '2023-01-31');
```

### Exercícios

* Adicione metadados a uma coleção de imagens.

---

## Aula 8.5 – Exportação por tile e por município

### Conteúdo

* Exportação em loop
* Uso de FeatureCollection como recorte
* Automatização de tarefas

### Exemplo – Exportação por município

```javascript
var municipios = ee.FeatureCollection('users/seu_asset/municipios');

municipios.evaluate(function(fc) {
  fc.features.forEach(function(f) {
    var geom = ee.Feature(f).geometry();
    var nome = ee.Feature(f).get('NM_MUN');

    Export.image.toDrive({
      image: image.clip(geom),
      description: nome,
      fileNamePrefix: nome,
      region: geom,
      scale: 10,
      maxPixels: 1e13
    });
  });
});
```

### Exercícios

* Automatize exportações para múltiplos municípios.

---

## 📌 Projeto Prático do Módulo 8 – Exportação automatizada Sentinel-2

### Objetivo

Automatizar a exportação de imagens Sentinel-2 por município ou tile, com nomes padronizados.

### Etapas

1. Selecionar área de estudo (municípios ou tiles)
2. Filtrar imagens Sentinel-2
3. Criar mosaicos mensais
4. Ajustar visualização
5. Exportar automaticamente

### Desafio extra

* Exportar imagens quinzenais
* Organizar pastas por ano e município

---
