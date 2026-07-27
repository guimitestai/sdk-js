# 🧪 Guimí Test AI — SDK JavaScript/TypeScript

[![npm version](https://img.shields.io/npm/v/guimitestai.svg)](https://www.npmjs.com/package/guimitestai)
[![License: BSL-1.1](https://img.shields.io/badge/License-BSL--1.1-orange.svg)](https://github.com/guimitestai/sdk-js/blob/main/LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green.svg)](https://nodejs.org/)

> **Teste sua IA antes que um hacker faça isso em produção.**

SDK oficial JavaScript/TypeScript para testes, observabilidade e conformidade de LLMs. Detecte prompt injection, alucinações, shadow AI e violações de LGPD — de forma simples, em minutos.

---

## Instalação

```bash
npm install guimitestai
# ou
pnpm add guimitestai
# ou
yarn add guimitestai
```

---

## Início Rápido

```typescript
import { GuimiClient } from 'guimitestai';

// Modo gratuito — logs no console, sem API key
const guimi = new GuimiClient();

// Modo Pro — dados no dashboard guimitestai.com
const guimi = new GuimiClient({ apiKey: 'sk-guimi-...' });
```

---

## Módulos

### 🔭 Observabilidade

```typescript
import { Tracer } from 'guimitestai';

const tracer = new Tracer({ apiKey: 'sk-guimi-...' });

const trace = await tracer.trace({
  model: 'gpt-4o',
  input: 'Qual é a capital do Brasil?',
  output: 'Brasília',
  latencyMs: 342,
  tokens: { prompt: 18, completion: 4, total: 22 },
  metadata: { environment: 'production', version: '2.1.0' }
});

console.log(trace.traceId); // aparece no dashboard
```

### ⚖️ LLM-as-Judge

```typescript
import { Evaluator } from 'guimitestai';

const evaluator = new Evaluator({ apiKey: 'sk-guimi-...' });

const result = await evaluator.evaluate({
  input: 'Explique machine learning',
  output: 'Machine learning é...',
  criteria: ['accuracy', 'safety', 'helpfulness']
});

console.log(result.score);    // 0.0 – 1.0
console.log(result.passed);   // true/false
console.log(result.feedback); // explicação detalhada
```

### 🔴 Red-Teaming OWASP LLM Top 10

```typescript
import { RedTeamer } from 'guimitestai';

const redTeamer = new RedTeamer({ apiKey: 'sk-guimi-...' });

const report = await redTeamer.run({
  target: async (prompt) => {
    // sua função que chama o LLM
    return await myLLM.complete(prompt);
  },
  profile: 'owasp_llm_top10' // Pro: full OWASP coverage
});

console.log(report.vulnerabilities); // lista de vulnerabilidades encontradas
console.log(report.riskScore);       // 0-100
```

### 🛡️ Compliance LGPD / EU AI Act

```typescript
import { ComplianceChecker } from 'guimitestai';

const checker = new ComplianceChecker({ apiKey: 'sk-guimi-...' });

const result = await checker.check({
  text: 'O usuário João Silva, CPF 123.456.789-00...',
  frameworks: ['lgpd', 'eu_ai_act']
});

console.log(result.violations); // dados pessoais detectados
console.log(result.compliant);  // false
```

---

## Modo Gratuito vs Pro

| Funcionalidade | Gratuito | Pro |
|---|---|---|
| Traces no console | ✅ | ✅ |
| Traces no dashboard | ❌ | ✅ |
| LLM-as-Judge (básico) | ✅ accuracy, helpfulness | ✅ todos os critérios |
| Red-Teaming | ✅ 3 ataques básicos | ✅ OWASP LLM Top 10 completo |
| Compliance LGPD | ❌ | ✅ |
| Relatórios PDF | ❌ | ✅ |
| Suporte prioritário | ❌ | ✅ |

**Obtenha sua API key Pro em [guimitestai.com](https://guimitestai.com)**

---

## Licença

Este SDK é distribuído sob a **Business Source License 1.1 (BSL-1.1)**.

- ✅ **Uso gratuito** para projetos pessoais, acadêmicos e startups com menos de 10 funcionários
- ✅ **Uso interno** em empresas de qualquer tamanho
- ❌ **Uso comercial como serviço** (SaaS/PaaS) requer licença comercial
- 📅 Converte para Apache 2.0 em **1 de janeiro de 2028**

Veja [LICENSE](./LICENSE) para detalhes completos.

---

## Links

- 🌐 [guimitestai.com](https://guimitestai.com)
- 📦 [npm](https://www.npmjs.com/package/guimitestai)
- 🐍 [SDK Python](https://github.com/guimitestai/sdk)
- 📖 [Documentação](https://guimitestai.com/docs)
- 🐛 [Issues](https://github.com/guimitestai/sdk-js/issues)
