# Carregamento determinístico de corpus (RAG)

```
[LEITURA_DO_CORPUS]
escopo: "global|eixo|subeixo"
alvo: "<caminho_logico>"
[/LEITURA_DO_CORPUS]
```

## Valores aceitos

```
escopo = global
alvo = global
```

```
escopo = eixo
alvo = "eixo 1" | "eixo 3" | "eixo 1 e 3"
```


```
escopo = subeixo
alvo = "eixo X/nome-do-subeixo"
```

## Comportamento

- Carrega corpus a partir de:

```
source=/mnt/data/as-cronicas-do-sol-e-do-gelo-v1.zip
```

- O escopo passa a valer para **todas as perguntas subsequentes**
- Nova sessão ⇒ novo comando obrigatório

## Regras duras

- Leitura real dos arquivos é obrigatória
- Arquivos lidos devem ser explicitamente listados

- **Antes de qualquer resposta**:
- ao menos uma citação literal do corpus deve ser exibida
- É proibido:
- citar arquivos inexistentes
- inferir fatos fora do texto carregado
- responder sem lastro textual
- `escopo=global` exige leitura exaustiva (tudo-ou-nada)

## Inferência

- Inferência interpretativa é permitida
- Deve ser explicitamente rotulada como **inferência**
- Nunca apresentada como citação