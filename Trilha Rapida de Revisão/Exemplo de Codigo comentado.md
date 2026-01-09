```javascript
// =======================================================
// 1️⃣ DEFINIÇÃO DA ÁREA DE ESTUDO (AOI)
// =======================================================

// Aqui estamos criando uma geometria simples (polígono).
// Em projetos reais, isso pode vir de:
// - um asset
// - um GeoJSON
// - um desenho no mapa
var AOI = ee.Geometry.Rectangle([-46.7, -23.7, -46.4, -23.4]);

// Centraliza o mapa na área de interesse
Map.centerObject(AOI, 10);

// Adiciona a geometria no mapa apenas para visualização
Map.addLayer(AOI, {color: 'red'}, 'Área de Estudo');


// =======================================================
// 2️⃣ DEFINIÇÃO DO INTERVALO DE DATAS
// =======================================================

// Datas no formato YYYY-MM-DD
// O GEE trabalha com objetos ee.Date internamente
var dataInicio = '2024-06-01';
var dataFim    = '2024-06-30';


// =======================================================
// 3️⃣ CARREGAMENTO DA COLEÇÃO SENTINEL-2
// =======================================================

// COPERNICUS/S2_SR_HARMONIZED é a coleção:
// - Sentinel-2
// - Reflectância de superfície
// - Corrigida atmosfericamente
var colecaoS2 = ee.ImageCollection('COPERNICUS/S2_SR_HARMONIZED')

  // Filtra apenas imagens que intersectam a área de estudo
  .filterBounds(AOI)

  // Filtra imagens dentro do intervalo de datas definido
  .filterDate(dataInicio, dataFim)

  // Filtra imagens com até 20% de nuvens
  // CLOUDY_PIXEL_PERCENTAGE é um metadado da imagem
  .filter(ee.Filter.lte('CLOUDY_PIXEL_PERCENTAGE', 20))

  // Ordena a coleção da imagem com MENOS nuvens para MAIS nuvens
  // Isso garante que a "primeira" imagem seja a melhor
  .sort('CLOUDY_PIXEL_PERCENTAGE');


// =======================================================
// 4️⃣ SELEÇÃO DA PRIMEIRA IMAGEM DA COLEÇÃO
// =======================================================

// .first() retorna a primeira imagem da coleção ordenada
// Importante: isso ainda é SERVER-SIDE (lazy evaluation)
var imagem = ee.Image(colecaoS2.first());


// =======================================================
// 5️⃣ DEFINIÇÃO DA COMPOSIÇÃO FALSA COR (8-11-4)
// =======================================================

// Bandas escolhidas:
// B8  → Infravermelho Próximo (NIR)
// B11 → Infravermelho de Ondas Curtas (SWIR)
// B4  → Vermelho
//
// Essa combinação é muito usada para:
// - agricultura
// - análise de vegetação
// - estresse hídrico
var visParametros = {
  bands: ['B8', 'B11', 'B4'],
  min: 0,
  max: 4000,
  gamma: 1.2
};


// =======================================================
// 6️⃣ VISUALIZAÇÃO NO MAPA
// =======================================================

// Recorta a imagem para a área de interesse
// Isso NÃO altera a imagem original, apenas a visualização
var imagemClip = imagem.clip(AOI);

// Adiciona a imagem no mapa com os parâmetros definidos
Map.addLayer(imagemClip, visParametros, 'Sentinel-2 8-11-4');


// =======================================================
// 7️⃣ INFORMAÇÕES ÚTEIS PARA DEBUG E ENSINO
// =======================================================

// Mostra no console a data da imagem selecionada
print('Data da imagem:',
  ee.Date(imagem.get('system:time_start')).format('YYYY-MM-dd')
);

// Mostra a porcentagem de nuvens da imagem
print('Nuvens (%):',
  imagem.get('CLOUDY_PIXEL_PERCENTAGE')
);
```