# TypeScript do zero até Canvas vazio

Este documento descreve como criar, do zero absoluto, um projeto web simples para aplicações técnicas (engenharia, física, diagramas), usando **TypeScript + Canvas 2D**, sem frameworks.

## Objetivo

- TypeScript (não JS cru)
- Canvas 2D (primeiro passo)
- Código procedural
- Portabilidade via browser

## Pré-requisitos (executar uma única vez)

### 1) Instalar Node.js (LTS)

Baixar em: https://nodejs.org  
Durante a instalação, marcar: **Add to PATH**

Verificar no PowerShell:

    node -v
    npm -v

### 2) Ajustar PowerShell (Windows)

Abrir PowerShell como Administrador e executar:

    Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned

Fechar e reabrir o PowerShell.

## Criação do projeto

Criar pasta e inicializar:

    mkdir pereira-web-canvas
    cd pereira-web-canvas
    npm init -y

Instalar TypeScript local:

    npm install --save-dev typescript

Criar pastas:

    mkdir src
    mkdir public

## Estrutura esperada

    pereira-web-canvas/
    ├─ src/
    │  └─ main.ts
    ├─ public/
    │  └─ index.html
    ├─ package.json
    └─ tsconfig.json

## Configuração do TypeScript

Criar `tsconfig.json` com o conteúdo:

    {
      "compilerOptions": {
        "target": "ES2020",
        "module": "ES2020",
        "outDir": "public",
        "strict": true,
        "noEmitOnError": true
      },
      "include": ["src"]
    }

## Código TypeScript (Canvas vazio funcional)

Criar `src/main.ts` com o conteúdo:

    const canvas = document.getElementById("canvas") as HTMLCanvasElement;
    const ctx = canvas.getContext("2d")!;

    canvas.width = 800;
    canvas.height = 500;

    // fundo
    ctx.fillStyle = "#ffffff";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    // teste visual
    ctx.strokeStyle = "#000000";
    ctx.lineWidth = 2;
    ctx.beginPath();
    ctx.moveTo(100, 100);
    ctx.lineTo(700, 400);
    ctx.stroke();

    ctx.font = "16px Arial";
    ctx.fillStyle = "#000";
    ctx.fillText("Canvas funcionando", 10, 20);

## HTML mínimo

Criar `public/index.html` com o conteúdo:

    <!DOCTYPE html>
    <html lang="pt-BR">
    <head>
      <meta charset="UTF-8">
      <title>Canvas TypeScript</title>
    </head>
    <body>
      <canvas id="canvas"></canvas>
      <script type="module" src="./main.js"></script>
    </body>
    </html>

## Compilação

Na raiz do projeto, executar:

    npx tsc

Isso gera:

    public/main.js

## Execução

Abrir diretamente no navegador:

    public/index.html

Resultado esperado: Canvas branco, linha diagonal e texto “Canvas funcionando”.


## Adendo — Por que TypeScript é a escolha correta

Este adendo registra, de forma objetiva, os motivos técnicos que justificam a adoção de **TypeScript** — **além** da tipagem estática.  
Objetivo: evitar regressão futura para JavaScript “cru” por subestimar os ganhos reais do TS.

### 1) TypeScript é um sistema de engenharia (não “JS com tipos”)

TypeScript adiciona ao ecossistema web propriedades que aproximam o desenvolvimento da disciplina de linguagens usadas em contextos técnicos: **contratos**, **verificação antecipada** e **refatoração segura**.

### 2) Refatoração confiável (em escala)

TypeScript torna operações comuns **mecanicamente verificáveis**:

- renomear símbolos com segurança
- mover código entre arquivos sem quebras silenciosas
- alterar assinaturas de funções com feedback imediato
- encontrar usos inválidos antes de rodar

Em JS puro, isso depende muito mais de testes manuais e atenção contínua.

### 3) Contratos explícitos entre camadas

Com `interface`, `type`, `union`, `generic`, você declara contratos claros entre:

- modelo matemático
- motor de cálculo
- renderização
- interação

Isso reduz ambiguidades típicas (“pode ser `null`?”, “isso é nó ou barra?”, “coordenada local ou global?”).

### 4) Erros mais cedo (build-time em vez de runtime)

TypeScript empurra uma classe inteira de erros para a fase de build:

- propriedade inexistente
- tipo incompatível
- retorno inesperado
- uso incorreto de APIs

Você troca o ciclo **“rodar e descobrir”** por **“compilar e corrigir”**.

### 5) IntelliSense e navegação estrutural reais

Com TS, o editor deixa de “chutar”:

- autocomplete confiável
- ir-para-definição e referências precisas
- documentação inline útil
- *find references* que funciona de verdade

Isso reduz carga cognitiva e acelera evolução do projeto.

### 6) Rigor configurável como política (`tsconfig`)

Você transforma preferências em regras:

- `strict`
- `noImplicitAny`
- `strictNullChecks`
- etc.

Isso evita “apodrecimento” do projeto ao longo do tempo.

### 7) Tipos não existem em runtime (importante)

- Tipos **não** afetam performance
- Tipos **não** existem em runtime
- TS compila para JS, e os tipos somem

TypeScript organiza o pensamento; JavaScript executa.

### 8) Síntese final

TypeScript foi adotado porque:

- permite evolução **segura**
- reduz ambiguidade conceitual
- torna refatoração **confiável**
- aproxima o frontend web do rigor esperado em **engenharia**
- não impõe runtime próprio nem dependência ao usuário final