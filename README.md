# tarefas-cli

Gerenciador de tarefas na linha de comando, escrito em **TypeScript**. Adiciona, lista, conclui e remove tarefas, guardando tudo em um arquivo JSON local.

## Por que este projeto

Mostra fundamentos de um bom projeto Node/TypeScript:

- **TypeScript estrito** (`strict: true`), com tipos de dominio bem definidos
- **Arquitetura em camadas**: dominio puro (`task.ts`), persistencia (`store.ts`) e interface (`cli.ts`) separados, cada um testavel de forma independente
- **Funcoes puras e imutaveis** no nucleo (nenhuma muta o estado recebido), o que torna o comportamento previsivel
- **Tratamento de erros** com um tipo proprio (`ErroDeTarefa`), distinguindo falhas esperadas de bugs
- **Testes automatizados** com Vitest, cobrindo dominio e integracao com disco (usando pastas temporarias)

## Tecnologias

TypeScript, Node.js (ES Modules), Vitest, tsx.

## Como usar

```bash
# Instala as dependencias
npm install

# Roda direto do codigo-fonte (sem compilar)
npm start -- add "Estudar TypeScript" --prioridade alta
npm start -- list
npm start -- done 1
npm start -- remove 1
```

Ou compile para um binario:

```bash
npm run build
node dist/index.js list
```

### Comandos

| Comando | Descricao |
|---------|-----------|
| `add <titulo> [--prioridade baixa\|media\|alta]` | Cria uma tarefa |
| `list` | Lista as tarefas (pendentes primeiro, por prioridade) |
| `done <id>` | Marca como concluida |
| `remove <id>` | Remove |
| `help` | Mostra a ajuda |

As tarefas ficam em `~/.tarefas/tarefas.json`. Para mudar o local, defina a variavel `TAREFAS_ARQUIVO`.

### Exemplo de saida

```
$ npm start -- list
[ ] #2 (alta) Revisar contrato
[ ] #1 (media) Estudar TypeScript
[x] #3 (baixa) Comprar cafe
```

## Testes

```bash
npm test          # roda uma vez
npm run test:watch  # modo observacao
npm run typecheck   # verifica os tipos sem gerar codigo
```

## Estrutura

```
tarefas-cli/
  src/
    task.ts    # dominio: tipos e regras puras
    store.ts   # persistencia em JSON
    cli.ts     # interpretacao de comandos
    index.ts   # ponto de entrada
  tests/
    task.test.ts
    cli.test.ts
```

## Licenca

[MIT](LICENSE)
