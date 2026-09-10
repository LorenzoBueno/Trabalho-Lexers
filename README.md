# TP1 — Análise Comparativa de Lexers ANTLR4

Trabalho Prático 1 da disciplina **Linguagens de Programação** (PUCRS/Escola Politécnica, 2026/II).

Análise crítica e comparação de dois analisadores léxicos (lexers) desenvolvidos com **ANTLR4**, com foco nas regras de reconhecimento em exemplos de **texto**, **inteiro** e **número real**.

## Analisadores léxicos escolhidos

| Linguagem | Arquivo | Fonte |
|---|---|---|
| Python | [`PythonLexer.g4`](./PythonLexer.g4) | [antlr/grammars-v4](https://github.com/antlr/grammars-v4) |
| Java | [`JavaLexer.g4`](./JavaLexer.g4) | [antlr/grammars-v4](https://github.com/antlr/grammars-v4) |

## Estrutura do repositório

```
Trabalho 1
├── PythonLexer.g4
├── JavaLexer.g4
├── .antlr
├── diagramas/
│   ├── python-string.png
│   ├── python-decimal-integer.png
│   ├── python-float-number.png
│   ├── java-string-literal.png
│   ├── java-decimal-literal.png
│   └── java-float-literal.png
└── README.md
```

## Regras analisadas

Para cada lexer, foram escolhidas três regras independentes:

| Categoria | Regra (Python) | Regra (Java) |
|---|---|---|
| TEXTO | `STRING` | `STRING_LITERAL` |
| INTEIRO | `DECIMAL_INTEGER` | `DECIMAL_LITERAL` |
| REAL | `FLOAT_NUMBER` | `FLOAT_LITERAL` |

### Resumo das diferenças principais

- **Prefixos de string**: Python suporta prefixos (`u`, `f`, `r`, `b`, combinações como `rb`/`br`) diretamente na regra `STRING`, alterando a semântica do literal (raw, bytes, f-string). Java não tem prefixos em `STRING_LITERAL`.
- **Strings multilinha**: Python define isso na própria regra `STRING` (`LONG_STRING`, com aspas triplas). Java trata isso como uma regra à parte, `TEXT_BLOCK`.
- **Separador de dígitos (`_`)**: suportado em `DECIMAL_LITERAL` e `FLOAT_LITERAL` do Java (ex: `10_000.00`); **não suportado** em `DECIMAL_INTEGER`/`FLOAT_NUMBER` do Python.
- **Sufixos numéricos**: Java tem sufixos explícitos (`L`/`l` para inteiros, `f`/`F`/`d`/`D` para reais). Python não tem sufixos equivalentes nessas regras.
- **Zeros à esquerda**: em Python, `DECIMAL_INTEGER` só reconhece uma sequência de dígitos começando com `[1-9]`, ou uma sequência formada só por `0`s — um número como `007` não casa como um único token. Em Java, esse caso é coberto por `OCT_LITERAL`, uma regra separada para literais octais.

## Ferramentas utilizadas

- [ANTLR4](https://www.antlr.org/) — geração e teste das gramáticas léxicas
- [ANTLR4 grammar syntax support (VS Code)](https://marketplace.visualstudio.com/items?itemName=mike-lischke.vscode-antlr4) — geração dos diagramas de sintaxe (railroad diagrams) e testes interativos de reconhecimento de tokens

## Grupo

- Antonio Dal Bem
- Arthur Ferreira
- Lorenzo Bueno

## Disclosure

Os arquivos `PythonLexer.g4` e `JavaLexer.g4` utilizados neste trabalho não foram desenvolvidos pelo grupo. Ambos foram obtidos do repositório público [antlr/grammars-v4](https://github.com/antlr/grammars-v4), mantido pela comunidade ANTLR, e são utilizados aqui exclusivamente para fins de análise e comparação acadêmica, conforme enunciado do TP1.
