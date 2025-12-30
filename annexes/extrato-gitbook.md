# Geração canônica de extrato GitBook

```
[EXTRATO_GITBOOK]
fonte:
conversa: "<nome da conversa>" # opcional
corpus: "ativo|nao_usar" # default: ativo (se houver LEITURA_DO_CORPUS)
escopo:
eixo: "<numero|lista>" # opcional (ex: 3 ou 1,3,6)
subeixo: "<caminho>" # opcional (ex: 9/ecce-ego)
recorte:
periodo:
inicio: "YYYY-MM-DD" # opcional
fim: "YYYY-MM-DD" # opcional
eventos_chave:
- "<evento datável>" # opcional
estrutura:
modo: "canonica" # fixo
arquivos:
narrativa: "sim|nao" # default: sim
simbolos: "sim|nao" # default: sim
viradas: "sim|nao" # default: sim
sintese: "sim|nao" # default: sim
rigor:
exigir_citacoes_literais: "sim|nao" # default: sim
separar_fato_interpretacao: "sim|nao" # default: sim
saida:
formato: "gitbook"
modo: "multi_arquivos" # fixo
[/EXTRATO_GITBOOK]
```

## Regras implícitas

- Estrutura **fixa** (README + simbolos / viradas / sintese)
- Ausência de qualquer arquivo obrigatório = execução inválida
- Citações literais sempre entre aspas
- Inferências **devem** ser marcadas como inferência
- Nenhum conteúdo fora do escopo declarado