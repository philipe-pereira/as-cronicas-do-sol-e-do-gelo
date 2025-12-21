## Geração automática pelo Aurélio

```
[EXPORT_MARKDOWN]
conversa: "<nome exato da conversa/sessão>"
escopo: "<evento|periodo|topico>"
periodo:
  inicio: "YYYY-MM-DD"           # opcional
  fim:    "YYYY-MM-DD"           # opcional
  notas:  "<texto livre>"        # opcional (ex: 'antes da viagem', 'pós-retorno', etc.)
fatos_ancora:
  - "<fato datável 1>"           # opcional (ex: '14/06/2025 não queria ir ao Brasil')
  - "<fato datável 2>"
modo_saida: "arquivo_unico|multi_arquivos"
tipo_saida: "cronica|fragmentos|carta|linha_do_tempo|resumo_estrutural"
granularidade: "baixa|media|alta"
nivel_interpretacao: "baixo|medio|alto"
voz: "philipe_1a_pessoa|philipe_3a_pessoa|mista"
estilo: "classico|seco|literario_controlado"
secao_destino: "cronologico|acronologico|ambos"
eixos:
  incluir: [1,2,3,4,5,6,7,8,9]   # opcional
  excluir: []                    # opcional
metadados:
  tags: ["...","..."]            # opcional
  ciclo_octahebdomal: "C1"       # opcional (ex: C1)
  missao: "M3"                   # opcional (ex: M1..M5)
  estado: "sol|gelo|neblina|guerra_tatica|paz_rara"  # opcional
politica_de_fontes: "nao_citar|citar_trechos_curto|somente_resumo"
confianca_minima: "baixa|media|alta"
privacidade:
  redigir_nomes: "sim|nao"        # default: sim
  redigir_locais: "sim|nao"       # default: nao
nomenclatura_arquivos:
  prefixo_data: "sim|nao"         # default: sim (ex: 2025-06-14-...)
  slug: "<manual|auto>"           # default: auto
saida:
  incluir_frontmatter: "sim|nao"  # default: sim
  incluir_links_internos: "sim|nao" # default: sim
  incluir_bloco_constantes: "sim|nao" # default: sim (se tiver material)
[/EXPORT_MARKDOWN]
```