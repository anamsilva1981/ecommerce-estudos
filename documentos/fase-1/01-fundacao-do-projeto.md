# Ordem 1 — Fundação do Projeto

## Propósito deste documento

Este documento é um **guia de aprendizagem e execução** para a primeira etapa do e-commerce.

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

Ao terminar esta etapa, o Frontend ainda não precisa ter o e-commerce funcional.

O que precisa existir é uma base técnica suficientemente clara para que as próximas funcionalidades possam ser construídas sem reorganizar o projeto a cada nova tela.

Ao final, deve estar definido e funcionando:

- aplicação Frontend criada e executando localmente;
- estratégia de organização de pastas;
- separação entre área do Cliente e área Administrativa;
- estratégia de rotas;
- layouts principais;
- tema e tokens visuais iniciais;
- Design System inicial;
- componentes compartilhados essenciais;
- convenções de código;
- configuração de ambientes;
- estratégia inicial de comunicação com a API;
- regras mínimas de qualidade;
- critérios objetivos para considerar a fundação concluída.

---

# 2. Antes de começar: decisões de contexto

Antes de criar pastas ou componentes, registrar as decisões básicas do projeto.

## 2.1 Framework e versão

### Pergunta que precisa ser respondida

Qual tecnologia será usada no Frontend e qual versão?

### O que estudar

- diferença entre framework e biblioteca;
- ciclo de vida e suporte de versões;
- documentação oficial da tecnologia escolhida;
- convenções recomendadas pelo próprio framework.

### Decisão a registrar

```text
Framework:
Versão:
Motivo da escolha:
Documentação oficial:
```

### Critério de validação

Você deve conseguir explicar por que essa tecnologia foi escolhida sem responder apenas “porque eu já conheço”.

---

# 3. Arquitetura de pastas

## Objetivo

Decidir como o código será organizado para que seja fácil localizar, evoluir e manter as funcionalidades.

Não comece criando pastas aleatoriamente. Primeiro compare estratégias.

## 3.1 Opção A — Organização por tipo técnico

Exemplo:

```text
src/
├── components/
├── pages/
├── services/
├── models/
├── hooks/
└── utils/
```

### Característica

Arquivos semelhantes ficam juntos pelo tipo técnico.

### Vantagens

- simples de entender em projetos pequenos;
- estrutura inicial familiar;
- fácil localizar “todos os services” ou “todos os components”.

### Desvantagens

- conforme o sistema cresce, uma única funcionalidade fica espalhada em muitas pastas;
- aumenta o custo para entender tudo que pertence a um domínio;
- pode gerar pastas enormes.

### Pergunta para reflexão

Se você precisar alterar completamente a funcionalidade de produtos, quantas pastas diferentes terá que abrir?

---

## 3.2 Opção B — Organização por feature

Exemplo:

```text
src/
├── features/
│   ├── products/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   └── models/
│   ├── cart/
│   └── checkout/
```

### Característica

Tudo que pertence à mesma funcionalidade fica próximo.

### Vantagens

- boa escalabilidade organizacional;
- facilita manutenção por funcionalidade;
- reduz acoplamento entre áreas;
- torna mais claro o que pertence a cada domínio.

### Desvantagens

- exige critérios claros para decidir o que é compartilhado;
- pode gerar duplicação se a equipe mover cedo demais coisas reutilizáveis para dentro de features.

### Pergunta para reflexão

Um `ProductCard` pertence exclusivamente à feature de produtos ou será reutilizado na Home, busca e favoritos?

---

## 3.3 Opção C — Organização híbrida

Exemplo:

```text
src/
├── app/
├── store/
│   ├── home/
│   ├── catalog/
│   ├── product/
│   ├── cart/
│   └── checkout/
├── admin/
│   ├── dashboard/
│   ├── products/
│   ├── categories/
│   └── orders/
├── shared/
│   ├── components/
│   ├── services/
│   ├── models/
│   └── utils/
└── assets/
```

### Característica

O projeto é separado por grandes contextos de negócio e mantém uma área explícita para recursos realmente compartilhados.

### Vantagens

- deixa Cliente e Admin claramente separados;
- permite organizar funcionalidades internamente por domínio;
- facilita crescimento sem concentrar tudo em uma pasta global;
- combina organização de negócio com reutilização.

### Desvantagens

- exige disciplina para não transformar `shared` em depósito de arquivos;
- algumas decisões de fronteira podem ser subjetivas.

---

## 3.4 Decisão obrigatória

Antes de implementar, preencher:

```text
Estratégia escolhida:

Por que ela faz sentido para este e-commerce:

Quais alternativas foram descartadas:

Por que foram descartadas:

Regra para algo entrar em shared:
```

## 3.5 Validação de aprendizagem

Você deve conseguir responder:

- Qual diferença existe entre organização por tipo e por feature?
- Por que uma arquitetura pode funcionar bem em um projeto pequeno e mal em um projeto grande?
- O que caracteriza algo como compartilhado?
- Em qual pasta entraria uma nova funcionalidade de favoritos?
- Em qual pasta entraria um botão reutilizado pelo Cliente e pelo Admin?

---

# 4. Separação das duas frentes do Frontend

O e-commerce terá pelo menos dois grandes contextos visuais.

## Store / Cliente

É a parte utilizada pelo comprador.

Exemplos futuros:

- Home;
- catálogo;
- produto;
- busca;
- carrinho;
- checkout;
- minha conta;
- pedidos.

## Admin

É a parte utilizada pela operação da loja.

Exemplos futuros:

- dashboard;
- categorias;
- marcas;
- produtos;
- estoque;
- pedidos;
- clientes;
- promoções.

## Pergunta de arquitetura

Cliente e Admin ficarão:

1. no mesmo projeto Frontend, separados por módulos/áreas; ou
2. em aplicações Frontend diferentes?

## O que estudar antes de decidir

- SPA;
- modularização;
- múltiplas aplicações;
- compartilhamento de código;
- deploy independente;
- complexidade operacional.

## Decisão a registrar

```text
Estratégia Cliente/Admin:

Motivo:

Consequências da decisão:
```

> Para esta etapa de estudos, a decisão deve privilegiar clareza de arquitetura e aprendizagem, não complexidade de infraestrutura sem necessidade.

---

# 5. Rotas

## Objetivo

Definir como o usuário navegará pela aplicação e como Cliente e Admin serão separados.

Não é necessário implementar todas as rotas futuras agora.

Primeiro deve existir um **mapa de rotas**.

## 5.1 Conceitos a estudar

- roteamento client-side;
- rota estática;
- rota dinâmica;
- parâmetros de rota;
- query parameters;
- rotas aninhadas;
- lazy loading;
- rotas públicas;
- rotas privadas/protegidas;
- fallback / 404.

## 5.2 Rotas iniciais candidatas

### Cliente

```text
/
/produtos
/produtos/:id
```

### Admin

```text
/admin
/admin/produtos
/admin/produtos/novo
/admin/produtos/:id/editar
```

Essas rotas representam a estrutura inicial, mas algumas telas só serão implementadas nas ordens seguintes.

## 5.3 Rotas futuras — não implementar agora

Exemplos:

```text
/login
/cadastro
/carrinho
/checkout
/minha-conta
/meus-pedidos
/admin/pedidos
/admin/clientes
```

## 5.4 Decisões que precisam ser tomadas

```text
Padrão de URL do Cliente:
Padrão de URL do Admin:
Convenção para parâmetros dinâmicos:
Estratégia para 404:
Estratégia futura para rotas protegidas:
Será usado lazy loading? Onde?
```

## 5.5 Validação de aprendizagem

Você deve conseguir explicar:

- por que `/produtos/:id` é diferente de `/produtos`;
- quando usar query parameter e quando usar parâmetro de rota;
- por que uma rota administrativa precisará futuramente de proteção;
- por que não é necessário criar todas as rotas do projeto na Ordem 1.

---

# 6. Layout base

## O que significa “layout base”

Layout base é a estrutura visual persistente que envolve o conteúdo das páginas.

Ele evita repetir Header, Navbar, Footer ou Sidebar em cada tela.

## 6.1 StoreLayout

Exemplo conceitual:

```text
┌──────────────────────────────────┐
│ Header                           │
├──────────────────────────────────┤
│ Navbar                           │
├──────────────────────────────────┤
│                                  │
│ Conteúdo da rota atual           │
│                                  │
├──────────────────────────────────┤
│ Footer                           │
└──────────────────────────────────┘
```

O conteúdo central muda conforme a rota.

## 6.2 AdminLayout

Exemplo conceitual:

```text
┌──────────────┬───────────────────────────┐
│              │ Header administrativo    │
│ Sidebar      ├───────────────────────────┤
│              │                           │
│              │ Conteúdo da rota atual    │
│              │                           │
└──────────────┴───────────────────────────┘
```

## 6.3 O que estudar

- composição de componentes;
- layouts aninhados;
- outlet/router outlet equivalente do framework;
- responsabilidade de componentes estruturais;
- responsividade de layout.

## 6.4 Decisões a registrar

```text
Layouts iniciais:

O que pertence ao StoreLayout:

O que pertence ao AdminLayout:

O que não deve ficar dentro dos layouts:
```

## 6.5 Validação

Se Header ou Footer mudar, você deve conseguir alterar uma única implementação e refletir a mudança em todas as páginas que usam aquele layout.

---

# 7. Tema e Design System inicial

## Objetivo

Criar regras visuais reutilizáveis antes de cada tela inventar sua própria solução.

Nesta fase não é necessário construir um Design System completo.

## 7.1 Primeiro: entender tokens

Estudar:

- design tokens;
- cores semânticas;
- escala tipográfica;
- espaçamento;
- border radius;
- breakpoints;
- estados de interação;
- contraste;
- responsividade.

## 7.2 Tokens candidatos

### Cores

```text
primary
secondary
background
surface
text-primary
text-secondary
success
warning
error
```

### Tipografia

```text
font-family
font-size-xs
font-size-sm
font-size-md
font-size-lg
font-size-xl
font-weight-regular
font-weight-medium
font-weight-bold
```

### Espaçamento

Definir uma escala coerente, em vez de usar valores aleatórios em cada componente.

### Outros

```text
border-radius
shadow
breakpoints
z-index
```

## 7.3 Decisão a registrar

```text
Estratégia de tema:

Onde os tokens ficarão:

Como serão nomeados:

Como Cliente e Admin compartilharão tokens:
```

---

# 8. Componentes compartilhados iniciais

## Regra principal

Não construir dezenas de componentes “porque talvez sejam usados”.

Criar apenas o que já possui justificativa arquitetural.

## Candidatos iniciais

```text
Button
Input
Select
Container
Loading
ErrorMessage
EmptyState
Modal
```

Elementos de layout:

```text
Header
Navbar
Footer
Sidebar
```

## Perguntas antes de criar um componente compartilhado

- Ele será usado em mais de um contexto?
- Existe uma regra visual ou comportamental que precisa permanecer consistente?
- É realmente um componente genérico ou pertence a uma feature?

## O que estudar

- componentização;
- composição;
- props/inputs;
- responsabilidade única;
- controlled/uncontrolled components, se aplicável;
- acessibilidade de componentes.

---

# 9. Convenções do projeto

## Objetivo

Evitar que cada nova funcionalidade introduza uma forma diferente de escrever e organizar código.

## Decisões iniciais

Definir convenções para:

- nomes de arquivos;
- nomes de componentes;
- nomes de services;
- organização de imports;
- aliases de importação;
- tipagem;
- tratamento de erros;
- estados de loading;
- comentários;
- branches;
- commits;
- pull requests.

## Ferramentas candidatas

- ESLint;
- Prettier;
- formatter/linter específico do framework, se houver;
- hooks de Git, se fizer sentido.

## Validação

O projeto deve conseguir detectar automaticamente pelo menos parte dos desvios de padrão.

---

# 10. Configuração de ambientes

## Objetivo

Permitir que o mesmo código se conecte a configurações diferentes sem alterar valores manualmente no código-fonte.

## Ambientes candidatos

```text
development
staging / homologation
production
```

## Variáveis iniciais candidatas

```text
API_URL
APP_ENV
```

## O que estudar

- environment variables;
- build-time versus runtime configuration;
- `.env`;
- secrets;
- por que credenciais não devem ser commitadas.

## Decisões a registrar

```text
Ambientes existentes inicialmente:

Convenção dos arquivos de ambiente:

Quais variáveis o Frontend precisa:

Quais valores jamais podem ir para o repositório:
```

---

# 11. Comunicação com o Backend

Mesmo que a API ainda não esteja pronta, a aplicação deve ter uma estratégia definida para comunicação HTTP.

## O que estudar

- HTTP;
- métodos GET, POST, PUT/PATCH e DELETE;
- status codes;
- request/response;
- DTOs;
- tratamento de erros;
- interceptors/middlewares, quando aplicável;
- timeout;
- loading state.

## Possível separação

```text
api/
services/
models/
```

## Decisões a tomar

- componentes podem chamar HTTP diretamente?
- haverá uma camada de services?
- onde ficarão os tipos de request e response?
- como erros serão normalizados?
- como a URL base da API será configurada?

## Regra candidata

> Componentes de interface não devem conhecer detalhes de transporte HTTP além do necessário. A comunicação com a API deve ficar encapsulada em uma camada apropriada.

Essa regra deve ser estudada e validada antes de ser adotada definitivamente.

---

# 12. Responsividade inicial

## Objetivo

A fundação não precisa entregar todas as telas responsivas, mas deve definir como o projeto tratará diferentes tamanhos de viewport.

## O que estudar

- mobile first;
- desktop first;
- breakpoints;
- fluid layouts;
- container width;
- grid/flex;
- imagens responsivas.

## Decisões a registrar

```text
Estratégia responsiva:
Breakpoints iniciais:
Largura máxima de conteúdo:
Comportamento esperado do StoreLayout no mobile:
Comportamento esperado do AdminLayout no mobile:
```

---

# 13. Acessibilidade mínima da fundação

Acessibilidade não deve entrar apenas no final do projeto.

## O que estudar nesta etapa

- HTML semântico;
- navegação por teclado;
- foco visível;
- labels de formulário;
- contraste;
- uso correto de button e link;
- landmarks básicos.

## Regra

Componentes básicos criados na fundação devem nascer com comportamento acessível, para não multiplicar problemas nas telas futuras.

---

# 14. Testes da fundação

Não é necessário criar uma suíte completa nesta etapa, mas a estratégia inicial deve ser compreendida.

## O que estudar

- teste unitário;
- teste de componente;
- teste de integração;
- E2E;
- diferença entre testar comportamento e implementação.

## O que pode ser validado agora

- aplicação inicia;
- rotas base carregam;
- StoreLayout renderiza corretamente;
- AdminLayout renderiza corretamente;
- componentes básicos possuem comportamento esperado;
- página 404 funciona, se implementada nesta etapa.

---

# 15. Plano de execução sugerido

Esta é a ordem prática recomendada **depois de estudar e registrar as decisões anteriores**.

## Bloco A — Inicialização

- [ ] Criar o projeto Frontend.
- [ ] Confirmar versão do framework e runtime.
- [ ] Configurar TypeScript, se aplicável.
- [ ] Garantir que aplicação executa localmente.
- [ ] Garantir que o build inicial funciona.

## Bloco B — Arquitetura

- [ ] Escolher estratégia de organização de pastas.
- [ ] Registrar justificativa.
- [ ] Criar estrutura mínima de pastas.
- [ ] Definir separação Cliente/Admin.

## Bloco C — Navegação

- [ ] Definir mapa inicial de rotas.
- [ ] Criar roteamento base.
- [ ] Criar StoreLayout.
- [ ] Criar AdminLayout.
- [ ] Criar páginas placeholder somente quando forem necessárias para validar navegação.

## Bloco D — Base visual

- [ ] Definir tokens iniciais.
- [ ] Configurar tema.
- [ ] Criar componentes estruturais necessários.
- [ ] Criar apenas os componentes compartilhados realmente justificáveis.

## Bloco E — Infraestrutura de Frontend

- [ ] Configurar ambientes.
- [ ] Configurar URL base da API.
- [ ] Definir camada de services/API.
- [ ] Configurar aliases/imports, se adotados.
- [ ] Configurar lint/formatter.

## Bloco F — Validação

- [ ] Executar lint.
- [ ] Executar testes existentes.
- [ ] Executar build.
- [ ] Navegar pelas rotas base.
- [ ] Validar StoreLayout.
- [ ] Validar AdminLayout.
- [ ] Validar comportamento inicial em desktop e mobile.

---

# 16. Critérios de aceite da Ordem 1

A Ordem 1 pode ser considerada concluída quando:

- [ ] A aplicação Frontend executa localmente sem erro.
- [ ] A estratégia de arquitetura de pastas foi estudada, escolhida e justificada.
- [ ] Cliente e Admin possuem separação arquitetural clara.
- [ ] O mapa inicial de rotas está documentado.
- [ ] As rotas necessárias para validar a arquitetura funcionam.
- [ ] StoreLayout existe e funciona.
- [ ] AdminLayout existe e funciona.
- [ ] Tema/tokens iniciais estão definidos.
- [ ] A regra para componentes compartilhados está definida.
- [ ] Ambientes e variáveis iniciais estão configurados.
- [ ] A estratégia de comunicação com o Backend está documentada.
- [ ] Lint/formatter estão configurados.
- [ ] Build passa.
- [ ] A arquitetura consegue receber a próxima feature sem reorganização estrutural relevante.

---

# 17. Perguntas de revisão antes de avançar

Antes de iniciar a Ordem 2, responda sem consultar este documento:

1. Por que escolhemos esta arquitetura de pastas?
2. Qual seria a principal alternativa e por que não a escolhemos?
3. Onde entra uma nova página do Cliente?
4. Onde entra uma nova página do Admin?
5. Como decidir se um componente deve ir para `shared`?
6. Qual diferença existe entre uma rota estática, dinâmica e uma query parameter?
7. O que o StoreLayout resolve?
8. O que o AdminLayout resolve?
9. Por que não criamos antecipadamente todos os componentes do Design System?
10. Como o Frontend descobrirá a URL da API em cada ambiente?
11. Onde deve ficar a responsabilidade de comunicação HTTP?
12. O que precisa acontecer para considerarmos esta fundação concluída?

Se essas respostas estiverem claras e a implementação atender aos critérios de aceite, a fundação está pronta para sustentar as próximas etapas.

---

# 18. Registro de decisões

Preencher durante o desenvolvimento.

| Decisão | Opções consideradas | Escolha | Motivo | Data |
|---|---|---|---|---|
| Framework e versão |  |  |  |  |
| Arquitetura de pastas |  |  |  |  |
| Organização Cliente/Admin |  |  |  |  |
| Estratégia de rotas |  |  |  |  |
| Layouts |  |  |  |  |
| Estratégia de tema |  |  |  |  |
| Componentes compartilhados |  |  |  |  |
| Ambientes |  |  |  |  |
| Camada de API/services |  |  |  |  |
| Estratégia responsiva |  |  |  |  |

---

## Próxima etapa

Depois que esta fundação estiver compreendida, implementada e validada, seguir para a próxima ordem definida em `documentos/estrutura-do-projeto.md`.
