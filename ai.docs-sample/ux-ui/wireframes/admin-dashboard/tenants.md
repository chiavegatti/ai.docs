# Admin Dashboard — Tenants Management (Wireframe)

## Objetivo da Tela
Permitir que a operação/admin da plataforma gerencie empresas (tenants), planos, uso e status operacional.

## Usuários
- Admin da Plataforma

## Blocos da Tela (Hierarquia Visual)
1. Header
   - Indicadores globais:
     - Tenants ativos
     - Jobs em processamento
     - Backlog de revisão humana
2. Lista de Empresas (Tenants)
   - Tabela com:
     - Nome da empresa
     - Plano/Pacote atual
     - Créditos disponíveis
     - Volume do mês
     - Status (Ativo/Suspenso)
     - CTA: Ver detalhes
3. Filtros e Busca
   - Busca por nome
   - Filtro por status
   - Filtro por plano
4. Ações Administrativas
   - Suspender/Reativar tenant
   - Ajustar créditos (crédito manual)
   - Ver histórico de consumo
5. Alertas Operacionais
   - Tenants com falha de cobrança
   - Tenants com backlog elevado
   - Revisores sobrecarregados

## Estados da Tela
- Empty State:
  - Mensagem: "Nenhuma empresa cadastrada"
- Loading State:
  - Skeleton da tabela
- Error State:
  - Mensagem clara + retry

## Acessibilidade (Obrigatório)
- Tabela navegável por teclado
- Ações com rótulos claros
- Confirmação para ações destrutivas (suspender tenant)
- Alertas anunciados via aria-live

## Eventos/Interações
- Clique em "Ver detalhes" abre visão completa do tenant
- Ações administrativas exigem confirmação
