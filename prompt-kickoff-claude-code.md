# Prompt para Google Stitch (protótipo visual)

```
Crie um protótipo de interface para um sistema web simples de "Controle de EPI's - Almoxarifado".

Estilo visual: limpo, corporativo/industrial, cores neutras (cinza, azul escuro), boa legibilidade, componentes no estilo shadcn/ui.

Telas necessárias:

1. Login
   - Campos de email e senha, botão "Entrar"

2. Dashboard / Estoque
   - Sidebar de navegação (Dashboard, EPIs, Funcionários, Movimentações, Usuários)
   - Tabela com saldo atual de cada EPI (nome, CA, validade, quantidade), destacando em vermelho/amarelo itens com saldo baixo
   - Botões de ação rápida: "Registrar Entrada" e "Registrar Saída"

3. Cadastro de EPIs
   - Listagem em tabela com busca (nome/código/CA)
   - Modal ou página de formulário: código, nome, CA, validade, marca, unidade, quantidade inicial
   - Botões editar/excluir por linha

4. Cadastro de Funcionários
   - Listagem em tabela com busca (nome)
   - Modal ou página de formulário: nome, setor, matrícula, ativo (toggle)

5. Registrar Movimentação
   - Formulário com seleção de tipo (Entrada/Saída)
   - Se Saída: campo de seleção de funcionário aparece
   - Campos: EPI (select), quantidade, observação
   - Mensagem de erro visível se saída ultrapassar o saldo

6. Histórico de Movimentações
   - Tabela com data, tipo (badge Entrada/Saída), EPI, funcionário (se saída), quantidade, usuário que registrou
   - Filtros por EPI, funcionário e período
   - Botão "Exportar Excel" (desabilitado, com tooltip "em breve")

7. Usuários (visível apenas para admin)
   - Listagem de usuários com role
   - Formulário para criar novo usuário (nome, email, senha, role)

Priorize simplicidade e clareza — é um sistema pequeno de uso interno, não precisa de elementos visuais complexos.
```
