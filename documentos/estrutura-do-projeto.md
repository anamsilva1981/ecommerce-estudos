# Mercado Online para Estudos — Descrição do Projeto

## 1. Visão geral

Este projeto será um **mercado online**, construído com finalidade de estudo prático de desenvolvimento de software.

A aplicação representará um mercado real no qual:

- o **cliente** poderá acessar a loja, localizar produtos, adicionar itens ao carrinho e realizar uma compra;
- o **administrador do mercado** poderá cadastrar e manter produtos, controlar estoque, acompanhar pedidos e visualizar indicadores do negócio;
- o **Frontend** será responsável por toda a experiência visual e interação nas áreas Cliente e Admin;
- o **Backend** será responsável por banco de dados, APIs, autenticação, regras de negócio, persistência e integrações.

O objetivo não é reproduzir uma grande plataforma como KaBuM, Amazon ou Mercado Livre. O projeto será propositalmente menor, mas deverá representar um **produto real e completo**, permitindo estudar como as partes de uma aplicação comercial se relacionam de ponta a ponta.

---

## 2. Objetivo de aprendizagem

O projeto será usado como laboratório de desenvolvimento.

A proposta é não apenas implementar telas, mas entender antes de cada etapa:

1. qual problema aquela parte resolve;
2. quais alternativas técnicas existem;
3. quais decisões precisam ser tomadas;
4. quais dependências existem entre Frontend e Backend;
5. como implementar;
6. como validar se a implementação está correta.

Os documentos detalhados de cada etapa funcionarão como **guias de estudo e execução**.

---

## 3. Áreas da aplicação

O sistema terá duas experiências principais no Frontend.

### 3.1. Loja — visão do Cliente

É a aplicação usada por quem deseja fazer compras no mercado.

Exemplos:

- Home;
- catálogo;
- categorias;
- busca;
- página de produto;
- carrinho;
- login e cadastro;
- endereços;
- checkout;
- pagamento;
- pedidos.

### 3.2. Painel Administrativo — visão do Mercado

É a aplicação usada pela operação e gestão do mercado.

Exemplos:

- cadastro de categorias;
- cadastro de produtos;
- controle de preço;
- estoque;
- pedidos;
- clientes;
- promoções;
- dashboard gerencial com indicadores de vendas e desempenho.

> Cliente e Admin pertencem ao mesmo produto, mas possuem objetivos, permissões e interfaces diferentes.

---

## 4. Divisão de responsabilidades

| Área | Responsabilidade |
|---|---|
| **Frontend** | Interfaces Cliente e Admin, navegação, componentes, formulários, estados da interface, consumo das APIs, responsividade, acessibilidade e testes de interface |
| **Backend** | APIs, banco de dados, autenticação, autorização, regras de negócio, estoque, carrinho persistido, pedidos, pagamentos, indicadores agregados e integrações |
| **Ambos** | Definição dos contratos das APIs, fluxos funcionais, tratamento de erros, integração e testes de ponta a ponta |

As responsabilidades permanecem fixas durante o projeto: **Frontend não precisa trocar de papel com Backend e vice-versa**.

---

# 5. Módulos do projeto

O escopo será organizado em **19 módulos funcionais**.

| Nº | Módulo | Principal visão | Implementação | O que resolve |
|---:|---|---|---|---|
| 1 | Fundação do projeto | Compartilhado | Frontend | Estrutura inicial, arquitetura de pastas, rotas, layouts, tema e base do Design System |
| 2 | Estrutura visual da loja | Cliente | Frontend | Header, navegação, footer e elementos reutilizáveis da experiência do cliente |
| 3 | Categorias | Admin + Cliente | Frontend + Backend | Organiza produtos em grupos como bebidas, limpeza, higiene e alimentos |
| 4 | Produtos | Admin + Cliente | Frontend + Backend | Permite cadastrar, editar, listar e consultar produtos |
| 5 | Preços | Admin + Cliente | Frontend + Backend | Mantém e apresenta o preço atual de cada produto |
| 6 | Estoque | Admin + Interno | Frontend + Backend | Controla quantidade disponível e indisponibilidade de produtos |
| 7 | Catálogo e descoberta | Cliente | Frontend + Backend | Exibe produtos por lista, categoria, busca, filtro e ordenação |
| 8 | Home e vitrines | Cliente | Frontend + Backend | Apresenta categorias, ofertas e produtos em destaque |
| 9 | Autenticação | Cliente + Admin | Frontend + Backend | Cadastro, login, sessão, logout e controle de acesso |
| 10 | Cliente e endereços | Cliente + Admin | Frontend + Backend | Mantém dados pessoais e locais de entrega |
| 11 | Carrinho | Cliente | Frontend + Backend | Armazena os itens escolhidos, quantidades e resumo da compra |
| 12 | Entrega | Cliente + Admin | Frontend + Backend | Define área atendida, taxa, modalidade e prazo de entrega |
| 13 | Checkout | Cliente | Frontend + Backend | Reúne endereço, entrega, itens, valores e confirmação antes da compra |
| 14 | Pagamento | Cliente + Interno | Frontend + Backend | Registra e acompanha a forma e o estado do pagamento |
| 15 | Pedidos | Cliente + Admin | Frontend + Backend | Cria a compra e permite acompanhamento pelo cliente e pelo mercado |
| 16 | Promoções | Cliente + Admin | Frontend + Backend | Permite preços promocionais, ofertas e campanhas simples |
| 17 | Substituição / indisponibilidade | Cliente + Admin | Frontend + Backend | Trata o cenário em que um produto comprado fica indisponível durante a separação |
| 18 | Qualidade e entrega técnica | Compartilhado | Frontend + Backend | Testes, segurança básica, acessibilidade, CI/CD e deploy |
| 19 | Dashboard gerencial | Admin / Proprietário | Frontend + Backend | Permite ao dono do mercado acompanhar vendas, evolução do faturamento, pedidos e outros indicadores do negócio |

---

# 6. Fases do projeto

Os módulos não serão construídos de uma vez. O projeto será evoluído em **3 fases**.

## Fase 1 — Mercado funcional

### Objetivo

Construir o menor fluxo completo capaz de representar uma compra real.

### Resultado esperado

Ao final desta fase:

> **o mercado cadastra um produto → o cliente encontra o produto → adiciona ao carrinho → informa onde receber → finaliza a compra → o mercado recebe o pedido.**

| Ordem | Entrega | Visão | Responsável principal |
|---:|---|---|---|
| 1 | [Fundação do projeto](./fase-1/01-fundacao-do-projeto.md) | Compartilhado | Frontend |
| 2 | Estrutura visual da loja | Cliente | Frontend |
| 3 | Categorias | Admin + Cliente | Frontend + Backend |
| 4 | Produtos | Admin + Cliente | Frontend + Backend |
| 5 | Preços | Admin + Cliente | Frontend + Backend |
| 6 | Estoque básico | Admin + Interno | Frontend + Backend |
| 7 | Catálogo e página de produto | Cliente | Frontend + Backend |
| 8 | Home com produtos reais | Cliente | Frontend + Backend |
| 9 | Carrinho | Cliente | Frontend + Backend |
| 10 | Cliente e endereço de entrega | Cliente | Frontend + Backend |
| 11 | Entrega básica | Cliente + Admin | Frontend + Backend |
| 12 | Checkout | Cliente | Frontend + Backend |
| 13 | Pedido | Cliente + Admin | Frontend + Backend |

### Observação

Pagamento real não precisa bloquear a primeira versão. Inicialmente, o pedido pode ser criado com uma forma de pagamento simulada ou controlada em ambiente de teste.

---

## Fase 2 — Operação realista de mercado

### Objetivo

Adicionar funcionalidades que tornam a aplicação mais próxima da rotina de um mercado real.

| Ordem | Entrega | Visão | Responsável principal |
|---:|---|---|---|
| 14 | Autenticação completa | Cliente + Admin | Frontend + Backend |
| 15 | Minha conta e histórico | Cliente | Frontend + Backend |
| 16 | Gestão de clientes | Admin | Frontend + Backend |
| 17 | Pagamento integrado em sandbox | Cliente + Interno | Frontend + Backend |
| 18 | Gestão completa de pedidos | Admin | Frontend + Backend |
| 19 | Movimentação de estoque | Admin | Frontend + Backend |
| 20 | Promoções e ofertas | Cliente + Admin | Frontend + Backend |
| 21 | Tratamento de item indisponível | Cliente + Admin | Frontend + Backend |
| 22 | Substituição de produtos | Cliente + Admin | Frontend + Backend |
| 23 | Busca, filtros e ordenação aprimorados | Cliente | Frontend + Backend |

---

## Fase 3 — Evolução, gestão e qualidade profissional

### Objetivo

Usar o projeto já funcional para estudar gestão do negócio e preocupações que aparecem em aplicações profissionais.

| Ordem | Entrega | Visão | Responsável principal |
|---:|---|---|---|
| 24 | Dashboard gerencial do proprietário | Admin / Proprietário | Frontend + Backend |
| 25 | Testes unitários ampliados | Compartilhado | Frontend + Backend |
| 26 | Testes de integração | Compartilhado | Frontend + Backend |
| 27 | Testes E2E do fluxo de compra | Compartilhado | Frontend + Backend |
| 28 | Acessibilidade | Cliente + Admin | Frontend |
| 29 | Performance | Cliente | Frontend + Backend |
| 30 | Segurança e permissões | Cliente + Admin | Frontend + Backend |
| 31 | Observabilidade básica | Interno | Backend |
| 32 | CI/CD | Infraestrutura | Frontend + Backend |
| 33 | Deploy e ambientes | Infraestrutura | Frontend + Backend |

### Dashboard gerencial — direção inicial

O dashboard não faz parte do primeiro fluxo de compra. Ele será construído quando o sistema já possuir dados suficientes para gerar informações úteis.

Indicadores candidatos para estudo futuro:

- vendas do dia, semana e mês;
- comparação de vendas com períodos anteriores;
- quantidade de pedidos;
- ticket médio;
- produtos mais vendidos;
- produtos com baixo estoque;
- pedidos por status;
- evolução de faturamento ao longo do tempo.

A lista definitiva de indicadores será decidida somente quando esta etapa for estudada.

---

# 7. Fluxo geral do sistema

```text
ADMIN / MERCADO

Categoria
   ↓
Produto
   ↓
Preço
   ↓
Estoque
   ↓
BACKEND / API
   ↓
CLIENTE
Home / Catálogo
   ↓
Produto
   ↓
Carrinho
   ↓
Endereço / Entrega
   ↓
Checkout
   ↓
Pagamento
   ↓
Pedido
   ↓
ADMIN / MERCADO
Separação / Atualização do pedido
   ↓
DADOS ACUMULADOS
   ↓
DASHBOARD GERENCIAL
Indicadores para o proprietário
```

Esse fluxo é importante porque determina boa parte da ordem de desenvolvimento. Antes de a loja do cliente exibir dados reais, precisa existir uma maneira de cadastrá-los e disponibilizá-los pela API. Da mesma forma, o dashboard só passa a fazer sentido depois que pedidos, vendas e estoque já geram dados reais ou simulados suficientes para análise.

---

# 8. Estratégia de execução

O projeto será construído em **fatias funcionais**, e não com todo o Frontend primeiro e todo o Backend depois.

Exemplo:

```text
Produto

Admin Frontend → formulário e tela de produtos
Backend → modelo, banco, regras e API
Cliente Frontend → catálogo e detalhe
Integração → teste do fluxo completo
```

Somente depois de uma fatia estar funcionando de ponta a ponta o projeto avança para dependências posteriores.

---

# 9. Documentação de aprendizagem e execução

Este documento descreve **o projeto e seu escopo**.

Cada etapa terá um documento próprio explicando **como estudá-la, decidir e executá-la**.

Esses documentos deverão seguir, sempre que fizer sentido, a estrutura:

```text
Entender
   ↓
Conhecer alternativas
   ↓
Comparar
   ↓
Tomar decisões
   ↓
Registrar decisões
   ↓
Implementar
   ↓
Validar
```

O primeiro guia é:

- [01 — Fundação do projeto](./fase-1/01-fundacao-do-projeto.md)

Os próximos guias serão criados conforme o projeto avançar, evitando definir prematuramente decisões que dependem de etapas anteriores.

---

# 10. O que não faz parte do escopo inicial

Para manter o projeto adequado ao objetivo de estudo, inicialmente não serão tratados como prioridade:

- marketplace com vários vendedores;
- sistema de reputação de vendedores;
- programa complexo de fidelidade;
- recomendação por inteligência artificial;
- múltiplos centros de distribuição;
- arquitetura de microsserviços;
- filas e arquitetura distribuída avançada;
- busca com Elasticsearch/OpenSearch;
- antifraude avançado;
- ERP completo;
- operação fiscal complexa;
- escala de grandes varejistas.

Esses tópicos poderão ser estudados futuramente se surgirem como uma evolução natural do projeto.

---

## Resumo

O projeto será um **mercado online com 19 módulos funcionais**, dividido em três níveis de evolução:

1. **Mercado funcional** — construir a compra de ponta a ponta;
2. **Operação realista** — aproximar o sistema do cotidiano de um mercado;
3. **Gestão e qualidade profissional** — estudar dashboard gerencial, testes, segurança, performance, CI/CD e operação.

A prioridade não será quantidade de funcionalidades. Será compreender, implementar e integrar corretamente cada parte do sistema.