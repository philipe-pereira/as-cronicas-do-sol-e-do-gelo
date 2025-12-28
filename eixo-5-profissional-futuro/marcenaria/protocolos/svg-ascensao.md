# svg-ascensao

## Objetivo do protocolo

Definir um **formato único, inequívoco, auditável e durável** para intercâmbio de esquemas técnicos entre humano e assistente, aplicável a:
- divisórias
- layout de ambientes
- móveis
- carpintaria estrutural

O protocolo existe para **eliminar ambiguidades**, reduzir retrabalho e permitir raciocínio técnico confiável ao longo do tempo.

Ele evita explicitamente:
- interpretações visuais subjetivas
- decisões implícitas escondidas no desenho
- dependência de softwares proprietários ou binários

---

## Princípios fundamentais

1. **SVG como formato base**  
   Vetorial, textual, versionável e legível por humanos.

2. **Unidades explícitas**  
   Toda geometria é expressa em milímetros (`mm`).

3. **Semântica governa geometria**  
   A forma existe para servir ao significado, nunca o contrário.

4. **Nada importante é implícito**  
   Tudo que importa tem `id` e metadados explícitos.

5. **Separação rigorosa de camadas**  
   Estrutura, uso, cota e anotação nunca se misturam.

---

## Estrutura obrigatória do SVG

### ViewBox

- O `viewBox` deve representar o espaço em **mm**.
- A origem padrão é o **canto superior esquerdo**.

Exemplo:
```xml
<svg viewBox="0 0 9000 9000" ...>
```

---

## Metadata (obrigatório)

A metadata é a **autoridade máxima** do desenho.

```xml
<metadata id="asce-meta" type="application/json">
{
  "schema": "SVG-ASCENSAO-v1.2",
  "units": "mm",
  "scale": "1:50",
  "origin": "top-left",
  "project": "basement-dividers",
  "revision": "v6",
  "author": "philipe",
  "notes": "todas as medidas internas, parede = face acabada"
}
</metadata>
```

### Campos obrigatórios
- `schema`
- `units`
- `scale`
- `origin`

### Campos recomendados
- `project`
- `revision`
- `author`
- `notes`

---

## Camadas padrão (obrigatórias)

Cada camada é um `<g>` com `id` fixo.

- `layer-walls` — estrutura física (paredes)
- `layer-openings` — aberturas e vazios
- `layer-zones` — zonas de uso (não estruturais)
- `layer-dimensions` — cotas
- `layer-annotations` — textos livres

Nenhum elemento estrutural deve existir fora dessas camadas.

---

## Paredes

### Conceito

- **Parede lógica** = entidade conceitual contínua
- **Segmento de parede** = geometria concreta

### Representação

```xml
<g id="wall-perimeter" class="wall"
   data-type="wall"
   data-role="perimeter"
   data-thickness-mm="94">

  <polygon id="wall-seg-01" class="wall-seg" points="..."/>
  <polygon id="wall-seg-02" class="wall-seg" points="..."/>
</g>
```

### Regras
- `g.wall` representa a parede-mãe
- `polygon.wall-seg` representa segmentos
- Segmentos **podem ser discontínuos** (por portas ou recessos)
- Portas **nunca pertencem a segmentos**, apenas à parede-mãe

### Atributos importantes
- `data-thickness-mm` (obrigatório)
- `data-role` (perimeter | divider | interior | exterior)

---

## Aberturas (openings)

Aberturas são **volumes negativos**, não objetos decorativos.

### Tipos suportados
- `door`
- `window`
- `cased-opening`
- `radiator-recess`
- `closet-recess`

### Representação padrão

```xml
<rect id="opening-guest" class="opening door"
  data-type="door"
  data-wall="wall-divider-01"
  data-width-mm="813"
  data-height-mm="2030"
  x="..." y="..." width="813" height="94"/>
```

### Regras
- `data-wall` é obrigatório (id da parede-mãe)
- `data-width-mm` é obrigatório
- `data-height-mm` é obrigatório para portas e janelas

---

## Zonas de uso (não estruturais)

Zonas **não representam construção**, apenas intenção de uso.

### Representação

```xml
<polygon id="zone-salon" class="zone salon"
  data-type="zone"
  data-usage="salon"
  data-permanence="fixed"
  data-confidence="high"
  points="..."/>
```

### Campos obrigatórios
- `data-usage`
- `data-permanence` (fixed | semi | temporary)
- `data-confidence` (high | medium | low)

Zonas **nunca** definem paredes automaticamente.

---

## Cotas

Cotas são entidades semânticas completas.

### Estrutura obrigatória

```xml
<g id="dim-01" class="dim"
   data-target="opening-guest"
   data-value-mm="813"
   data-kind="opening">

  <line class="dim-ext" .../>
  <line class="dim-line" .../>
  <text class="dim-text">813</text>
</g>
```

### Regras
- O valor verdadeiro é `data-value-mm`
- O texto é apenas informativo

---

## Estilo (secundário)

Cores, espessuras e fontes **não têm valor semântico**.

O desenho deve continuar interpretável mesmo sem estilo.

---

## Erros comuns (a evitar)

- paredes desenhadas apenas com linhas
- cotas como texto solto
- assumir escala sem declarar
- usar aparência para transmitir significado

---

## Regra de ouro

> **Semântica governa geometria.**

Se houver conflito entre forma e metadado, **o metadado vence**.