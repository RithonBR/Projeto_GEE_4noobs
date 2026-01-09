### Módulo 12 – Integração com Python e Google Colab

**Objetivo:** Expandir o uso do Google Earth Engine para fora do Code Editor, integrando análises com Python, Google Colab e ambientes GIS locais, permitindo automação, escalabilidade e integração com pipelines de ciência de dados.

Este módulo mostra como o GEE deixa de ser apenas uma ferramenta online e passa a fazer parte de **fluxos profissionais de análise geoespacial**, ciência de dados e Machine Learning.

---

## 12.1 – Earth Engine com Python

Além do JavaScript no Code Editor, o Google Earth Engine possui uma **API oficial em Python**, muito utilizada para:

* automação de processos
* integração com bancos de dados
* pipelines de ML
* execução em servidores ou notebooks

### Diferença principal

* JavaScript (Code Editor): foco em visualização e Apps
* Python API: foco em automação, análise e integração

### Instalação da API

```python
pip install earthengine-api
```

### Importação

```python
import ee
ee.Initialize()
```

### Boas práticas

* Use Python para processamento em lote
* Use o Code Editor para prototipagem visual

---

## 12.2 – Autenticação e configuração do ambiente

Para usar o GEE em Python é necessário autenticar sua conta Google.

### Autenticação local

```python
ee.Authenticate()
ee.Initialize()
```

Após executar, será solicitado:

1. Login com conta Google
2. Autorização do Earth Engine
3. Inserção do token

### Boas práticas

* Autentique apenas uma vez por ambiente
* Nunca compartilhe tokens

---

## 12.3 – Integração com Google Colab

O **Google Colab** é um ambiente ideal para trabalhar com o GEE, pois:

* não exige instalação local
* integra Python, gráficos e mapas
* permite compartilhamento fácil

### Instalação no Colab

```python
!pip install earthengine-api
```

### Autenticação no Colab

```python
import ee
ee.Authenticate()
ee.Initialize()
```

### Visualização de mapas (geemap)

```python
!pip install geemap
import geemap
Map = geemap.Map()
Map
```

### Boas práticas

* Use Colab para notebooks demonstrativos
* Salve resultados no Google Drive

---

## 12.4 – Fluxo GEE + Python + GIS local

Um fluxo profissional típico envolve:

1. Processamento no GEE
2. Exportação via Python
3. Análise em GIS local (QGIS, ArcGIS)
4. Pós-processamento ou ML

### Exemplo: acessar ImageCollection

```python
collection = (ee.ImageCollection('COPERNICUS/S2_SR')
              .filterDate('2023-01-01', '2023-01-31')
              .filterBounds(ee.Geometry.Point(-45, -12)))
```

### Redução temporal

```python
image = collection.median()
```

### Exportação

```python
task = ee.batch.Export.image.toDrive(
    image=image,
    description='sentinel2_median',
    scale=10,
    region=ee.Geometry.Point(-45, -12).buffer(5000)
)
task.start()
```

### Boas práticas

* Organize nomes e pastas
* Salve metadados junto aos outputs

---

## 12.5 – Automação e pipelines em Python

Com Python é possível criar **pipelines automáticos**.

### Exemplo: loop por datas

```python
import datetime

start = datetime.date(2023, 1, 1)
end = datetime.date(2023, 3, 1)

current = start
while current < end:
    next_date = current + datetime.timedelta(days=30)
    print(current, next_date)
    current = next_date
```

### Integração com GEE

* loops por município
* exportações em lote
* análises temporais

### Boas práticas

* Controle erros e logs
* Evite loops client-side desnecessários

---

## 📌 Projeto prático – Pipeline automatizado via Python

### Objetivo

Criar um pipeline que:

* selecione municípios
* filtre imagens Sentinel-2
* gere mosaicos mensais
* exporte automaticamente

### Etapas

1. Autenticação no Python
2. Leitura de municípios
3. Loop temporal
4. Exportação automática

### Desafio extra 🚀

* Integrar com Pandas
* Gerar relatório automático
* Conectar com banco de dados

---

