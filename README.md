# Pátio Satélite — Planejador de Distribuição de Viaturas

Ferramenta web de página única (um único arquivo `patio_satelite.html`) para **planejar a disposição de viaturas, formaturas e croquis sobre imagem de satélite real**, em escala verdadeira do terreno. Foi pensada para o trabalho de logística e planejamento de estacionamento/formatura de meios, permitindo posicionar cada viatura no tamanho real, medir distâncias, anotar o croqui e gerar uma imagem de relatório com legenda.

> **Resumo em uma linha:** abra o arquivo no navegador, monte o plano sobre o satélite e exporte uma imagem pronta para o relatório — tudo offline e sem instalar nada.

![Visão geral do sistema](docs/img/01-visao-geral.png)
> _Figura 1 — Tela inicial: mapa de satélite à esquerda e painel de controle à direita._
<!-- PRINT SUGERIDO: janela cheia do app, com algumas viaturas no mapa e o painel lateral aberto na aba "Frota". -->

---

## Sumário

1. [Principais vantagens](#principais-vantagens)
2. [Requisitos e considerações importantes](#requisitos-e-considerações-importantes)
3. [Download e primeira execução](#1-download-e-primeira-execução)
4. [Conhecendo a interface](#2-conhecendo-a-interface)
5. [Passo a passo de utilização](#3-passo-a-passo-de-utilização)
   - [3.1 Posicionar o mapa e escolher a camada](#31-posicionar-o-mapa-e-escolher-a-camada)
   - [3.2 Cadastrar a frota](#32-cadastrar-a-frota)
   - [3.3 Inserir viaturas no mapa](#33-inserir-viaturas-no-mapa)
   - [3.4 Selecionar e editar elementos](#34-selecionar-e-editar-elementos)
   - [3.5 Ocultar e reexibir elementos](#35-ocultar-e-reexibir-elementos)
   - [3.6 Zona de formatura (preenchimento automático)](#36-zona-de-formatura-preenchimento-automático)
   - [3.7 Desenhar: medir, linhas e textos](#37-desenhar-medir-linhas-e-textos)
   - [3.8 Grade de orientação](#38-grade-de-orientação)
   - [3.9 Legenda](#39-legenda)
   - [3.10 Exportar a imagem do relatório](#310-exportar-a-imagem-do-relatório)
   - [3.11 Salvar, exportar e importar o projeto](#311-salvar-exportar-e-importar-o-projeto)
6. [Atalhos de teclado](#4-atalhos-de-teclado)
7. [Boas práticas](#5-boas-práticas)
8. [Solução de problemas (FAQ)](#6-solução-de-problemas-faq)
9. [Privacidade, dados e licenciamento](#7-privacidade-dados-e-licenciamento)
10. [Tecnologias](#8-tecnologias)

---

## Principais vantagens

- **Escala real garantida.** Cada viatura é um polígono georreferenciado. Independentemente do zoom, da rotação do mapa ou da camada escolhida, ela mantém o tamanho verdadeiro no terreno (ex.: uma VBTP de 6,9 m × 2,7 m ocupa exatamente essa área).
- **Funciona offline, sem instalação.** É um único arquivo HTML com todas as bibliotecas embutidas. Basta um duplo-clique. Só é necessário acesso à internet para carregar as imagens de satélite.
- **Várias fontes de satélite.** Alterna entre Esri, Google Satélite e Google Híbrido (com nomes de vias e rótulos), escolhendo a que tiver a melhor imagem na sua região.
- **Edição direta e rápida.** Clique em qualquer elemento (viatura, linha ou texto) para editá-lo em um painel flutuante sobre o mapa; mova, gire, duplique ou remova em grupo.
- **Seleção múltipla.** Selecione várias viaturas por área (arrasto) ou por `Ctrl+clique` e trabalhe todas de uma vez.
- **Ferramentas de croqui.** Medição de distâncias, linhas livres, textos com quebra de linha e uma grade de orientação em escala real para alinhar meios e formaturas.
- **Relatório pronto para uso.** Exporta uma imagem com cabeçalho (data, centro, zoom, rumo, escala), o recorte do mapa e a legenda automática com contagem por tipo e área ocupada.
- **Salvamento automático + backup.** O trabalho é salvo no próprio navegador e pode ser exportado/importado como arquivo `.json` para backup ou para passar a outra máquina.

---

## Requisitos e considerações importantes

- **Navegador recomendado: Google Chrome** (ou Edge/Chromium atualizado). A exportação da imagem usa a **captura de tela do navegador**, recurso mais bem suportado nesses navegadores.
- **Conexão com a internet** apenas para exibir as imagens de satélite. Todo o restante (edição, cálculos, salvamento) funciona localmente.
- **A exportação é uma "foto" da tela.** Por isso, a nitidez da imagem final acompanha a resolução do seu monitor. Para máxima qualidade, enquadre bem a área e use uma tela grande antes de exportar.
- **Imagens de satélite são ilustrativas.** As camadas Esri/Google servem para planejamento visual. Para uso oficial que exija base cartográfica licenciada, considere uma fonte apropriada (API licenciada do Google, Mapbox/MapTiler ou ortofotos próprias).
- **Os dados ficam no seu navegador.** Nada é enviado a servidores. Limpar os dados do navegador ou usar aba anônima pode apagar o trabalho não exportado — use o **Exportar JSON** para backup.

---

## 1. Download e primeira execução

1. **Baixe** o arquivo `patio_satelite.html` para uma pasta de sua preferência (ex.: `Documentos\Patio`).
2. **Abra** o arquivo com um duplo-clique. Ele abrirá no navegador padrão. Se preferir, clique com o botão direito → *Abrir com* → *Google Chrome*.
3. Na primeira abertura, o app já vem com **exemplos de viaturas** cadastradas (VBTP Guarani, Marruá, Cam 5 ton) para você começar a testar imediatamente.
4. **Posicione o mapa** na sua área de interesse (veja o passo 3.1).

![Abertura do arquivo](docs/img/02-abertura.png)
> _Figura 2 — O sistema é um único arquivo; basta abrir no navegador._
<!-- PRINT SUGERIDO: o arquivo patio_satelite.html no explorador de arquivos, ou a aba do navegador recém-aberta. -->

> **Dica:** crie um atalho do arquivo na área de trabalho para acesso rápido.

---

## 2. Conhecendo a interface

A tela é dividida em duas áreas: o **mapa** (à esquerda) e o **painel de controle** (à direita), organizado em abas.

| Aba | Para que serve |
|-----|----------------|
| **Mapa** | Rotação/rumo do mapa, notas de uso e botão de exportar imagem. |
| **Frota** | Cadastrar tipos de viatura (nome, dimensões, cor) e inseri-los no mapa. |
| **Formatura** | Criar e dimensionar a zona de formatura e preenchê-la automaticamente. |
| **Desenho** | Medir distâncias, desenhar linhas, inserir textos, selecionar por área e configurar a grade. |
| **Legenda** | Ver os tipos presentes, ligar/desligar por tipo e recuperar elementos ocultos. |
| **Dados** | Salvar/limpar, exportar e importar o projeto em `.json`. |

![Painel de controle](docs/img/03-abas.png)
> _Figura 3 — Barra de abas do painel de controle._
<!-- PRINT SUGERIDO: recorte do topo do painel lateral mostrando as abas. -->

---

## 3. Passo a passo de utilização

### 3.1 Posicionar o mapa e escolher a camada

1. Navegue no mapa como em qualquer mapa web: **arraste para mover** e use a **roda do mouse para o zoom**.
2. No **seletor de camadas** (canto superior direito do mapa), escolha a base de imagem:
   - **Satélite (Esri)**
   - **Satélite (Google)** — costuma ser a mais nítida.
   - **Híbrido (Google)** — satélite com nomes de vias e rótulos.
   - **OpenStreetMap** — mapa de ruas.
3. Para **girar o mapa** conforme a orientação do terreno, use a aba **Mapa** → controle de **Rumo** (arraste o controle ou digite o valor; o botão **Norte** volta a 0°). A escala real, no canto inferior, é sempre respeitada.

![Seletor de camadas](docs/img/04-camadas.png)
> _Figura 4 — Alternando entre as camadas de satélite._
<!-- PRINT SUGERIDO: o seletor de camadas aberto no canto superior direito do mapa. -->

---

### 3.2 Cadastrar a frota

1. Vá para a aba **Frota**.
2. Preencha **Nome**, **Comprimento (m)** e **Largura (m)** da viatura.
3. O campo **Cor (sugerida)** já vem preenchido com uma cor sorteada **entre as que ainda não foram usadas** — isso agiliza o cadastro e evita repetição. Você pode trocá-la à vontade clicando no seletor de cor.
4. Clique em **Adicionar à frota**. O tipo aparece na lista e o campo de cor já sugere a próxima cor livre.
5. Cada item da lista tem os botões: **＋** (inserir no centro do mapa), **✎** (editar dimensões/nome) e **🗑** (excluir o tipo).

![Cadastro de frota](docs/img/05-frota.png)
> _Figura 5 — Cadastro de tipos de viatura com cor sugerida automaticamente._
<!-- PRINT SUGERIDO: aba "Frota" com o formulário preenchido e a lista de tipos abaixo. -->

---

### 3.3 Inserir viaturas no mapa

Há duas formas:

- **Modo "clicar para inserir":** clique no card do tipo na lista (ele fica ativo) e depois **clique no mapa** em cada ponto onde quer uma viatura daquele tipo. Pressione `Esc` para sair do modo.
- **Inserir no centro:** clique no botão **＋** do tipo para colocar uma unidade no centro do mapa atual.

Cada viatura inserida já aparece no tamanho real do terreno e pode ser reposicionada em seguida.

![Inserindo viaturas](docs/img/06-inserir.png)
> _Figura 6 — Viaturas posicionadas em escala real sobre o satélite._
<!-- PRINT SUGERIDO: mapa com várias viaturas do mesmo tipo posicionadas em fila. -->

---

### 3.4 Selecionar e editar elementos

**Selecionar:**
- **Clique** em uma viatura, linha ou texto para selecioná-lo.
- **`Ctrl+clique`** adiciona/remove outras viaturas da seleção (seleção múltipla).
- **`Shift`+arraste** sobre o mapa desenha um retângulo e seleciona todas as viaturas dentro dele. (Alternativa: botão **Selecionar em área**, na aba Desenho — ao ativá-lo, arraste com o mouse.)

**Editar (painel flutuante que aparece sobre o mapa):**
- **Viatura (uma):** editar Nome, Comprimento, Largura, Cor e Ângulo; girar (⟲ 15° / 90° / ⟳ 15°); Duplicar; Ocultar/Mostrar; Remover.
- **Viaturas (grupo):** mover todas juntas (arraste qualquer uma), girar, duplicar, ocultar/mostrar e remover em bloco.
- **Texto:** editar o conteúdo (com quebra de linha por `Enter`) e a cor; arraste o texto no mapa para reposicionar.
- **Linha / medição:** editar a cor; arraste a linha para mover ou arraste os pontos (alças) para ajustar o traçado.

Para mover uma viatura, **arraste-a**. Para girar uma única viatura, use a **alça laranja** que aparece ao selecioná-la, ou o campo Ângulo.

![Painel de edição](docs/img/07-edicao.png)
> _Figura 7 — Painel de edição flutuante ao selecionar uma viatura._
<!-- PRINT SUGERIDO: uma viatura selecionada com o painel "Editar" aberto sobre o mapa. -->

![Seleção múltipla](docs/img/08-selecao-multipla.png)
> _Figura 8 — Seleção de várias viaturas por área (Shift + arraste)._
<!-- PRINT SUGERIDO: retângulo de seleção sobre um grupo de viaturas, com o painel de grupo aberto. -->

---

### 3.5 Ocultar e reexibir elementos

- No painel de edição de qualquer elemento, use **🚫 Ocultar / 👁 Mostrar** para tirar aquele item específico da visualização e do relatório.
- Um elemento oculto some do mapa. Para **reexibi-lo**, vá à aba **Legenda** → seção **Ocultos**, que lista cada item oculto (viatura, linha ou texto) com um botão **Mostrar** (e um **Mostrar todos**).
- Para ocultar **um tipo inteiro** de uma vez, use o "olho" 👁 ao lado do tipo, também na aba **Legenda**.

![Elementos ocultos](docs/img/09-ocultos.png)
> _Figura 9 — Lista de recuperação de elementos ocultos na aba Legenda._
<!-- PRINT SUGERIDO: aba "Legenda" mostrando a seção "Ocultos" com itens e botões "Mostrar". -->

---

### 3.6 Zona de formatura (preenchimento automático)

1. Na aba **Formatura**, crie a zona e ajuste **Largura**, **Altura** e **Rumo** (ângulo). No mapa, a zona pode ser movida (arraste o corpo), girada (alça de rotação) e redimensionada (alças de canto).
2. Escolha o tipo de viatura para preencher.
3. Use **Estimar** para ver quantas cabem, e **Preencher** para dispor automaticamente as viaturas alinhadas ao rumo da zona.

![Zona de formatura](docs/img/10-formatura.png)
> _Figura 10 — Zona de formatura preenchida automaticamente._
<!-- PRINT SUGERIDO: uma zona retangular sobre o mapa preenchida com viaturas em grade. -->

---

### 3.7 Desenhar: medir, linhas e textos

Na aba **Desenho**:

- **Medir distância:** clique para adicionar pontos; **duplo-clique** encerra. A distância total aparece na linha.
- **Linha:** desenho livre com vários pontos; **duplo-clique** encerra.
- **Texto:** clique no mapa e digite. Para **quebrar linha**, selecione o texto e use `Enter` no campo de edição do painel (o texto respeita as quebras que você fizer).
- **Desfazer último** / **Limpar todos** para gerenciar os desenhos.
- Clique sobre qualquer desenho para **editá-lo** (cor, texto, pontos) ou removê-lo.

![Ferramentas de desenho](docs/img/11-desenho.png)
> _Figura 11 — Medição de distância e texto de anotação no croqui._
<!-- PRINT SUGERIDO: mapa com uma medição (com rótulo de distância) e um texto multilinha. -->

---

### 3.8 Grade de orientação

Ainda na aba **Desenho**, seção **Grade de orientação**:

1. Marque **Mostrar grade**.
2. Defina o **Espaçamento (m)** e o **Rumo (°)** para alinhar a quadrícula ao terreno ou à formatura.
3. Use **Centralizar na vista atual** para posicionar a grade onde você está olhando.

A grade é quadriculada em **escala real**, serve de guia para alinhar viaturas e formaturas, acompanha o rumo informado e também aparece no relatório exportado.

![Grade de orientação](docs/img/12-grade.png)
> _Figura 12 — Grade em escala real usada para alinhamento._
<!-- PRINT SUGERIDO: mapa com a grade branca ativada sobre as viaturas. -->

---

### 3.9 Legenda

A aba **Legenda** mostra os tipos presentes no mapa (cor, nome, dimensões e contagem), permite **ligar/desligar a exibição por tipo** e concentra a **recuperação de elementos ocultos** (ver 3.5). A legenda também é gerada automaticamente na imagem exportada.

---

### 3.10 Exportar a imagem do relatório

A exportação faz uma **captura de tela** da área do mapa (assim ela funciona inclusive com as camadas do Google, que não podem ser copiadas diretamente) e monta um relatório com **cabeçalho + imagem + legenda**.

1. Enquadre bem a área no mapa (zoom e rumo desejados). Para a melhor nitidez, use a camada **Satélite (Google)** ou **Híbrido (Google)**.
2. Clique em **Exportar imagem** (aba **Mapa** ou no topo).
3. O navegador abrirá a janela de compartilhamento de tela. **Escolha "Esta guia"** e confirme.
4. O sistema oculta automaticamente os controles, tira o print, restaura tudo e baixa o arquivo **`plano_distribuicao_viaturas.png`**.

O cabeçalho traz **data, centro, zoom, rumo do mapa e escala aproximada**; uma bússola indica o norte real; e a legenda lista os tipos, a contagem e a área ocupada. Elementos ocultos individualmente **não** entram no relatório.

![Janela de compartilhamento](docs/img/13-exportar-guia.png)
> _Figura 13 — Ao exportar, selecione "Esta guia" para o recorte ficar correto._
<!-- PRINT SUGERIDO: a janela do Chrome pedindo para escolher o que compartilhar, com "Esta guia" destacada. -->

![Relatório exportado](docs/img/14-relatorio.png)
> _Figura 14 — Exemplo de imagem final: cabeçalho, mapa e legenda._
<!-- PRINT SUGERIDO: o arquivo PNG exportado aberto, mostrando cabeçalho + mapa + legenda. -->

> **Observações da exportação**
> - Se aparecer erro ou nada for baixado, confira se você concedeu a permissão e selecionou **"Esta guia"**.
> - Como é uma captura de tela, a resolução final depende do seu monitor. Telas maiores geram imagens mais nítidas.

---

### 3.11 Salvar, exportar e importar o projeto

- **Salvamento automático:** o trabalho é gravado no próprio navegador (armazenamento local). Ao reabrir o arquivo na mesma máquina/navegador, ele volta como estava.
- **Exportar JSON:** na aba **Dados**, gera um arquivo `.json` com toda a frota, viaturas, zona, desenhos, grade e visibilidade. Use para **backup** ou para **levar o plano a outra máquina**.
- **Importar JSON:** carrega um projeto salvo, substituindo o conteúdo atual.

![Exportar e importar](docs/img/15-dados.png)
> _Figura 15 — Backup e transferência do projeto em `.json`._
<!-- PRINT SUGERIDO: aba "Dados" com os botões de exportar/importar JSON. -->

> **Recomendação:** exporte um `.json` ao final de cada sessão importante. Limpar os dados do navegador apaga o salvamento automático, mas não o `.json`.

---

## 4. Atalhos de teclado

| Atalho | Ação |
|--------|------|
| **Clique** | Selecionar elemento |
| **Ctrl + clique** | Adicionar/remover da seleção |
| **Shift + arraste** | Selecionar viaturas por área |
| **Arraste** | Mover elemento (ou o grupo selecionado) |
| **Q / E** | Girar a(s) viatura(s) selecionada(s) 15° |
| **Setas** | Ajustar a posição em passos finos |
| **Shift + setas** | Ajustar a posição em passos maiores |
| **Delete / Backspace** | Remover o(s) elemento(s) selecionado(s) |
| **Esc** | Sair do modo atual / cancelar / limpar seleção |
| **Duplo-clique** (medir/linha) | Encerrar o desenho |

---

## 5. Boas práticas

- **Padronize as cores** por tipo de meio; a sugestão automática de cor já ajuda a não repetir.
- **Use a grade** para alinhar filas e formaturas com precisão.
- **Gire o mapa** para o rumo da via/pátio antes de posicionar — fica mais intuitivo.
- **Nomeie os textos** de forma curta e objetiva; use quebra de linha para rótulos com duas linhas.
- **Exporte um `.json`** como backup antes de grandes mudanças.
- **Para o relatório final**, enquadre a área, ative a grade se necessário e use uma camada Google para melhor nitidez.

---

## 6. Solução de problemas (FAQ)

**A imagem de satélite não aparece / aparece "não disponível".**
Verifique a conexão com a internet e experimente outra camada (Google costuma ter melhor cobertura em alto zoom).

**Ao exportar, a imagem sai cortada ou desalinhada.**
Selecione **"Esta guia"** na janela de compartilhamento (e não a tela inteira ou outra janela). Assim o recorte da área do mapa fica exato.

**Cliquei em exportar e nada aconteceu.**
A exportação exige a permissão de captura de tela. Se você cancelou a janela, o download não ocorre. Tente de novo e conceda a permissão.

**Ocultei um texto e ele sumiu.**
Vá à aba **Legenda** → seção **Ocultos** e clique em **Mostrar** ao lado do item.

**Perdi meu trabalho.**
Se estava na mesma máquina/navegador e não limpou os dados, ele deve recarregar sozinho. Para segurança, sempre **Exporte JSON**.

**A viatura parece do tamanho errado.**
As dimensões vêm do cadastro do tipo (aba Frota). Edite o tipo (✎) ou a viatura individual (painel de edição) para corrigir comprimento/largura.

---

## 7. Privacidade, dados e licenciamento

- **Privacidade:** o aplicativo roda inteiramente no seu navegador. Nenhum dado do seu plano é enviado a servidores externos; apenas as imagens de satélite são requisitadas dos provedores de mapa.
- **Armazenamento:** o projeto fica salvo no armazenamento local do navegador e nos arquivos `.json` que você exportar.
- **Licenciamento das imagens:** as camadas Esri/Google são exibidas para fins de planejamento visual. Para produtos oficiais que exijam base licenciada, utilize uma fonte apropriada (API licenciada, Mapbox/MapTiler ou ortofotos próprias).

---

## 8. Tecnologias

- **Leaflet** (mapa interativo) e **leaflet-rotate** (rotação/rumo), embutidos no arquivo.
- Camadas de satélite: **Esri World Imagery**, **Google Satélite/Híbrido** e **OpenStreetMap**.
- Exportação por **captura de tela** nativa do navegador (Screen Capture API).
- **HTML/CSS/JavaScript** puro, em arquivo único, sem dependências externas em tempo de execução (exceto os tiles de satélite).

---

### Como incluir as imagens deste manual

1. Crie uma pasta `docs/img` ao lado deste `README.md`.
2. Salve os prints com os nomes indicados nos comentários de cada figura (ex.: `01-visao-geral.png`, `04-camadas.png`, ...).
3. Os comentários `<!-- PRINT SUGERIDO: ... -->` descrevem o que capturar em cada ponto. Ao ser aberto num visualizador de Markdown (GitHub, Obsidian, VS Code), as imagens aparecerão automaticamente nos lugares corretos.
