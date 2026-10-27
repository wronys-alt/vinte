# Plano: CRM JWK Digital Branding (sobre o Twenty)

## 1. Decisões de arquitetura

- Base: fork do Twenty, sem alterar o core sempre que possível.
- Customização de dados e UX via app SDK em `packages/twenty-apps/internal/jwk`, modelado em `internal/real-estate`.
- Identidade visual: tema próprio em `twenty-ui` (mudança pequena e isolada no core, ver seção 3).
- Hospedagem: VPS Hostinger com Docker Compose oficial (ver seção 5).

## 2. Modelo de dados (app `jwk`)

Objetos nativos reaproveitados: Company, Person, Opportunity, Task, Note, Workflow, Dashboard.

Objetos novos:

| Objeto | Campos principais |
|---|---|
| Serviço | nome, linha (Branding, Registro, Gestão), tipo (projeto ou recorrente), valor base, duração |
| Projeto | empresa, serviço, fase (Diagnóstico, Estratégia, Identidade, Ativação, Continuidade), início, entrega, responsável, status |
| Marca registrada (INPI) | empresa, marca, nº do processo, classe, status, protocolo, próximo prazo |
| Contrato recorrente | empresa, serviço/plano (Essencial, Avançado, Executivo), valor mensal, início, renovação, status |

Campos novos em objetos nativos:
- Company: porte, setor, faturamento, estágio da marca, fit com o público-alvo (sim, não, revisar).
- Person: origem do lead (site, WhatsApp, Instagram, LinkedIn, indicação), idioma.
- Opportunity: serviços de interesse, data da reunião de alinhamento, resposta em 24h (sim/não).

Funil de vendas: Lead, Reunião de alinhamento, Diagnóstico inicial, Proposta, Fechado ganho, Fechado perdido.
Funil de entrega: as 5 fases da metodologia, no objeto Projeto.

Roles: Fundador (tudo), Comercial, Entrega.
Views: pipeline kanban, leads sem resposta há mais de 24h, projetos por fase, marcas INPI com prazo próximo, renovações dos próximos 60 dias.
Dashboard: leads por origem, conversão por etapa, receita recorrente mensal, projetos em andamento.

## 3. Identidade visual

Extraída de https://www.jwk.com.br (CSS real, não estimada).

| Token | Valor |
|---|---|
| Fundo base | `#0A0D10` |
| Superfície | `#0F1318` |
| Elevado | `#151A21` |
| Borda | `#1E2530` |
| Âmbar (primária) | `#F5A623` (variação do logo: `#F7AA0C`) |
| Azul (secundária) | `#6FA3D8` |
| Texto primário | `#F0EBE3` |
| Texto secundário | `#8A8F99` |
| Texto discreto | `#4A5060` |
| Tipografia | títulos DM Serif Display, corpo Inter (300 a 600), dados JetBrains Mono |
| Raios | 12px (médio), 18px (grande) |
| Movimento | `cubic-bezier(.16,1,.3,1)`, 250ms |

Tom: escuro, editorial, premium. O logo é um monograma âmbar sobre fundo escuro com cantos arredondados (`favicon.svg`).

Aplicação no Twenty:
- Editar `packages/twenty-ui/src/theme/constants/ThemeDark.ts` (e `ThemeCommon.ts` para fontes e raios) com a paleta acima. Tema escuro como padrão.
- Fontes carregadas em `packages/twenty-front/index.html`.
- Logo e favicon em `packages/twenty-front/public`.
- Cuidado: contraste do âmbar sobre fundo escuro é bom, mas o texto sobre botão âmbar deve ser escuro (`#0A0D10`). Validar WCAG AA.
- Modo claro: derivar depois, apenas se necessário.
- E-mails transacionais (`twenty-emails`) com a mesma paleta, em fase posterior.

## 4. Integrações

1. Formulário do site para o CRM (cria Person, Company e Opportunity via API/webhook). Inclui consentimento LGPD e origem do lead.
2. Brevo: sincronização de contatos da newsletter.
3. Google/Microsoft: e-mail e calendário nativos (reuniões de 30 min).
4. WhatsApp: fase posterior (WhatsApp Business API via logic functions). Início com registro manual.
5. Workflows: lead novo vira tarefa com prazo de 24h; alerta de prazo INPI; lembrete de renovação.

## 5. Hospedagem na Hostinger

Veredito: serve, desde que seja **VPS**. Hospedagem compartilhada, Cloud Startup e Web Hosting não rodam o Twenty (precisa de Docker, Postgres e Redis).

- Mínimo oficial: 2 GB de RAM. Recomendado: **KVM 2 (2 vCPU, 8 GB)** para folga com o worker, o Postgres e o Redis.
- Sistema: Ubuntu 24.04, com Docker (a Hostinger oferece template com Docker).
- Subir com `packages/twenty-docker/docker-compose.yml`: server, worker, db, redis.
- Domínio: `crm.jwk.com.br`, DNS apontando para o IP da VPS. Proxy reverso com HTTPS (Caddy ou Nginx com Let's Encrypt).
- Storage: volume local no início. Migrar para S3/R2 se os anexos crescerem.
- Backup: snapshot semanal da Hostinger **mais** `pg_dump` diário enviado para armazenamento externo (Drive, R2 ou S3). Snapshot sozinho não basta.
- Segurança: firewall liberando só 22, 80 e 443; SSH por chave; fail2ban; chaves `APP_SECRET` e `ENCRYPTION_KEY` guardadas fora do servidor.
- Manutenção: você assume atualizações, monitoramento e restauração. Se não quiser essa carga, o Twenty Cloud evita tudo isso, ao custo mensal por usuário.
- Limite: um único servidor, sem alta disponibilidade. Para uma consultoria pequena é adequado.

## 6. Fases e entregas

| Fase | Entrega | Pronto quando |
|---|---|---|
| 0. Base | Ambiente local rodando, tema JWK aplicado | Login, tela de empresas e pipeline com a identidade JWK |
| 1. Dados | App `jwk`: objetos, campos, funil, roles, views | Cadastro de ponta a ponta de um lead até um projeto |
| 2. Dashboard e workflows | Dashboard comercial, tarefas de 24h, alertas INPI e renovação | Alertas disparando em dados de teste |
| 3. Captação | Formulário do site integrado, Brevo | Lead do site aparece no CRM em segundos |
| 4. Produção | VPS Hostinger, HTTPS, backups testados | Restauração de backup validada |
| 5. Migração | Importar clientes e propostas atuais (CSV) | Base real carregada |
| 6. Depois | WhatsApp, e-mails com marca, modo claro | Conforme prioridade |

Ordem sugerida: 0, 1, 4 (subir cedo para usar de verdade), depois 2, 3 e 5.

## 7. Riscos

- Atualizar o fork do upstream: mantendo as mudanças no app e no tema, o conflito fica restrito a 2 ou 3 arquivos do `twenty-ui`.
- Licença AGPL: uso interno não exige abrir o código.
- Dados pessoais (LGPD): consentimento no formulário, backup criptografado, acesso por role.
- Perguntas em aberto: etapas reais do funil, quem usa o CRM, valores dos planos, se há base de clientes para importar.
