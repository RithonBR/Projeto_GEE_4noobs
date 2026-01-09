# Módulo 1 – Introdução ao Google Earth Engine

## Visão Geral do Módulo

Neste módulo inicial, o aluno será introduzido ao **Google Earth Engine (GEE)**, compreendendo seu propósito, arquitetura em nuvem e principais aplicações no Sensoriamento Remoto. O foco é criar uma **base conceitual sólida**, preparando o aluno para os módulos práticos seguintes.

---

## Objetivos de Aprendizagem

Ao final deste módulo, o aluno será capaz de:

* Entender o que é o Google Earth Engine e por que ele é utilizado
* Compreender a diferença entre processamento local e em nuvem
* Navegar com segurança pela interface do Code Editor
* Executar seu primeiro script no GEE

---

## Aula 1.1 – O que é o Google Earth Engine

O **Google Earth Engine (GEE)** é uma plataforma de computação em nuvem desenvolvida pelo Google para **armazenamento, processamento e análise de grandes volumes de dados geoespaciais**, especialmente imagens de satélite e dados ambientais.

Diferentemente de softwares GIS tradicionais, onde os dados precisam ser baixados e processados localmente, no GEE **os dados já estão disponíveis na nuvem** e o processamento ocorre diretamente nos servidores do Google. Isso permite análises rápidas, escaláveis e reprodutíveis, mesmo quando trabalhamos com séries temporais longas ou áreas extensas.

Em termos simples, o GEE combina três pilares principais:

* Um **catálogo massivo de dados geoespaciais globais**
* **Capacidade computacional em nuvem**
* Uma **linguagem de programação** para análise espacial

---

### Histórico e motivação da plataforma

O Google Earth Engine foi criado no início da década de 2010 com o objetivo de **democratizar o acesso a dados ambientais globais** e facilitar estudos sobre mudanças ambientais em escala planetária.

Antes do GEE, análises envolvendo décadas de imagens Landsat ou grandes regiões exigiam infraestrutura computacional robusta, alto custo de armazenamento e longos tempos de processamento. Isso limitava o acesso principalmente a grandes instituições.

A proposta do GEE foi mudar esse cenário, oferecendo:

* Acesso gratuito para pesquisa, educação e uso não comercial
* Dados prontos para uso, sem necessidade de download
* Processamento distribuído em nuvem

Hoje, o GEE é amplamente utilizado por **universidades, centros de pesquisa, órgãos governamentais e empresas**, sendo uma das principais plataformas para análise ambiental em larga escala.

---

### Principais áreas de aplicação

O Google Earth Engine é uma ferramenta extremamente versátil. Entre suas principais aplicações, destacam-se:

#### 🌱 Agricultura

* Monitoramento de culturas agrícolas
* Análise de vigor vegetativo (NDVI, EVI)
* Estimativa de área plantada
* Acompanhamento de safras ao longo do tempo

#### 🌳 Meio ambiente

* Monitoramento de desmatamento
* Análise de áreas protegidas
* Estudos de degradação ambiental
* Avaliação de queimadas

#### 🌧️ Clima e hidrologia

* Análise de precipitação e temperatura
* Monitoramento de secas e enchentes
* Estudos hidrológicos em bacias
* Integração com dados climáticos globais

#### 🗺️ Monitoramento de uso e cobertura da terra

* Classificação de uso e cobertura do solo
* Detecção de mudanças temporais
* Avaliação da expansão urbana
* Estudos territoriais em diferentes escalas

---

### Exemplos reais de projetos desenvolvidos com GEE

Ao longo dos anos, o GEE foi utilizado em diversos projetos de alto impacto, como:

* Mapas globais de desmatamento
* Monitoramento quase em tempo real de queimadas
* Estudos de expansão agrícola em larga escala
* Análises temporais de vegetação usando séries Landsat e Sentinel
* Desenvolvimento de aplicações interativas (Apps) para apoio à tomada de decisão

Esses exemplos mostram que o Google Earth Engine não é apenas uma ferramenta acadêmica, mas também uma **plataforma amplamente aplicada no mercado e em políticas públicas**.

---

## Aula 1.2 – Por que usar o Google Earth Engine

Nesta aula, vamos entender **por que o Google Earth Engine se tornou uma das principais plataformas de análise geoespacial do mundo** e quais problemas ele resolve quando comparado às abordagens tradicionais de Sensoriamento Remoto e GIS.

---

### Limitações do processamento local de imagens de satélite

Tradicionalmente, a análise de imagens de satélite é feita em softwares GIS instalados localmente, como QGIS ou ArcGIS. Embora essas ferramentas sejam poderosas, elas apresentam limitações importantes quando trabalhamos com grandes volumes de dados:

* Necessidade de **download de grandes quantidades de imagens**
* Alto consumo de **armazenamento em disco**
* Dependência de **hardware potente** (processador, memória RAM)
* Processamento lento para séries temporais longas
* Dificuldade em reproduzir análises em diferentes computadores

Essas limitações tornam inviável, por exemplo, analisar **décadas de imagens Landsat para um país inteiro** em um computador comum.

---

### Vantagens do processamento em nuvem

O Google Earth Engine elimina grande parte dessas limitações ao operar totalmente em **ambiente de computação em nuvem**. Entre as principais vantagens, destacam-se:

* Os dados já estão **armazenados nos servidores do Google**
* Não há necessidade de download das imagens
* Processamento distribuído e escalável
* Execução de análises complexas em poucos segundos ou minutos
* Possibilidade de trabalhar com áreas pequenas ou globais usando o mesmo código

Na prática, isso significa que o aluno pode focar **na análise e na lógica do problema**, e não na infraestrutura computacional.

---

### Acesso a grandes bases de dados globais

Um dos maiores diferenciais do GEE é seu **catálogo de dados geoespaciais**, que inclui:

* Imagens de satélite (Landsat, Sentinel, MODIS, entre outras)
* Dados climáticos e meteorológicos
* Modelos digitais de elevação
* Dados de uso e cobertura da terra
* Produtos prontos para análise ambiental

Esses dados estão **padronizados, organizados e constantemente atualizados**, permitindo análises consistentes e confiáveis.

---

### Comparação: GEE vs GIS tradicional

É importante destacar que o Google Earth Engine **não substitui completamente** softwares GIS tradicionais, mas os complementa.

| GIS Tradicional                       | Google Earth Engine                         |
| ------------------------------------- | ------------------------------------------- |
| Processamento local                   | Processamento em nuvem                      |
| Limitações de hardware                | Escalável                                   |
| Ideal para análises detalhadas locais | Ideal para grandes áreas e séries temporais |
| Forte em edição cartográfica          | Forte em automação e Big Data               |

Na prática, muitos fluxos de trabalho utilizam o GEE para **processar e analisar os dados**, e o GIS tradicional para **finalização cartográfica e análise local**.

---

### Aplicações práticas no mundo real

O uso do Google Earth Engine é cada vez mais comum em:

* Pesquisa científica
* Monitoramento ambiental contínuo
* Agricultura de precisão
* Planejamento territorial
* Desenvolvimento de aplicações interativas

Com o GEE, é possível criar **scripts reutilizáveis**, automatizar rotinas complexas e gerar resultados reproduzíveis, características fundamentais tanto no meio acadêmico quanto no mercado profissional.

---

## Aula 1.3 – Arquitetura e lógica de funcionamento do GEE

Nesta aula, o objetivo é compreender **como o Google Earth Engine funciona internamente** e por que sua lógica é diferente da programação tradicional. Entender esses conceitos é essencial para evitar erros comuns e escrever scripts eficientes.

---

### Conceito de Big Data geoespacial

O Google Earth Engine foi projetado para lidar com **Big Data geoespacial**, ou seja, grandes volumes de dados espaciais e temporais, como:

* Décadas de imagens de satélite
* Séries temporais contínuas
* Dados globais com alta resolução espacial

Para tornar isso viável, o GEE adota uma arquitetura em que **os dados e o processamento estão na nuvem**, e o usuário apenas define *o que deve ser feito* por meio de código.

---

### Server-side × Client-side

Um dos conceitos mais importantes do GEE é a separação entre **operações server-side** e **operações client-side**.

#### 🖥️ Client-side (lado do usuário)

* Executa no navegador do usuário
* Usa JavaScript puro
* Controla lógica de interface, laços simples e impressão de resultados
* Exemplo: variáveis JavaScript, `for`, `if`, `print()`

#### ☁️ Server-side (lado do servidor)

* Executa nos servidores do Google
* Manipula grandes volumes de dados
* Usa objetos do Earth Engine (`ee.Image`, `ee.Feature`, `ee.ImageCollection`)
* Escala automaticamente para grandes áreas e períodos

No GEE, **quase todo o processamento pesado ocorre no server-side**. O código escrito pelo usuário é, na prática, uma **descrição da tarefa**, não a execução imediata dela.

---

### Objetos do Earth Engine

Os principais objetos do GEE são:

* `ee.Image` – uma imagem raster
* `ee.ImageCollection` – uma coleção de imagens
* `ee.Feature` – um elemento vetorial
* `ee.FeatureCollection` – uma coleção de vetores

Esses objetos **não contêm os dados localmente**. Eles são referências a dados armazenados na nuvem.

Por isso, comandos como `print()` ou tentativas de acessar valores diretamente podem não funcionar como esperado para iniciantes.

---

### Lazy evaluation (execução sob demanda)

O Google Earth Engine utiliza o conceito de **lazy evaluation**, ou execução sob demanda.

Isso significa que:

* O código **não é executado linha por linha** como em linguagens tradicionais
* As operações são apenas **encadeadas**
* O processamento real só ocorre quando uma ação é solicitada

Exemplos de ações que disparam a execução:

* Visualizar uma camada no mapa (`Map.addLayer`)
* Exportar dados (`Export.image.toDrive`, `Export.table.toDrive`)
* Solicitar informações explícitas (`getInfo()`)

Esse modelo permite ao GEE **otimizar o processamento**, evitando cálculos desnecessários.

---

### Exemplo conceitual

Quando o usuário escreve um script no GEE, ele está basicamente dizendo:

> “Aqui estão os dados que quero usar e as operações que desejo aplicar. Execute isso apenas quando necessário.”

Isso explica por que alguns scripts parecem não rodar imediatamente ou por que erros aparecem apenas no momento da visualização ou exportação.

---

### Principais erros de iniciantes

Alguns erros comuns que surgem quando esses conceitos não são compreendidos:

* Tentar usar valores de objetos `ee` como se fossem variáveis JavaScript
* Usar laços `for` para percorrer `ImageCollection`
* Esperar resultados imediatos sem uma ação final
* Confundir erros de sintaxe com erros de execução server-side

Compreender a lógica server-side × client-side e o conceito de lazy evaluation é um **marco fundamental** no aprendizado do Google Earth Engine.

---

### Conclusão da aula

Ao final desta aula, o aluno deve entender que:

* O GEE é uma plataforma baseada em computação em nuvem
* O código descreve operações, não a execução imediata
* O processamento ocorre majoritariamente no server-side
* A execução acontece apenas quando solicitada

Esses conceitos serão utilizados em **todos os módulos seguintes do curso**.

---

## Aula 1.4 – Criando sua conta no Google Earth Engine

Nesta aula, o foco é **operacional**: orientar passo a passo como criar e acessar uma conta no Google Earth Engine. Esse é um pré-requisito essencial para a realização das aulas práticas do curso.

---

### Requisitos para criar uma conta

Para utilizar o Google Earth Engine, é necessário:

* Possuir uma **conta Google ativa** (Gmail)
* Ter acesso à internet
* Concordar com os termos de uso da plataforma

Não é necessário possuir experiência prévia em programação ou GIS para criar a conta.

---

### Solicitação de acesso ao Google Earth Engine

O Google Earth Engine não é liberado automaticamente para todas as contas Google. É necessário realizar uma **solicitação de acesso**.

O processo consiste em:

1. Acessar a página oficial do Google Earth Engine
2. Clicar em **“Sign up”** ou **“Request access”**
3. Fazer login com sua conta Google
4. Preencher um formulário simples informando:

   * Nome
   * Instituição ou ocupação
   * Finalidade de uso (educacional, pesquisa, profissional)

Em cursos e atividades educacionais, recomenda-se indicar o uso como **educação ou pesquisa**.

---

### Termos de uso e política da plataforma

Durante a solicitação, o usuário deverá aceitar os **termos de uso do Google Earth Engine**, que incluem:

* Uso gratuito para fins acadêmicos, educacionais e de pesquisa
* Restrições para uso comercial direto
* Responsabilidade sobre os dados e resultados gerados

É importante destacar que o GEE permite uso profissional, desde que respeitadas as políticas estabelecidas pelo Google.

---

### Tempo de aprovação

Após o envio da solicitação:

* A aprovação geralmente ocorre em **poucas horas ou alguns dias**
* O usuário receberá um e-mail de confirmação
* Em alguns casos, o acesso pode ser liberado imediatamente

Caso a aprovação demore mais do que o esperado, recomenda-se verificar a caixa de spam ou reenviar a solicitação.

---

### Primeiro acesso ao Code Editor

Com a conta aprovada, o próximo passo é acessar o **Google Earth Engine Code Editor**, que é o ambiente principal de desenvolvimento da plataforma.

No primeiro acesso, o usuário poderá:

* Visualizar a interface do editor
* Acessar exemplos prontos
* Executar scripts básicos

Esse ambiente será explorado em detalhes na próxima aula.

---

### Atividade prática da aula

1. Solicitar acesso ao Google Earth Engine
2. Confirmar a aprovação da conta
3. Acessar o Code Editor pela primeira vez
4. Registrar qualquer dúvida ou dificuldade encontrada no processo

---

### Conclusão da aula

Ao final desta aula, o aluno terá:

* Uma conta ativa no Google Earth Engine
* Acesso ao Code Editor
* Condições técnicas para iniciar as aulas práticas do curso

Este passo marca oficialmente o **início da jornada prática no Google Earth Engine**.

---

## Aula 1.5 – Interface do Code Editor

Nesta aula, vamos explorar de forma **visual e prática** a interface do **Google Earth Engine Code Editor**, entendendo a função de cada painel e como eles se integram no fluxo de trabalho. Dominar essa interface é fundamental para programar com eficiência no GEE.

---

### Visão geral do Code Editor

O Code Editor é o ambiente online onde os scripts do Google Earth Engine são escritos, executados e visualizados. Ele reúne, em uma única interface:

* Escrita de código
* Visualização de mapas
* Inspeção de dados
* Gerenciamento de assets
* Execução de exportações

A interface é dividida em **painéis principais**, que veremos a seguir.

---

### 📝 Painel de Scripts (Editor de Código)

Localizado normalmente à esquerda, o painel de scripts é onde o código JavaScript é escrito.

Principais funcionalidades:

* Escrita e edição de scripts
* Organização por abas
* Salvamento automático dos códigos
* Comentários e organização do código

Boas práticas desde o início:

* Usar comentários para explicar o código
* Manter scripts organizados e nomeados corretamente

---

### 🗺️ Painel de Mapas

O painel central é onde os resultados espaciais são visualizados.

Funcionalidades principais:

* Visualização de camadas raster e vetoriais
* Controle de zoom e navegação
* Ativação e desativação de camadas
* Mudança de mapas base

Tudo que é adicionado com `Map.addLayer()` aparece neste painel.

---

### 💬 Console

O console exibe mensagens, resultados e erros gerados pelo script.

Principais usos:

* Visualizar objetos com `print()`
* Ler mensagens de erro
* Acompanhar execuções do código

O console é uma ferramenta essencial para **depuração (debug)** dos scripts.

---

### 🔍 Inspector

O Inspector permite consultar valores diretamente no mapa.

Com ele, é possível:

* Clicar em um ponto do mapa
* Ver valores de pixels
* Inspecionar atributos de feições

Essa ferramenta é muito útil para entender os dados e validar resultados.

---

### 📁 Aba Assets

A aba Assets é onde ficam armazenados:

* Dados vetoriais importados
* Imagens próprias
* Resultados salvos

Nela, o usuário pode:

* Importar arquivos (Shapefile, GeoJSON, etc.)
* Organizar dados em pastas
* Compartilhar assets com outros usuários

---

### ⏱️ Aba Tasks

A aba Tasks mostra todas as tarefas de exportação criadas pelo usuário.

Principais funções:

* Iniciar exportações manualmente
* Acompanhar o status das tarefas
* Identificar falhas de exportação

No GEE, **nenhuma exportação é iniciada automaticamente** — o usuário sempre precisa confirmar a tarefa nesta aba.

---

### Fluxo típico de trabalho no Code Editor

Um fluxo comum de uso do Code Editor envolve:

1. Escrever o script no painel de código
2. Executar o script
3. Visualizar resultados no mapa
4. Inspecionar dados com o Inspector
5. Verificar mensagens no Console
6. Exportar resultados via Tasks

Entender esse fluxo ajuda o aluno a trabalhar de forma organizada e eficiente.

---

### Atividade prática da aula

1. Abrir o Code Editor
2. Identificar cada painel apresentado
3. Executar um script de exemplo
4. Adicionar uma camada ao mapa
5. Visualizar mensagens no Console

---

### Conclusão da aula

Ao final desta aula, o aluno será capaz de:

* Navegar com segurança pelo Code Editor
* Entender a função de cada painel
* Interpretar mensagens e erros básicos
* Preparar-se para escrever seus primeiros scripts completos

Na próxima aula, daremos início à prática com o **primeiro script no Google Earth Engine**.

---

## Aula 1.6 – Primeiro script no Google Earth Engine

Nesta aula, o foco é **100% prático**. O objetivo é executar o primeiro script no Google Earth Engine, entendendo a estrutura básica de um código, a visualização no mapa e a interação com o ambiente.

---

### Objetivo da aula

Ao final desta aula, o aluno será capaz de:

* Escrever e executar um script simples no GEE
* Centralizar o mapa em uma área de interesse
* Adicionar uma camada raster ao mapa
* Alterar parâmetros de visualização

---

### Estrutura básica de um script no GEE

Um script simples no Google Earth Engine geralmente possui:

1. Definição da área ou ponto de interesse
2. Carregamento de um dado (imagem ou coleção)
3. Configuração de visualização
4. Exibição do resultado no mapa

Mesmo scripts simples seguem essa lógica, que será reutilizada ao longo de todo o curso.

---

### Primeiro comando: centralizando o mapa

Começaremos centralizando o mapa em uma região do Brasil. Use o comando abaixo:

```javascript
Map.setCenter(-45.9, -12.1, 8);
```

* Os dois primeiros valores representam **longitude e latitude**
* O último valor define o **nível de zoom**

💡 *Dica:* altere os valores para sua região e observe o comportamento do mapa.

---

### Carregando um dado: Modelo Digital de Elevação (SRTM)

Agora vamos carregar uma imagem de elevação disponível no catálogo do GEE:

```javascript
var srtm = ee.Image('USGS/SRTMGL1_003');
```

Aqui estamos criando uma **referência** a uma imagem armazenada na nuvem. Nenhum dado é baixado para o seu computador.

---

### Visualizando a imagem no mapa

Para visualizar a imagem, usamos o comando `Map.addLayer()`:

```javascript
Map.addLayer(srtm, {min: 0, max: 3000}, 'SRTM');
```

* `srtm`: imagem que será exibida
* `{min, max}`: parâmetros de visualização
* `'SRTM'`: nome da camada no mapa

Ao executar o script, a camada aparecerá no painel de mapas.

---

### Script completo da aula

```javascript
// Centraliza o mapa
Map.setCenter(-45.9, -12.1, 8);

// Carrega o Modelo Digital de Elevação (SRTM)
var srtm = ee.Image('USGS/SRTMGL1_003');

// Adiciona a camada ao mapa
Map.addLayer(srtm, {min: 0, max: 3000}, 'SRTM');
```

Execute o código clicando no botão **Run**.

---

### Interagindo com o mapa

Após executar o script:

* Ative e desative a camada no painel de mapas
* Use o zoom para explorar diferentes regiões
* Clique no **Inspector** e observe os valores de elevação

Essas ações ajudam a entender como os dados estão sendo representados.

---

### Atividade prática da aula

1. Execute o script apresentado
2. Altere o centro do mapa para sua cidade ou região
3. Ajuste os valores de `min` e `max`
4. Renomeie a camada no `Map.addLayer()`

---

### Erros comuns e como evitar

* **Mapa não aparece:** verifique se clicou em *Run*
* **Imagem muito escura ou clara:** ajuste `min` e `max`
* **Erro de digitação:** revise nomes e parênteses

Erros fazem parte do processo e ajudam no aprendizado.

---

### Conclusão da aula

Este foi o **primeiro contato prático** com o Google Earth Engine.

A partir deste ponto, o aluno já sabe:

* Executar scripts no Code Editor
* Carregar dados do catálogo do GEE
* Visualizar informações espaciais no mapa

Nos próximos módulos, avançaremos para o uso de **imagens de satélite, filtros, índices espectrais e análises temporais**.

---
