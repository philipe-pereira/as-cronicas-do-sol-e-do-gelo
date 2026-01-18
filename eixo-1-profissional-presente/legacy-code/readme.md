# Opções de migração de aplicações Java

Este documento consolida as opções consideradas para substituir o modelo **JNLP/Java Web Start**, e registra os caminhos técnicos escolhidos para evolução futura.  

## 1) As 5 opções reais que existiam

| Opção | Descrição curta | Vantagens | Desvantagens | Decisão |
|---|---|---|---|---|
| **1 — Reposição direta do JNLP** | Procurar um “novo JNLP” (execução local fácil via browser) | Teoricamente manteria a experiência antiga | Browsers modernos bloqueiam execução local; modelo de segurança acabou; alternativas tendem a ser instáveis/abandonadas | **Descartada** (não viável) |
| **2 — Desktop app distribuído (installer)** | Manter Swing/Java e distribuir instalador/atualizações | Reuso máximo do código; simples conceitualmente; funciona offline | Perde portabilidade web; distribuição/updates são mais pesados que JNLP; exige instalação | **Aceita** para legado (ex.: Cemig) |
| **3 — Swing “via web” por sessão remota** | Rodar Swing no servidor e “streamar” UI (VNC/RDP-like) | Pouca mudança no Swing; centraliza execução | Latência; UX inferior; escalabilidade e custos; arquitetura mais complexa | **Descartada** (possível, mas pouco sustentável) |
| **4 — Vaadin / JavaFX WebView** | Manter Java como base e levar UI ao browser via framework/empacotamento | Continua em Java; integração backend forte | Toolchain pesada; build e dependências; portabilidade não é “instantânea”; atrito operacional | **Não escolhida** (alto atrito) |
| **5 — Reescrita total para Web** | UI no browser com **TS + Canvas/SVG/WebGL/WebGPU** | Portabilidade total; browser como runtime universal; controle fino de rendering; longevidade | Reescrita de UI; curva inicial de aprendizado | **Escolhida** para projetos pessoais/futuros |

> **Síntese:** JNLP acabou. Swing continua válido para legado. Para novos projetos portáveis, a base é **web nativa**.

---

## 2) Caminho A — Web nativa (TypeScript + Canvas / SVG / WebGL / WebGPU)

Este é o caminho principal adotado.

### Ordem lógica de estudo

1. **JavaScript moderno + TypeScript**
   - ES Modules (`import` / `export`)
   - tipos, interfaces, generics
   - organização por arquivos (módulos)
   - build mental **sem framework** (procedural)

2. **Canvas 2D**
   - modelo procedural (equivalente ao `paintComponent`)
   - sistema de coordenadas
   - transformações (`translate`, `scale`, `rotate`)
   - *event handling* (mouse, wheel, touch)
   - *render loop* (`requestAnimationFrame`) quando precisar

3. **SVG**
   - vetorial declarativo (precisão/zoom)
   - `viewBox`, transform, grupos
   - *hit testing* e eventos (cliques/drag) com semântica forte
   - ideal para desenhos técnicos e diagramas “limpos”

4. **Arquitetura gráfica**
   - separação **modelo / render / interação**
   - estado explícito (params, seleção, zoom/pan)
   - redraw determinístico (render sempre a partir do estado)

5. **WebGL / WebGPU (quando necessário)**
   - GPU para performance (muitos elementos, simulações, 3D)
   - renderização acelerada e pipelines gráficos
   - entra quando Canvas/SVG não entregarem desempenho

### Termos-chave (para pesquisa rápida)
- `CanvasRenderingContext2D`
- `requestAnimationFrame`
- `devicePixelRatio` (canvas “retina”)
- pan/zoom (transform + view)
- `viewBox` (SVG)
- WebGL vs WebGPU (pipeline, shaders)

---

## 3) Caminho B — C/C++/Rust → WebAssembly (WASM) + Canvas/WebGPU

Este caminho é **complementar** e faz sentido quando você quer **motor de cálculo pesado** no browser.

### Quando vale a pena
- cálculo intensivo (muitos elementos, iterações, grandes matrizes)
- reaproveitar código científico existente em C/C++/Rust
- performance crítica, mantendo a UI web

### Conceitos-chave (para começar)
- **WebAssembly (WASM)**: bytecode executado no browser
- **Emscripten** (C/C++)
- **wasm-bindgen** (Rust)
- **memória linear** e serialização de dados
- ponte **JS ↔ WASM**
- WASM como **motor de cálculo**, UI continua em **Canvas/SVG/WebGPU**

---

## 4) Síntese final (para não voltar ao assunto)
- **JNLP acabou** e não volta como era
- **Swing** fica como solução de legado (quando for aceitável instalar)
- **Browser** é o runtime universal
- **Canvas/SVG** são as primitivas gráficas modernas
- **TypeScript** é a base de engenharia para o frontend
- **WASM** é aceleração, não “framework de UI”
