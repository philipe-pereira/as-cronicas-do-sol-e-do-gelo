# svg-ascensao

## Objetivo do protocolo

Definir um **formato único, inequívoco e durável** para intercâmbio de esquemas técnicos entre humano e assistente.

O protocolo evita:
- ambiguidades semânticas
- decisões implícitas
- dependência de softwares proprietários

---

## Princípios

- SVG como formato base
- unidades explícitas (mm)
- semântica > aparência
- tudo importante tem `id`

---

## Estrutura obrigatória

### Metadata

```xml
<metadata id="asce-meta" type="application/json">
{
  "schema": "SVG-ASCENSAO-v1.2",
  "units": "mm",
  "scale": "1:50",
  "origin": "top-left"
}
</metadata>
```

---

## Camadas padrão

- layer-walls
- layer-openings
- layer-zones
- layer-dimensions
- layer-annotations

---

## Paredes

- Parede lógica = `<g class="wall">`
- Geometria = `<polygon class="wall-seg">`
- Portas **não pertencem a segmentos**, mas à parede-mãe.

---

## Zonas de uso

- Não estruturais
- Informativas
- Usadas para tomada de decisão

Atributos importantes:
- data-usage
- data-permanence
- data-confidence

---

## Aberturas

- portas
- janelas
- recessos (radiator-recess, closet-recess)

Todos modelados como **volumes negativos**.

---

## Cotas

- agrupadas em `<g class="dim">`
- valor canônico em `data-value-mm`

---

## Regra de ouro

> **Semântica governa geometria.**