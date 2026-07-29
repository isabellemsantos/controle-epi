# Prompt de Kickoff — Claude Code

```
Crie um mini projeto Next.js 14+ (App Router) chamado "controle-epis" com a seguinte stack:

- Prisma ORM com SQLite (arquivo dev.db local, sem configuração externa)
- Better Auth para autenticação (email/senha), com suporte a roles "admin" e "operador"
- Tailwind CSS + shadcn/ui para os componentes
- TypeScript

## Schema do banco (Prisma)
Use o schema.prisma deste repositório (prisma/schema.prisma), ajustando apenas se necessário para compatibilidade com Better Auth.

## Funcionalidades a implementar

1. Autenticação
   - Tela de login (email/senha)
   - Seed inicial cria um usuário admin (defina email/senha via variável de ambiente)
   - Usuário admin tem uma tela para criar novos usuários (role "operador")
   - Middleware protegendo todas as rotas exceto /login

2. Cadastro de EPIs (CRUD)
   - Listagem com busca por nome/código/CA
   - Formulário de criação/edição: código, nome, CA, validade, marca, unidade (PC, PR, CX...), quantidade inicial
   - Exibir saldo atual em cada item da listagem

3. Cadastro de Funcionários (CRUD)
   - Listagem com busca por nome
   - Formulário de criação/edição: nome, setor, matrícula (opcional), ativo

4. Movimentação de Estoque
   - Tela para registrar ENTRADA: seleciona EPI + quantidade + observação (soma ao saldo)
   - Tela para registrar SAÍDA: seleciona EPI + funcionário + quantidade + observação (subtrai do saldo)
   - Validar que a saída não pode ultrapassar o saldo disponível (mostrar erro amigável)
   - Toda movimentação salva automaticamente o usuário logado e a data/hora

5. Dashboard / Estoque
   - Tela inicial mostrando saldo atual de todos os EPIs (destacar itens com saldo baixo, ex: < 5 unidades)
   - Tela de histórico de movimentações, filtrável por EPI ou por funcionário

## Requisitos técnicos
- Usar Server Actions do Next.js para as mutações (criar/editar/registrar movimentação)
- Validação de formulários com Zod
- Layout simples com sidebar (Dashboard, EPIs, Funcionários, Movimentações, Usuários [somente admin])
- Deixar preparado (mas não implementar) um botão "Exportar Excel" desabilitado/"em breve" na tela de histórico, para a fase 2

## Entregáveis
- Projeto completo rodando com `npm install && npx prisma migrate dev && npm run dev`
- Seed script criando o usuário admin inicial
- README explicando como rodar localmente e como fazer deploy via Docker/EasyPanel (volume persistindo o dev.db)
```
