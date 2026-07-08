# CLAUDE.md

Este arquivo fornece orientação ao Claude Code (claude.ai/code) ao trabalhar com código neste repositório.

## Visão Geral do Projeto

**Calculadora do Milhão** é uma aplicação web de simulação financeira. Projeta o crescimento patrimonial através de venda de opções + ETF, mês a mês, até atingir uma meta de patrimônio.

- Arquivo único: `index.html` (aplicação single-page HTML/CSS/JavaScript)
- Hospedada em GitHub Pages (ramo `main`)
- Sem dependências externas além de Chart.js (via CDN)

## Estrutura do Código

O arquivo `index.html` contém três seções principais:

### 1. Estilos CSS (linhas 16-383)
- Sistema de variáveis CSS para temas (claro/escuro) via `data-theme`
- Paleta de cores com variáveis: `--accent`, `--danger`, `--good`, etc.
- Layout responsivo com grid: coluna fixa (Parâmetros) + coluna flexível (Resultados)
- Responsivo em telas pequenas (max-width: 860px)

### 2. Markup HTML (linhas 385-526)
- **Header**: Título + botão de alternância de tema
- **Painel esquerdo**: Controles de entrada (sliders + inputs numéricos)
  - Patrimônio inicial, Meta, Taxa de extração, Rendimento, Teto de alocação, etc.
- **Painel direito**: Resultados da simulação
  - Card "Hero" com resultado (meta atingida/não atingida)
  - Gráfico de evolução do patrimônio (Chart.js)
  - Tabela de marcos (250k, 500k, 750k, 1M)
  - Tabela "Extrato mês a mês" com filtros e exportação CSV

### 3. Lógica JavaScript (linhas 528-1003)
- **Sincronização sliders ↔ inputs**: `syncPair()`
- **Simulação**: `simulate()` — itera 360 meses calculando patrimônio mensal
- **Renderização**:
  - `renderHeadline()` — resultado final (meta atingida em X anos)
  - `renderMarcos()` — tabela de marcos atingidos
  - `renderChart()` — gráfico de evolução com Chart.js
  - `renderExtrato()` — tabela mensal com filtros opcionais
- **Exportação**: `exportExtratoCSV()` — downloads em formato CSV

## Fluxo de Dados

1. Usuário ajusta parâmetros via sliders/inputs
2. Event listeners disparam `recalc()`
3. `recalc()` chama `simulate()` → retorna arrays de meses/patrimônio/prêmio/rendimento
4. Resultados são renderizados em 4 visualizações (headline, marcos, chart, extrato)
5. Tema pode ser alternado (lightMode/darkMode) — atualiza Chart.js em tempo real

## Comandos Comuns

Como é uma aplicação web estática, não há build, testes ou lint. Apenas:

- **Testar localmente**: Abrir `index.html` em um navegador
  - No VS Code: Live Server ou similar
  - Na linha de comando: `python -m http.server 8000` (depois acesso em http://localhost:8000)

- **Deploy**: Push para `main` branch — GitHub Pages atualiza automaticamente

## Áreas-Chave para Edição

- **Parâmetros da simulação**: Buscar `const MARCOS = [...]` (linha 652) e `const MAX_MESES = 360` (linha 653)
- **Cores/tema**: Modificar variáveis CSS `:root` (linhas 17-56)
- **Fórmula de cálculo**: Função `simulate()` (linhas 657-738)
- **Textos do usuário**: Buscar por strings em português (ex: "Meta não atingida")

## GitHub Pages

- Configurado para publicar do ramo `main`
- URL: https://brunotrolo.github.io/calculadoraMilhao/
- Qualquer push para `main` dispara redeploy automático
