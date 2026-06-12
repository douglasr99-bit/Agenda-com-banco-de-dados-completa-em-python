# Agenda Python

Este projeto contém um aplicativo de agenda simples em Python que usa um banco de dados SQLite para salvar nomes e telefones.

## Arquivo principal

- `agenda_python.py`

## O que o código faz

O script implementa um sistema de agenda de contatos com as seguintes funcionalidades:

- criar ou abrir um banco de dados SQLite
- armazenar contatos com nome
- armazenar múltiplos números de telefone para cada contato
- classificar tipos de telefone padrão (`celular`, `fixo`, `fax`, `casa`, `trabalho`)
- adicionar novo contato
- editar nome e telefones de um contato existente
- excluir um contato
- listar todos os contatos salvos

## Componentes principais

### Banco de dados

- `BANCO`: script SQL que cria as tabelas `tipos`, `nomes` e `telefones`
- O banco de dados é criado automaticamente quando não existe
- As tabelas armazenam:
  - tipos de telefone
  - nomes de contatos
  - telefones vinculados ao contato e ao tipo

### Validação de entrada

- `nulo_ou_vazio(texto)`: verifica se uma entrada é vazia ou nula
- `valida_faixa_inteiro(...)`: solicita um valor inteiro dentro de um intervalo
- `valida_faixa_inteiro_ou_branco(...)`: permite selecionar um índice ou deixar em branco para cancelar

### Estruturas de dados

- `ListaUnica`: lista que só aceita elementos únicos de um determinado tipo
- `DBListaUnica`: estende `ListaUnica` e guarda objetos removidos para exclusão no banco

### Entidades do domínio

- `Nome`: representa um nome válido e cria uma chave interna para comparação
- `DBNome`: `Nome` com um campo `id` do banco
- `TipoTelefone`: tipo de telefone legível
- `DBTipoTelefone`: tipo de telefone com `id`
- `Telefone`: número de telefone com tipo opcional
- `DBTelefone`: `Telefone` com campos de banco (`id`, `id_nome`)
- `DBDadoAgenda`: agrupa um `DBNome` e uma lista de telefones para um contato

### Persistência com SQLite

- `DBAgenda`: gerencia a conexão, carregamento, inserção, atualização e exclusão de dados
  - `carregaTipos()`: carrega tipos de telefone já existentes do banco
  - `pesquisaNome()`: pesquisa contato por nome
  - `lista()`: lista todos os contatos
  - `novo()`, `atualiza()`, `apaga()`: manipulação de dados com transações

### Interface de linha de comando

- `Menu`: exibe opções e executa a escolha do usuário
- `AppAgenda`: implementa as ações do usuário:
  - `novo`
  - `apaga`
  - `alterar`
  - `lista`
  - adicionar, alterar e apagar telefones de um contato

## Como rodar em qualquer computador

### Requisitos

- Python 3 instalado
- sistema de arquivos com permissão de escrita no diretório onde o banco de dados será criado

### Passos

1. Abra um terminal na pasta `Agenda_Python`
2. Execute o script informando o arquivo de banco de dados SQLite que deseja usar:

```bash
python3 agenda_python.py agenda.db
```

> Se `agenda.db` não existir, o script irá criá-lo automaticamente com as tabelas e tipos de telefone padrão.

### Uso do programa

Após iniciar, o programa mostra um menu com opções:

- `Novo`: cadastrar novo contato
- `Editar`: modificar contato existente
- `Apagar`: excluir contato
- `Listar`: exibir todos os contatos
- `Sair`: encerrar

Para editar telefones de um contato, você poderá:

- adicionar (`N`)
- alterar (`A`)
- apagar (`D`)
- sair da edição (`S`)

### Observações

- O script não exige dependências externas; usa apenas a biblioteca padrão do Python
- O arquivo de banco é especificado como argumento. Sempre passe um nome de arquivo para o banco de dados
- A primeira execução cria o banco e carrega os tipos de telefone automáticos

## Exemplo completo

```bash
cd /home/sua_pasta/Agenda_Python
python3 agenda_python.py agenda.db
```

Em seguida, escolha uma opção no menu e siga as instruções na tela.
