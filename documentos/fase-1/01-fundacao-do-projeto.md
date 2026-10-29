# Ordem 1 — Fundação do Projeto

## Propósito deste documento

Este documento é um **guia de aprendizagem e execução** para a primeira etapa do projeto de **mercado online**.

O objetivo não é entregar uma arquitetura pronta para ser copiada. A proposta é orientar o raciocínio necessário para que a pessoa responsável pelo Frontend consiga:

1. entender o problema;
2. conhecer as principais opções;
3. comparar vantagens e desvantagens;
4. tomar decisões conscientes;
5. registrar as decisões;
6. implementar;
7. validar se a fundação ficou adequada antes de avançar.

> Regra desta etapa: **entender → comparar → decidir → registrar → implementar → validar**.

---

# 1. Resultado esperado da Ordem 1

Ao terminar esta etapa, o Frontend ainda não precisa ter o mercado online funcional.

O que precisa existir é uma base técnica suficientemente clara para que as próximas funcionalidades possam ser construídas sem reorganizar o projeto a cada nova tela.

Ao final, deve estar definido e funcionando:

- aplicação Frontend criada e executando localmente;
- **Next.js utilizado como framework principal do Frontend**;
- versão do Next.js registrada;
- estratégia de organização de pastas;
- separação entre área do Cliente e área Administrativa;
- estratégia de rotas;
- layouts principais;
- estratégia visual inicial;
- decisão sobre biblioteca de componentes, se for adotada;
- componentes compartilhados essenciais;
- convenções de código;
- configuração de ambientes;
- estratégia inicial de comunicação com o Backend;
- regras mínimas de qualidade;
- critérios objetivos para considerar a fundação concluída.

---

# 2. Decisão já tomada: Next.js

A tecnologia principal do Frontend será **Next.js**.

Essa escolha faz parte do objetivo de aprendizagem do projeto. Portanto, este documento não tratará Next.js como uma opção a ser comparada com outros frameworks antes da implementação.

O que ainda precisa ser estudado dentro do próprio Next.js:

- versão que será utilizada;
- estrutura recomendada pelo framework;
- sistema de roteamento;
- layouts;
- renderização no servidor e no cliente;
- Server Components e Client Components;
- carregamento de dados;
- tratamento de erros;
- variáveis de ambiente;
- convenções de projeto.

## Registro

```text
Framework: Next.js
Versão: a definir no início da implementação
Motivo principal: aprendizado prático de Next.js em um projeto realista
Documentação oficial: registrar durante o estudo
```

### Critério de validação

Você deve conseguir explicar quais responsabilidades o Next.js assume no projeto e como sua estrutura influencia rotas, layouts e componentes.

---

# 3. Arquitetura de pastas

## Objetivo

Decidir como o código será organizado para que seja fácil localizar, evoluir e manter as funcionalidades.

A estrutura não deve ser copiada de um exemplo sem entender o motivo.

## Estratégias a estudar

### Opção A — Organização por tipo técnico

Exemplo conceitual:

```text
components/
services/
hooks/
types/
utils/
```

Arquivos semelhantes ficam juntos pelo tipo técnico.

### Opção B — Organização por feature

Exemplo conceitual:

```text
features/
  products/
  cart/
  checkout/
```

Tudo que pertence a uma funcionalidade fica próximo.

### Opção C — Organização híbrida

Combina a estrutura nativa do Next.js com organização por domínio e recursos compartilhados.

Exemplo apenas para estudo:

```text
src/
├── app/
├── features/
├── components/
├── services/
├── types/
└── lib/
```

> Esta estrutura é apenas um exemplo. A organização definitiva será decidida depois do estudo das convenções do Next.js.

## Decisões que precisam ser tomadas

```text
Estratégia escolhida:
Por que ela faz sentido para o mercado online:
Quais alternativas foram descartadas:
Por que foram descartadas:
Regra para algo ser compartilhado:
```

## Validação de aprendizagem

Você deve conseguir responder:

- qual diferença existe entre organização por tipo e por feature;
- como o diretório `app` do Next.js influencia a arquitetura;
- quando algo pertence a uma feature;
- quando algo realmente deve ser compartilhado.

---

# 4. Separação Cliente e Admin

O mercado online terá dois grandes contextos visuais.

## Cliente

Área utilizada por quem compra.

Exemplos futuros:

- Home;
- catálogo;
- categorias;
- produto;
- busca;
- carrinho;
- checkout;
- conta;
- pedidos.

## Admin

Área utilizada pela operação e, futuramente, pelo proprietário do mercado.

Exemplos futuros:

- produtos;
- categorias;
- preços;
- estoque;
- pedidos;
- clientes;
- promoções;
- dashboard gerencial.

## Decisão arquitetural a estudar

Cliente e Admin poderão ficar:

1. na mesma aplicação Next.js, separados por rotas e layouts; ou
2. em aplicações diferentes.

Para o projeto de estudo, essa escolha ainda deve ser analisada antes da implementação definitiva.

## Registro

```text
Estratégia Cliente/Admin:
Motivo:
Consequências da decisão:
```

---

# 5. Rotas

## Objetivo

Entender como o Next.js organiza navegação e URLs antes de criar as telas.

## O que estudar

- App Router;
- segmentos de rota;
- rotas dinâmicas;
- route groups;
- layouts aninhados;
- páginas de erro;
- página 404;
- rotas públicas;
- rotas protegidas futuramente.

## Mapa inicial candidato

### Cliente

```text
/
/produtos
/produtos/[id]
```

### Admin

```text
/admin
/admin/produtos
/admin/produtos/novo
/admin/produtos/[id]/editar
```

Essas rotas servem como ponto de estudo e podem ser alteradas quando a estratégia de arquitetura for decidida.

## Validação

Você deve conseguir explicar:

- como uma pasta dentro de `app` pode gerar uma rota;
- como funciona uma rota dinâmica no Next.js;
- como Cliente e Admin podem possuir layouts diferentes;
- por que não é necessário criar todas as rotas futuras agora.

---

# 6. Layout base

## O que é

Layout base é a estrutura visual persistente que envolve diferentes páginas.

No mercado online, provavelmente existirão pelo menos dois contextos:

### Layout do Cliente

Pode conter futuramente:

```text
Header
Navegação
Conteúdo da página
Footer
```

### Layout do Admin

Pode conter futuramente:

```text
Header administrativo
Sidebar ou navegação administrativa
Conteúdo da página
```

## O que estudar no Next.js

- `layout.tsx`;
- layouts aninhados;
- composição;
- route groups;
- diferenças entre layout e página;
- persistência de elementos entre navegações.

## Decisão a registrar

```text
Quais layouts existirão inicialmente:
O que pertence ao layout do Cliente:
O que pertence ao layout do Admin:
O que não deve ficar dentro dos layouts:
```

---

# 7. Estratégia visual e biblioteca de componentes

A biblioteca de componentes **ainda não está decidida**.

Antes de escolher, deve existir uma etapa de estudo.

## O que comparar

- compatibilidade com Next.js;
- acessibilidade;
- facilidade de customização;
- qualidade da documentação;
- quantidade de abstração;
- impacto no aprendizado;
- manutenção;
- integração com a estratégia de estilos escolhida.

## Exemplos de alternativas para pesquisar

- shadcn/ui;
- Material UI;
- Chakra UI;
- criação de componentes próprios quando fizer sentido.

Esses nomes são apenas candidatas para comparação. **Nenhuma delas está definida como escolha do projeto neste momento.**

## Outras decisões futuras

Também deverão ser estudadas antes de serem registradas como padrão:

- Tailwind CSS ou outra estratégia de estilos;
- tokens visuais;
- tema;
- tipografia;
- cores;
- espaçamentos;
- breakpoints.

## Registro

```text
Biblioteca de componentes escolhida:
Alternativas analisadas:
Motivo da escolha:
Estratégia de estilos:
Motivo:
```

---

# 8. Componentes compartilhados iniciais

Não criar dezenas de componentes antecipadamente.

Criar apenas os necessários para validar a fundação e as primeiras funcionalidades.

Possíveis candidatos futuros:

```text
Button
Input
Select
Container
Loading
ErrorMessage
EmptyState
Modal
Header
Footer
Sidebar
```

A lista definitiva dependerá da biblioteca de componentes e da arquitetura escolhidas.

## Perguntas antes de compartilhar um componente

- ele será usado em mais de um contexto?
- existe comportamento ou aparência que precisa permanecer consistente?
- ele é realmente genérico ou pertence a uma feature específica?

---

# 9. Convenções do projeto

Definir convenções para evitar que cada funcionalidade introduza uma forma diferente de escrever código.

Itens a estudar e decidir:

- nomes de arquivos;
- nomes de componentes;
- organização de imports;
- aliases;
- tipagem;
- tratamento de erros;
- loading states;
- branches;
- commits;
- pull requests;
- lint;
- formatter.

O próprio ecossistema do Next.js deve ser considerado antes de escolher ferramentas adicionais.

---

# 10. Configuração de ambientes

## O que estudar

- variáveis de ambiente no Next.js;
- diferença entre variáveis públicas e privadas;
- `.env`;
- configuração de desenvolvimento e produção;
- secrets;
- valores que nunca devem ser commitados.

## Possíveis variáveis futuras

```text
API_URL
APP_ENV
```

Os nomes definitivos serão decididos quando a integração com o Backend for estudada.

---

# 11. Comunicação com o Backend

O Backend ainda não precisa estar tecnicamente definido nesta Ordem 1.

O importante nesta etapa é compreender como o Frontend Next.js consumirá uma API externa futuramente.

## O que estudar

- HTTP;
- GET, POST, PUT/PATCH e DELETE;
- request e response;
- status codes;
- DTOs;
- tratamento de erros;
- carregamento de dados no Next.js;
- comunicação feita no servidor ou no cliente;
- caching e revalidação em nível introdutório.

## Decisões que ficam para depois

- tecnologia definitiva do Backend;
- estrutura da API;
- camada de services;
- cliente HTTP;
- autenticação;
- política de cache;
- contratos definitivos.

---

# 12. Responsividade

A fundação deve definir como o projeto pensará diferentes tamanhos de tela, mas não precisa entregar todas as páginas prontas.

## O que estudar

- mobile first;
- desktop first;
- layouts fluidos;
- grid e flexbox;
- breakpoints;
- imagens responsivas;
- componente `Image` do Next.js.

## Registro

```text
Estratégia responsiva:
Breakpoints:
Largura máxima de conteúdo:
Comportamento esperado da área Cliente:
Comportamento esperado da área Admin:
```

---

# 13. Acessibilidade mínima

Acessibilidade deve ser considerada desde os componentes básicos.

Estudar:

- HTML semântico;
- navegação por teclado;
- foco visível;
- labels;
- contraste;
- diferença entre botão e link;
- landmarks.

A escolha futura da biblioteca de componentes também deverá considerar acessibilidade.

---

# 14. Testes da fundação

A estratégia de testes ainda será definida, mas é necessário compreender os níveis principais:

- teste unitário;
- teste de componente;
- integração;
- E2E.

Nesta etapa, o mínimo a validar é:

- aplicação Next.js inicia;
- build funciona;
- rotas base funcionam;
- layouts escolhidos funcionam;
- estrutura de pastas está coerente com a decisão tomada.

---

# 15. Plano de execução sugerido

## Bloco A — Next.js

- [ ] Estudar a estrutura básica atual do Next.js.
- [ ] Escolher a versão a utilizar.
- [ ] Criar a aplicação.
- [ ] Executar localmente.
- [ ] Validar o build inicial.

## Bloco B — Arquitetura

- [ ] Estudar as estratégias de organização de pastas.
- [ ] Entender as convenções do `app`.
- [ ] Escolher e registrar a arquitetura.
- [ ] Decidir a separação Cliente/Admin.

## Bloco C — Navegação e layouts

- [ ] Estudar App Router.
- [ ] Criar o mapa inicial de rotas.
- [ ] Estudar `layout.tsx` e layouts aninhados.
- [ ] Criar apenas a estrutura necessária para validar Cliente e Admin.

## Bloco D — Base visual

- [ ] Comparar alternativas de biblioteca de componentes.
- [ ] Comparar estratégias de estilos.
- [ ] Registrar as escolhas.
- [ ] Criar somente os componentes essenciais para a próxima etapa.

## Bloco E — Infraestrutura de Frontend

- [ ] Definir convenções básicas.
- [ ] Estudar variáveis de ambiente.
- [ ] Preparar a aplicação para futura comunicação com API.
- [ ] Configurar lint/formatter conforme a decisão tomada.

## Bloco F — Validação

- [ ] Rodar o projeto.
- [ ] Executar build.
- [ ] Navegar pelas rotas base.
- [ ] Validar os layouts.
- [ ] Revisar as decisões registradas.

---

# 16. Critérios de aceite da Ordem 1

A Ordem 1 estará concluída quando:

- [ ] Next.js estiver criado e executando localmente;
- [ ] a versão utilizada estiver registrada;
- [ ] a arquitetura de pastas tiver sido estudada, escolhida e justificada;
- [ ] Cliente e Admin possuírem separação arquitetural clara;
- [ ] o mapa inicial de rotas estiver documentado;
- [ ] a estratégia de layouts estiver definida;
- [ ] a biblioteca de componentes tiver sido estudada e decidida, caso seja adotada;
- [ ] a estratégia de estilos tiver sido estudada e decidida;
- [ ] as convenções iniciais estiverem registradas;
- [ ] a estratégia de ambientes estiver compreendida;
- [ ] a futura comunicação com Backend estiver conceitualmente definida;
- [ ] o build passar;
- [ ] a próxima funcionalidade puder ser iniciada sem reorganização estrutural relevante.

---

# 17. Perguntas de revisão antes de avançar

Antes da próxima ordem, você deve conseguir responder:

1. Por que o Next.js foi escolhido para este projeto?
2. Como o App Router organiza rotas?
3. Qual arquitetura de pastas foi escolhida e por quê?
4. Como Cliente e Admin serão separados?
5. Qual diferença existe entre página e layout no Next.js?
6. Como funciona uma rota dinâmica?
7. Qual biblioteca de componentes foi escolhida, se houver, e por quê?
8. Qual estratégia de estilos foi escolhida e por quê?
9. O que deve ser compartilhado entre funcionalidades?
10. Como o Frontend futuramente consumirá dados do Backend?
11. Como serão tratadas variáveis de ambiente?
12. O que precisa estar funcionando para considerar a fundação pronta?

---

# 18. Registro de decisões

Preencher durante o estudo e a implementação.

| Decisão | Opções consideradas | Escolha | Motivo | Data |
|---|---|---|---|---|
| Framework | Next.js | **Next.js** | Aprendizado prático no projeto | 29/10/2026 |
| Versão do Next.js |  |  |  |  |
| Arquitetura de pastas |  |  |  |  |
| Organização Cliente/Admin |  |  |  |  |
| Estratégia de rotas |  |  |  |  |
| Layouts |  |  |  |  |
| Biblioteca de componentes |  |  |  |  |
| Estratégia de estilos |  |  |  |  |
| Componentes compartilhados |  |  |  |  |
| Ambientes |  |  |  |  |
| Comunicação com API |  |  |  |  |
| Estratégia responsiva |  |  |  |  |

---

## Próxima etapa

Depois que esta fundação estiver compreendida, implementada e validada, seguir para a próxima ordem definida em `documentos/estrutura-do-projeto.md`.