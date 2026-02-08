# Client Dashboard — Overview (Wireframe)

## Objetivo da Tela
Fornecer uma visão rápida e acionável do uso da plataforma pela empresa (cliente B2B).

## Usuários
- Owner/Admin da Empresa
- Operador da Empresa

## Blocos da Tela (Hierarquia Visual)
1. Header
   - Nome da empresa
   - Saldo de créditos atual
   - CTA: Comprar créditos
2. Cards de Status
   - Card: Jobs em andamento
   - Card: Jobs finalizados (últimos 7 dias)
   - Card: Uso do mês (volume processado + créditos consumidos)
3. Lista de Projetos/Lotes Recentes
   - Tabela com: Nome do lote, Status, Qtd. imagens, Criado em, Ações
4. CTA Primário
   - Botão: Criar novo lote (batch upload)
5. Atalhos Rápidos
   - Acessar API Tokens
   - Ver histórico de cobranças
   - Convidar usuário

## Estados da Tela
- Empty State:
  - Mensagem: "Nenhum lote criado ainda"
  - CTA: Criar primeiro lote
- Loading State:
  - Skeleton para cards e tabela
- Error State:
  - Mensagem clara + ação de retry

## Acessibilidade (Obrigatório)
- Navegação completa por teclado
- Header e cards com hierarquia semântica correta (H1, H2)
- CTA com aria-label descritivo
- Estados de loading anunciados via aria-live

## Eventos/Interações
- Clique em "Criar novo lote" abre fluxo de batch upload
- Clique em lote abre detalhes/resultados
- Clique em "Comprar créditos" redireciona para billing
