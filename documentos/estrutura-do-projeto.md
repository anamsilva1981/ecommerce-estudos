# E-commerce para Estudos — Estrutura e Ordem de Execução

## Objetivo

Este documento organiza o projeto de e-commerce em **3 grandes fases de evolução**, deixando explícito:

- **o que será construído**;
- **em que ordem**;
- **em qual visão** a funcionalidade aparece: Cliente, Admin ou ambas;
- **quem implementa**: Frontend, Backend ou ambos;
- **por que aquela etapa vem naquele momento**;
- **de que etapa ela depende**.

A divisão de responsabilidades do projeto é fixa:

- **Frontend:** responsável por toda a aplicação web, incluindo a visão do Cliente e a visão do Admin.
- **Backend:** responsável por APIs, banco de dados, autenticação, regras de negócio, integrações e persistência.

> Regra principal de execução: **configurar/cadastrar → persistir/expor → consumir → interagir → registrar consequência**.

---

# Fase 1 — E-commerce Essencial

## Objetivo da fase

Entregar um e-commerce funcional de ponta a ponta, no qual a loja consiga cadastrar produtos e o cliente consiga encontrá-los, comprar, pagar e acompanhar o pedido.

| Ordem | Módulo / Entrega | Visão | Responsável | Por que vem aqui | Dependência principal |
|---:|---|---|---|---|---|
| 1 | Fundação do projeto: estrutura de pastas, rotas, layout base, tema e design system inicial | Compartilhado | Frontend | Cria a base técnica usada por todas as telas seguintes | Nenhuma |
| 2 | Header, navbar, footer e componentes básicos reutilizáveis | Cliente / Compartilhado | Frontend | Define a estrutura visual comum da aplicação | Fundação |
| 3 | Modelagem inicial de produto, categoria, marca, SKU, preço e estoque | Interno | Backend | Define os dados que alimentarão Admin e Cliente | Fundação técnica do backend |
| 4 | CRUD de categorias | Admin | Frontend + Backend | Produto depende de categoria para ser cadastrado corretamente | Modelagem |
| 5 | CRUD de marcas | Admin | Frontend + Backend | Permite associar produtos a fabricantes/marcas | Modelagem |
| 6 | CRUD de produtos | Admin | Frontend + Backend | É a origem dos dados que aparecerão na loja | Categorias e marcas |
| 7 | Imagens, especificações, preço e SKU do produto | Admin | Frontend + Backend | Completa o cadastro necessário para exibição e compra | CRUD de produtos |
| 8 | Estoque inicial por SKU | Admin | Frontend + Backend | Define disponibilidade real do produto | Produto/SKU |
| 9 | API pública/interna de produtos e categorias | Ambas | Backend | Permite que o frontend consuma os produtos cadastrados | CRUD e banco |
| 10 | Catálogo / listagem de produtos | Cliente | Frontend | Primeira visualização dos dados cadastrados pelo Admin | API de produtos |
| 11 | Card de produto reutilizável | Cliente | Frontend | Será usado em catálogo, Home, busca e vitrines | API de produtos |
| 12 | Página de detalhe do produto (PDP) | Cliente | Frontend + Backend | Permite conhecer o produto antes da compra | Catálogo + API |
| 13 | Busca básica, filtros, ordenação e paginação | Cliente | Frontend + Backend | Facilita descoberta quando o catálogo cresce | Catálogo |
| 14 | Home com banners, categorias e vitrines | Cliente | Frontend | A Home passa a reutilizar componentes e dados reais já existentes | Card + catálogo + categorias |
| 15 | Cadastro de cliente | Cliente | Frontend + Backend | Introduz identidade do comprador | Usuários no backend |
| 16 | Login, logout, sessão e recuperação de senha | Cliente | Frontend + Backend | Permite associar carrinho, endereços e pedidos ao usuário | Cadastro |
| 17 | Minha conta e dados pessoais | Cliente | Frontend + Backend | Centraliza dados do comprador | Autenticação |
| 18 | Endereços do cliente | Cliente | Frontend + Backend | O checkout precisa de um destino de entrega | Minha conta |
| 19 | Gestão básica de clientes | Admin | Frontend + Backend | Permite à operação consultar clientes cadastrados | Usuários |
| 20 | Carrinho | Cliente | Frontend + Backend | Conecta catálogo ao fluxo de compra | Produto + autenticação opcional |
| 21 | Validação de preço e estoque no carrinho | Interno | Backend | Evita comprar item indisponível ou com preço desatualizado | Carrinho + estoque |
| 22 | Gestão de estoque e movimentações básicas | Admin | Frontend + Backend | A operação precisa ajustar e acompanhar disponibilidade | Estoque inicial |
| 23 | Configuração básica de frete | Admin | Frontend + Backend | Define modalidades, regras, prazo e preço de entrega | Endereços + produtos |
| 24 | Consulta de CEP e opções de entrega | Cliente | Frontend + Backend | Permite calcular frete antes/finalização da compra | Configuração de frete |
| 25 | Checkout | Cliente | Frontend | Organiza identificação, endereço, frete, resumo e pagamento | Carrinho + endereço + frete |
| 26 | Criação do pedido | Interno | Backend | Converte o checkout em uma transação persistida | Checkout |
| 27 | Confirmação e detalhe do pedido | Cliente | Frontend + Backend | Dá retorno após a compra e permite consulta | Pedido criado |
| 28 | Meus pedidos | Cliente | Frontend + Backend | Permite acompanhar compras anteriores e atuais | Pedido |
| 29 | Gestão de pedidos | Admin | Frontend + Backend | A operação precisa consultar e alterar status | Pedido |
| 30 | Integração de pagamento em sandbox | Interno | Backend | Permite validar o fluxo financeiro sem operação real | Pedido |
| 31 | Seleção e retorno de pagamento | Cliente | Frontend | Cliente escolhe forma de pagamento e recebe o estado da transação | Gateway/backend |
| 32 | Atualização de pedido após pagamento | Interno | Backend | Mantém pedido coerente com o status financeiro | Webhook/pagamento |
| 33 | Baixa/reserva de estoque após compra | Admin / Interno | Backend | Garante consistência entre venda e disponibilidade | Pedido + pagamento |
| 34 | Segurança básica e separação Cliente/Admin | Ambas | Frontend + Backend | Protege dados e rotas administrativas | Autenticação |
| 35 | LGPD básica, consentimento e privacidade | Cliente / Interno | Frontend + Backend | Inclui requisitos mínimos de privacidade desde o início | Cadastro/autenticação |
| 36 | Testes unitários, integração e E2E do fluxo principal | Ambas | Frontend + Backend | Garante que o fluxo crítico funcione antes de evoluir | Funcionalidades da fase |
| 37 | CI/CD e deploy inicial | Infraestrutura | Frontend + Backend | Automatiza build, testes e entrega | Aplicação funcional |

## Fluxo principal da Fase 1

```text
ADMIN
Categoria / Marca
      ↓
Produto / SKU / Preço / Estoque
      ↓
BACKEND
Banco + API
      ↓
CLIENTE
Catálogo → Card → Detalhe → Home
      ↓
Autenticação
      ↓
Carrinho
      ↓
Frete
      ↓
Checkout
      ↓
Pedido
      ↓
Pagamento
      ↓
Atualização de estoque
      ↓
ADMIN
Gestão do pedido
```

---

# Fase 2 — E-commerce Profissional

## Objetivo da fase

Transformar o e-commerce essencial em uma operação mais completa, com relacionamento com o cliente, promoção, pós-venda, conteúdo, administração robusta e inteligência de negócio.

| Ordem | Módulo / Entrega | Visão | Responsável | Por que vem aqui | Dependência principal |
|---:|---|---|---|---|---|
| 38 | Favoritos / wishlist | Cliente | Frontend + Backend | Aumenta retenção e depende de usuário e catálogo já maduros | Cliente + produtos |
| 39 | Cupons | Cliente / Admin | Frontend + Backend | Introduz regras comerciais sobre carrinho/checkout existentes | Carrinho + preços |
| 40 | Promoções e campanhas | Cliente / Admin | Frontend + Backend | Evolui preço para regras temporais e segmentadas | Produtos + preços |
| 41 | Histórico e regras avançadas de preço | Admin / Interno | Frontend + Backend | Dá rastreabilidade e maior controle comercial | Preços/promos |
| 42 | Avaliações de produtos | Cliente / Admin | Frontend + Backend | Exige cliente, produto e pedido para validar compra | Pedidos entregues |
| 43 | Perguntas e respostas | Cliente / Admin | Frontend + Backend | Cria interação pré-compra e moderação | Produto + usuário |
| 44 | Comparador de produtos | Cliente | Frontend + Backend | Usa especificações já consolidadas do catálogo | Produtos/especificações |
| 45 | Produtos relacionados e similares | Cliente | Frontend + Backend | Cria cross-sell a partir do catálogo existente | Catálogo |
| 46 | Vistos recentemente | Cliente | Frontend + Backend | Primeira personalização baseada em comportamento | Usuário + produto |
| 47 | Recomendações básicas | Cliente | Frontend + Backend | Evolui descoberta usando eventos e histórico | Analytics básico |
| 48 | Notificações transacionais por e-mail | Cliente / Interno | Backend | Automatiza comunicação de pedidos e conta | Pedido + autenticação |
| 49 | Central de notificações | Cliente | Frontend + Backend | Consolida comunicações dentro da aplicação | Eventos de negócio |
| 50 | Cancelamento de pedido | Cliente / Admin | Frontend + Backend | Primeiro fluxo relevante de pós-venda | Pedido + pagamento |
| 51 | Troca e devolução | Cliente / Admin | Frontend + Backend | Expande pós-venda com workflow próprio | Pedido entregue |
| 52 | Reembolso / estorno | Admin / Interno | Backend | Liga pós-venda ao gateway financeiro | Pagamento + devolução |
| 53 | Garantia / RMA básico | Cliente / Admin | Frontend + Backend | Completa suporte pós-venda para eletrônicos | Pedido + produto |
| 54 | Atendimento / tickets | Cliente / Admin | Frontend + Backend | Centraliza solicitações relacionadas à operação | Cliente + pedido |
| 55 | CMS para banners e vitrines | Admin | Frontend + Backend | Retira conteúdo comercial do código | Home já funcional |
| 56 | Landing pages e conteúdo institucional | Cliente / Admin | Frontend + Backend | Permite campanhas sem novo deploy | CMS |
| 57 | Administração de usuários internos | Admin | Frontend + Backend | Necessário quando mais pessoas operam o painel | Autenticação |
| 58 | Roles e permissões (RBAC) | Admin / Interno | Frontend + Backend | Evita que todos os administradores tenham acesso total | Usuários internos |
| 59 | Auditoria de ações administrativas | Admin / Interno | Backend | Registra alterações sensíveis | RBAC |
| 60 | Financeiro operacional | Admin | Frontend + Backend | Consolida recebimentos, taxas, estornos e conciliação | Pedidos/pagamentos |
| 61 | Fiscal / nota fiscal | Admin / Interno | Backend | Introduz emissão e tratamento fiscal da venda | Pedido pago |
| 62 | Analytics de produto e funil | Admin | Frontend + Backend | Passa a medir comportamento e conversão | Eventos de uso |
| 63 | Dashboard de negócio | Admin | Frontend + Backend | Apresenta receita, ticket, conversão e produtos | Analytics |
| 64 | Marketing e newsletter | Cliente / Admin | Frontend + Backend | Permite aquisição e retenção | Clientes + CMS |
| 65 | Carrinho abandonado | Cliente / Interno | Backend | Usa comportamento e notificações para recuperação | Carrinho + notificações |
| 66 | Fidelidade / cashback / pontos | Cliente / Admin | Frontend + Backend | Adiciona retenção com regra financeira própria | Cliente + pedidos |
| 67 | Acessibilidade completa | Cliente / Admin | Frontend | Consolida WCAG sobre a interface já mais estável | Interfaces consolidadas |
| 68 | Performance web | Cliente | Frontend | Otimiza experiência conforme conteúdo e tráfego aumentam | Store funcional |
| 69 | Integrações externas adicionais | Interno | Backend | ERP, CRM, transportadoras e outros sistemas | Domínios consolidados |
| 70 | Testes profissionais da Fase 2 | Ambas | Frontend + Backend | Aumenta segurança antes de trabalhar escala | Fase 2 funcional |

---

# Fase 3 — Grande Operação / Escala

## Objetivo da fase

Evoluir o sistema para estudar problemas típicos de grandes operações: volume, concorrência, resiliência, observabilidade, busca especializada, marketplace e arquitetura distribuída.

| Ordem | Módulo / Entrega | Visão | Responsável | Por que vem aqui | Dependência principal |
|---:|---|---|---|---|---|
| 71 | Event tracking completo | Interno | Frontend + Backend | Cria base confiável para comportamento, BI e automação | Analytics |
| 72 | Filas e processamento assíncrono | Interno | Backend | Remove tarefas lentas do fluxo síncrono | Eventos de domínio |
| 73 | Eventos de domínio | Interno | Backend | Desacopla pedido, pagamento, estoque e notificação | Domínios maduros |
| 74 | Retry, idempotência e dead-letter queue | Interno | Backend | Garante resiliência em processamento distribuído | Filas/eventos |
| 75 | Cache com Redis | Interno | Backend | Reduz carga em produtos, categorias e sessões | APIs estáveis |
| 76 | Estratégias de invalidação de cache | Interno | Backend | Mantém consistência dos dados cacheados | Redis |
| 77 | CDN e otimização avançada de mídia | Cliente / Infra | Frontend + Infra | Melhora entrega global de assets | Store madura |
| 78 | Busca com Elasticsearch/OpenSearch | Cliente / Interno | Frontend + Backend | Substitui busca simples por mecanismo especializado | Catálogo grande |
| 79 | Fuzzy search, sinônimos, ranking e facetas | Cliente | Frontend + Backend | Aproxima a experiência de grandes varejistas | Search engine |
| 80 | Recomendação avançada | Cliente / Interno | Frontend + Backend | Usa comportamento e histórico em maior escala | Eventos + analytics |
| 81 | Observabilidade: logs estruturados | Interno | Backend + Infra | Permite diagnóstico consistente | Serviços funcionando |
| 82 | Métricas e dashboards técnicos | Interno | Backend + Infra | Mede saúde e capacidade | Logs/monitoramento |
| 83 | Distributed tracing / OpenTelemetry | Interno | Backend + Infra | Necessário quando uma operação atravessa vários serviços | Serviços distribuídos |
| 84 | Alertas e health checks | Interno | Backend + Infra | Detecta falhas antes de impacto prolongado | Observabilidade |
| 85 | Testes de carga e performance | Interno | Frontend + Backend | Revela gargalos sob tráfego alto | Observabilidade |
| 86 | Rate limiting e proteção contra abuso | Interno | Backend | Protege APIs em cenários de grande volume | APIs públicas |
| 87 | Segurança avançada / OWASP | Ambas | Frontend + Backend | Endurece aplicação antes de exposição maior | Segurança básica |
| 88 | Antifraude avançado | Interno | Backend | Reduz risco financeiro em alto volume | Pagamentos |
| 89 | Múltiplos centros de distribuição | Admin / Interno | Frontend + Backend | Adiciona complexidade logística real | Estoque/logística |
| 90 | Split de estoque e entrega | Cliente / Interno | Frontend + Backend | Permite pedido atendido por mais de um CD | Multi-CD |
| 91 | Marketplace: cadastro de sellers | Admin / Seller | Frontend + Backend | Abre nova dimensão de negócio | E-commerce maduro |
| 92 | Produtos e estoque por seller | Admin / Seller | Frontend + Backend | Cada vendedor passa a operar seu catálogo | Sellers |
| 93 | Pedido dividido por seller | Cliente / Interno | Frontend + Backend | Um carrinho pode originar múltiplos fluxos operacionais | Marketplace |
| 94 | Comissão e split de pagamento | Admin / Interno | Backend | Implementa economia do marketplace | Seller + pagamento |
| 95 | Repasses e conciliação de seller | Admin / Seller | Frontend + Backend | Completa o ciclo financeiro do marketplace | Split de pagamento |
| 96 | Reputação e SLA de seller | Cliente / Admin | Frontend + Backend | Permite governança da operação multi-seller | Marketplace |
| 97 | Feature flags | Interno | Frontend + Backend | Permite releases graduais e experimentação segura | CI/CD maduro |
| 98 | Deploy gradual / rollback | Infraestrutura | Frontend + Backend | Reduz risco de releases em produção | CI/CD |
| 99 | Escalabilidade horizontal | Infraestrutura | Backend + Infra | Suporta crescimento de tráfego | Métricas/carga |
| 100 | Load balancing | Infraestrutura | Backend + Infra | Distribui tráfego entre instâncias | Escala horizontal |
| 101 | Banco com réplicas / estratégias de escala | Interno | Backend + Infra | Aumenta capacidade e disponibilidade de persistência | Gargalo comprovado |
| 102 | Circuit breaker e resiliência | Interno | Backend | Impede falhas em cascata | Serviços distribuídos |
| 103 | Extração seletiva de microsserviços | Interno | Backend | Só ocorre quando limites e gargalos reais justificarem | Monólito modular maduro |
| 104 | Testes de contrato | Interno | Frontend + Backend | Protege comunicação entre serviços independentes | Microsserviços/APIs |
| 105 | Alta disponibilidade e disaster recovery | Infraestrutura | Backend + Infra | Fecha o ciclo de operação em escala | Arquitetura distribuída |

---

# Organização das frentes

## Visão do Cliente

Exemplos de funcionalidades dessa frente:

- Home;
- catálogo;
- busca;
- página de produto;
- autenticação;
- conta;
- favoritos;
- carrinho;
- frete;
- checkout;
- pagamento;
- pedidos;
- avaliações;
- perguntas;
- pós-venda;
- atendimento.

## Visão do Admin

Exemplos de funcionalidades dessa frente:

- categorias;
- marcas;
- produtos;
- SKU;
- preços;
- estoque;
- clientes;
- pedidos;
- frete;
- promoções;
- cupons;
- CMS;
- avaliações/moderação;
- pós-venda;
- usuários internos;
- permissões;
- financeiro;
- fiscal;
- analytics.

## Responsabilidade do Frontend

O Frontend implementa as duas experiências visuais:

```text
frontend
├── store      # visão do cliente
├── admin      # visão da operação da loja
└── shared     # código reutilizado entre as duas frentes
```

O `shared` não é uma terceira aplicação de negócio. Ele reúne elementos reutilizáveis, como:

- componentes de UI;
- models/types;
- services;
- utilitários;
- validações;
- loaders;
- tratamento visual de erro.

## Responsabilidade do Backend

O Backend é responsável por:

- modelagem de domínio;
- banco de dados;
- migrations;
- APIs;
- autenticação;
- autorização;
- regras de negócio;
- validação de estoque e preço;
- pedidos;
- pagamentos;
- integrações externas;
- filas/eventos;
- persistência;
- segurança de dados;
- processamento assíncrono.

---

# Regra de trabalho da dupla

Cada funcionalidade deve ser construída como uma **fatia vertical**, mantendo as responsabilidades fixas:

```text
Definir funcionalidade
        ↓
Alinhar contrato Front ↔ Back
        ↓
Frontend implementa Cliente/Admin
        +
Backend implementa API/regra/banco
        ↓
Integrar
        ↓
Testar
        ↓
Fechar a funcionalidade
        ↓
Ir para a próxima dependência
```

Não é recomendado construir todo o frontend e somente depois começar todo o backend. O ideal é fechar uma funcionalidade de ponta a ponta antes de avançar.

Exemplo:

```text
Categorias
   ↓
Produtos
   ↓
Catálogo
   ↓
Detalhe
   ↓
Home
```

Depois:

```text
Autenticação
   ↓
Carrinho
   ↓
Frete
   ↓
Checkout
   ↓
Pedido
   ↓
Pagamento
```

---

# Resumo das três fases

| Fase | Objetivo | Resultado esperado |
|---|---|---|
| **Fase 1 — Essencial** | Construir o fluxo de venda ponta a ponta | Loja cadastra; cliente encontra, compra e acompanha |
| **Fase 2 — Profissional** | Completar operação, experiência e gestão | Promoções, avaliações, pós-venda, CMS, financeiro, BI etc. |
| **Fase 3 — Escala** | Estudar problemas de grandes operações | Eventos, filas, cache, busca avançada, marketplace e sistemas distribuídos |

## Princípio arquitetural

O projeto deve começar como um **monólito modular bem estruturado**, evitando introduzir microsserviços sem necessidade.

Exemplo inicial:

```text
commerce
├── catalog
├── customers
├── cart
├── inventory
├── checkout
├── orders
├── payments
├── shipping
├── promotions
└── reviews
```

Somente na Fase 3, quando houver motivos técnicos reais para estudar desacoplamento, determinados módulos poderão ser extraídos para serviços independentes.

---

# Resultado final da trilha

A evolução planejada é:

```text
CRUD e API
    ↓
E-commerce funcional
    ↓
E-commerce profissional
    ↓
Operação orientada a eventos
    ↓
Alta escala e sistemas distribuídos
```

Assim, o projeto funciona simultaneamente como **produto de e-commerce** e como **trilha prática de estudos de engenharia de software**.
