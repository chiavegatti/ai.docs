# Client Dashboard — Project Details (Wireframe)

## Objetivo da Tela
Permitir que o cliente visualize os detalhes de um lote/projeto, acompanhe o status por imagem, solicite revisão humana e exporte resultados.

## Usuários
- Owner/Admin da Empresa
- Operador da Empresa

## Blocos da Tela (Hierarquia Visual)
1. Header do Projeto
   - Nome do projeto/lote
   - Status geral (Processando/Concluído/Erro)
   - Data de criação
   - Qtd. de imagens
   - Créditos consumidos (estimado/real)
2. Barra de Progresso do Lote
   - Progresso percentual
   - Itens concluídos vs total
3. Lista de Itens (Imagens)
   - Tabela com:
     - Thumbnail
     - Nome do arquivo
     - Status (Pendente/Processando/Concluído/Erro)
     - Indicador de revisão humana (Sim/Não)
     - CTA: Ver detalhes
4. Filtros e Ações em Massa
   - Filtro por status
   - Filtro por itens com erro
   - Seleção múltipla de itens
   - Ação: Solicitar revisão humana
5. Ações do Projeto
   - Botão: Exportar resultados
   - Botão: Baixar ZIP completo
6. Painel de Alertas
   - Avisos de erros de processamento
   - Avisos de créditos insuficientes
   - Avisos de revisão pendente

## Estados da Tela
- Empty State:
  - Projeto sem itens (erro de upload)
- Loading State:
  - Skeleton da tabela
- Error State:
  - Mensagem clara + retry
- Parcial:
  - Alguns itens com erro, outros concluídos

## Acessibilidade (Obrigatório)
- Tabela navegável por teclado
- Filtros com labels claros
- Status não dependem apenas de cor
- Barra de progresso com texto alternativo

## Eventos/Interações
- Clique em item abre detalhes da imagem (descrições + histórico)
- Seleção múltipla + “Solicitar revisão humana” abre confirmação de custo
- “Exportar resultados” cria export assíncrono e mostra status
