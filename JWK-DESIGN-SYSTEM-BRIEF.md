# Briefing: Design System da JWK Digital Branding

Use este documento como fonte única. Crie o design system e todos os componentes descritos, seguindo a identidade visual da JWK. Onde o documento diz "derivado", o valor não existe no site da JWK e foi proposto para completar o sistema; você pode ajustá-lo, mantendo a coerência com o restante.

## 1. Contexto

- **Marca:** JWK Digital Branding, consultoria de branding estratégico em Fortaleza (CE), fundada em 2016.
- **Produto:** um CRM interno (baseado no Twenty, app React com Linaria) para gerenciar leads, propostas, projetos de branding, registros de marca no INPI e contratos recorrentes.
- **Usuários:** equipe pequena da JWK, uso diário, telas densas (tabelas, kanban, formulários, dashboards).
- **Idioma da interface:** português do Brasil.
- **Tema:** escuro é o padrão. Modo claro é secundário e fica para depois (ver seção 11).

## 2. Personalidade visual

Escuro, editorial, premium e sóbrio. Contraste forte entre um fundo quase preto e um único acento âmbar. Títulos em serifa elegante, corpo em sans neutra. Poucas cores, muito respiro, bordas finas em vez de sombras pesadas.

Palavras-guia: estratégico, refinado, silencioso, preciso.

Evitar: gradientes chamativos, cores saturadas fora da paleta, ícones coloridos, sombras grandes, cantos totalmente quadrados em botões, excesso de decoração.

## 3. Cores

### 3.1 Núcleo (extraído do site)

| Token | Valor | Uso |
|---|---|---|
| `bg-base` | `#0A0D10` | Fundo da aplicação, fundo de inputs |
| `bg-surface` | `#0F1318` | Cards, painéis, sidebar |
| `bg-elevated` | `#151A21` | Menus, popovers, modais, hover de linha |
| `bg-border` | `#1E2530` | Bordas e divisores |
| `amber` | `#F5A623` | Cor primária, ações principais, foco |
| `amber-dim` | `rgba(245,166,35,.10)` | Fundo de item selecionado, badge âmbar |
| `amber-border` | `rgba(245,166,35,.20)` | Borda de item selecionado |
| `blue` | `#6FA3D8` | Cor secundária, links, informação |
| `blue-dim` | `rgba(111,163,216,.10)` | Fundo de badge azul |
| `text-primary` | `#F0EBE3` | Texto principal (branco quente) |
| `text-secondary` | `#8A8F99` | Texto de apoio, rótulos |
| `text-muted` | `#4A5060` | Placeholders, itens desabilitados |

Cor do logo (monograma): `#F7AA0C` sobre `#0A0D10`.

### 3.2 Estados do acento (encontrados no CSS do site)

| Token | Valor | Uso |
|---|---|---|
| `amber-hover` | `#FFB733` | Hover do botão primário |
| `amber-hover-alt` | `#FFC04A` | Realce em texto âmbar |
| `amber-pressed` | `#E08800` | Estado pressionado |

### 3.3 Semânticas (parte do site, parte derivada)

| Token | Valor | Observação |
|---|---|---|
| `success` | `#22C55E` (texto/ícone `#4ADE80`) | Presente no site |
| `danger` | `#F87171` | Presente no site |
| `teal` | `#3ECFB2` | Presente no site; usar como acento de apoio em gráficos |
| `warning` | usar `amber` | Derivado: não criar uma terceira cor quente |
| `info` | usar `blue` | Derivado |

Para cada semântica, gere também `-dim` (fundo a 10%) e `-border` (borda a 20%), no mesmo padrão do âmbar.

### 3.4 Regras de contraste

- Texto sobre botão âmbar: sempre `bg-base` (`#0A0D10`), peso 600.
- Texto sobre fundos escuros: mínimo WCAG AA (4.5:1 para texto normal). `text-muted` só para placeholders e itens desabilitados, nunca para informação essencial.
- Nunca usar âmbar como cor de texto em corpo longo; apenas em títulos curtos, números e links de destaque.
- Informação nunca depende só da cor: acompanhar de ícone ou texto.

### 3.5 Paleta para gráficos (derivada)

Ordem de séries: `amber`, `blue`, `teal`, `#C5CDD7` (cinza claro), `#8A8F99`, `#4A5060`. Máximo de 6 séries. Linhas de grade em `bg-border`.

## 4. Tipografia

| Papel | Família | Pesos |
|---|---|---|
| Títulos e números de destaque | DM Serif Display (regular e itálico) | 400 |
| Interface e corpo | Inter | 300, 400, 500, 600 |
| Dados, IDs, números de processo, código | JetBrains Mono | 400, 500 |

Fonte via Google Fonts: `DM Serif Display:ital@0;1`, `Inter:wght@300;400;500;600`, `JetBrains Mono:wght@400;500`.

Estilos do site:
- Títulos (h1, h2): DM Serif Display, `line-height` 1.05 a 1.15, `letter-spacing` -0.03em.
- Corpo: Inter, `line-height` 1.6, antialiased.
- Botão: Inter 600, `0.88rem`, `letter-spacing` 0.02em.
- Rótulos pequenos em caixa alta (eyebrow): Inter ou Mono, `letter-spacing` entre 0.08em e 0.14em, caixa alta.

Escala para o CRM (derivada, pois o app é mais denso que o site). Base 14px, razão aproximada 1.2:

| Token | Tamanho | Uso |
|---|---|---|
| `display` | 40px, DM Serif | Título de página vazia, boas-vindas |
| `heading-lg` | 28px, DM Serif | Título de página |
| `heading-md` | 20px, DM Serif | Título de card e de seção |
| `heading-sm` | 16px, Inter 600 | Título de grupo, cabeçalho de modal |
| `body` | 14px, Inter 400 | Texto padrão |
| `body-sm` | 13px, Inter 400 | Tabelas, listas |
| `caption` | 12px, Inter 500 | Rótulos, metadados |
| `overline` | 11px, Inter 600, caixa alta, tracking 0.12em | Eyebrows, títulos de coluna |
| `mono` | 13px, JetBrains Mono | IDs, nº INPI, valores tabulares |

Números em tabelas e dashboards: `font-variant-numeric: tabular-nums`.

## 5. Espaçamento, raios e movimento

- **Unidade base:** 4px. Escala: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64.
- **Raios (do site):** inputs 6px; cards e painéis 12px (`radius-md`) e 18px (`radius-lg`); botões primários em pílula (28px, totalmente arredondados); badges em pílula; avatares circulares. O site também usa 10, 14, 16, 20 e 24px: consolidar em `radius-sm 6`, `radius-md 12`, `radius-lg 18`, `radius-pill 999`.
- **Bordas:** 1px sólida `bg-border`. Preferir borda a sombra para separar elementos.
- **Sombras (derivadas):** só em elementos flutuantes (menu, popover, modal): `0 12px 32px rgba(0,0,0,.45)`. Cards não têm sombra.
- **Movimento:** `250ms`, easing `cubic-bezier(.16,1,.3,1)` para entradas e `cubic-bezier(.4,0,.2,1)` para hover. Respeitar `prefers-reduced-motion`.
- **Foco visível:** anel de 2px em `amber` com 2px de afastamento (`outline-offset: 2px`). Nunca remover o foco.

## 6. Elevação (camadas)

| Nível | Fundo | Uso |
|---|---|---|
| 0 | `bg-base` | Página, inputs |
| 1 | `bg-surface` | Sidebar, cards, tabelas |
| 2 | `bg-elevated` | Popover, dropdown, tooltip, hover de linha |
| 3 | `bg-elevated` + sombra + overlay `rgba(0,0,0,.6)` | Modal, drawer |

## 7. Logo e marca

- Monograma JWK em âmbar `#F7AA0C` dentro de um quadrado arredondado `#0A0D10` (raio 8 em 32px). Referência: `https://www.jwk.com.br/favicon.svg`.
- Logotipo textual: "jwk" em minúsculas, DM Serif Display, com "®" sobrescrito.
- Entregar: versão compacta (só monograma, para sidebar recolhida e favicon) e versão horizontal (monograma + "jwk"), em SVG.
- Área de respiro mínima: metade da altura do monograma.

## 8. Componentes a criar

Para cada componente, entregue: variantes, tamanhos, todos os estados (padrão, hover, foco, pressionado, desabilitado e, quando fizer sentido, carregando, erro, vazio), e uma tela de exemplo.

### 8.1 Primitivos
1. **Button:** primário (fundo âmbar, texto escuro, pílula), secundário (borda `bg-border`, texto claro), ghost, perigo, ícone-apenas, com carregamento. Tamanhos sm (28), md (36), lg (44).
2. **Link:** azul `blue`, sublinhado no hover.
3. **Input de texto, textarea, input numérico e moeda (R$):** fundo `bg-base`, borda `bg-border`, raio 6, foco em âmbar, rótulo, ajuda e mensagem de erro.
4. **Select, multi-select, combobox com busca.**
5. **Checkbox, radio, switch.**
6. **Input de data e intervalo de datas** (formato dd/mm/aaaa).
7. **Input de telefone** (+55) e **e-mail.**
8. **Badge/tag:** neutra, âmbar, azul, verde, vermelho, teal; com ponto opcional.
9. **Avatar** e grupo de avatares.
10. **Ícones:** traço fino de 1.5px, 16/20/24px, cor herdada. Conjunto de linha único e consistente.
11. **Tooltip, divisor, skeleton, spinner, barra de progresso.**

### 8.2 Componentes compostos
12. **Card** (padrão, selecionável, com cabeçalho e ações).
13. **Tabela de dados:** cabeçalho em `overline`, linhas de 40px, hover em `bg-elevated`, seleção em `amber-dim`, ordenação, colunas fixas, paginação, estado vazio, estado de carregamento.
14. **Kanban:** coluna com título, contador e valor total; card de oportunidade (empresa, serviço, valor, responsável, prazo); estados de arrastar e soltar.
15. **Menu dropdown, menu de contexto, popover.**
16. **Modal, drawer lateral (painel de registro), diálogo de confirmação.**
17. **Abas e navegação secundária (tabs).**
18. **Toast/notificação** (sucesso, erro, aviso, informação).
19. **Barra de filtros** com chips de filtro e visões salvas.
20. **Estado vazio** (ilustração simples em traço + título em DM Serif + ação).
21. **Linha do tempo (timeline)** de atividades: e-mail, nota, tarefa, mudança de etapa.
22. **Stepper/indicador de fases**, com as 5 fases da metodologia: Diagnóstico, Estratégia, Identidade, Ativação, Continuidade.
23. **Campo de comentário/nota** com menções.

### 8.3 Padrões de tela (templates)
24. **Shell da aplicação:** sidebar de 240px (recolhível a 64px), barra superior com busca global (atalho Cmd/Ctrl+K), área de conteúdo.
25. **Lista de registros:** título, filtros, visões, tabela ou kanban.
26. **Página de registro:** cabeçalho com nome, etapa e ações, abas (Visão geral, Atividade, Arquivos, Projetos), painel lateral com campos.
27. **Dashboard:** grade de cards com KPI (número em DM Serif + variação), gráfico de barras, linha e funil, tabela resumida.
28. **Login e onboarding.**
29. **Configurações.**

### 8.4 Componentes específicos da JWK
30. **Card de KPI:** rótulo em `overline`, valor em DM Serif 40px, variação em verde/vermelho com seta, mini gráfico opcional.
31. **Badge de status de projeto:** em andamento, aguardando cliente, em revisão, concluído, pausado.
32. **Badge de status INPI:** em exame, exigência, publicado, deferido, indeferido, arquivado; com o número do processo em mono.
33. **Indicador de SLA de 24h:** contagem regressiva do primeiro retorno ao lead (neutro, aviso em âmbar nas últimas 4h, perigo ao vencer).
34. **Badge de origem do lead:** site, WhatsApp, Instagram, LinkedIn, indicação.
35. **Seletor de plano:** Essencial, Avançado, Executivo.

## 9. Tom de texto da interface

Direto, profissional, em português do Brasil, sem gírias e sem exclamações. Rótulos curtos. Exemplos: "Novo lead", "Mover para Proposta", "Nenhuma oportunidade nesta etapa", "Prazo de resposta vencido".

## 10. Formato da entrega

1. **Tokens** em JSON (cores, tipografia, espaçamento, raios, sombras, movimento), com nomes exatamente como acima, mais uma versão em variáveis CSS (`--jwk-*`).
2. **Biblioteca de componentes** com todos os itens da seção 8, organizada por categoria.
3. **Páginas de exemplo** para os templates 24 a 27.
4. **Guia de uso** com os "faça e não faça" da seção 12.
5. Preparar a saída para ser mapeada ao tema do Twenty (arquivos `ThemeDark.ts` e `ThemeCommon.ts` em `packages/twenty-ui/src/theme/constants`): os tokens de cor, fonte e raio devem ter correspondência direta.

## 11. Fora de escopo agora

Modo claro, versão mobile completa (o CRM será usado principalmente no desktop; garantir apenas que a leitura em tablet funcione), animações complexas, e-mails transacionais.

## 12. Faça e não faça

**Faça**
- Use um único acento (âmbar) por tela para a ação principal.
- Use DM Serif Display só em títulos e números de destaque; o restante em Inter.
- Separe camadas com cor de fundo e borda de 1px.
- Mantenha tabelas densas e legíveis, com números alinhados à direita.
- Garanta foco visível e contraste AA em tudo.

**Não faça**
- Não use mais de um botão primário por área.
- Não use cores fora da paleta nem gradientes decorativos.
- Não use sombras em cards.
- Não use DM Serif em texto pequeno (abaixo de 16px) nem em tabelas.
- Não comunique estado só por cor.
- Não invente valores: use sempre os tokens.

## 13. Fonte da identidade

Cores, fontes, raios e animações foram extraídos diretamente do CSS de https://www.jwk.com.br. Se houver manual de marca ou arquivos de logo oficiais (SVG, PNG), eles têm prioridade sobre este documento.
