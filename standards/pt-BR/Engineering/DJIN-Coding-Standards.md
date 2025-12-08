# DJIN Tech — Padrões de Código

> Estrutura clara. Paradigma funcional. Simplicidade através de funções. Zod no núcleo. Legível para humanos.

---

## Estilo de Código

### Composition API & TypeScript Apenas

* Use `<script setup lang="ts">`
* Não misture Options API a menos que explicitamente justificado.

### Declarações de Função

* ❌ Evite funções anônimas: `const x = () => {}`
* ✅ Use funções nomeadas: `function x() {}`

### Blocos #region

* Use `// #region` e `// #endregion` consistentemente
* Funciona em `.ts`, `.vue` e blocos de template

```vue
<template>
  <!--#region Feature A -->
  <div>{{ sayHello() }}</div>
  <!--#endregion Feature A -->
</template>

<script setup lang="ts">
//#region Imports
import nuxt from 'nuxt'
//#endregion

//#region Feature A
const greeting = 'Hello World!'
function say(str: string) { return str }
function sayHello() { return say(greeting) }
//#endregion
</script>
```

> 💡 VS Code: `[CTRL+K CTRL+8]` para recolher todas as regiões

### Uso de Logger

* Crie um composable de classe `Logger` para lidar com logging se não existir
* Loggers devem sempre ter os métodos `log`, `info`, `warn`, `error`
* Logs devem ser legíveis como `[INFO][YYYY-MM-DD HH:MM:SS][File:Line] Message`
* Substitua todos os `console.log` por `Logger.log`

---

### Programação Nullable

* Assuma que todos os valores podem ser null ou undefined — especialmente os aninhados
  → Não confie em nada, nem mesmo no seu próprio código.
* Use optional chaining (`?.`) consistentemente para evitar erros de runtime
  → `user?.profile?.address?.street`
* Forneça valores de fallback usando nullish coalescing (`??`) ou factories padrão
  → `const name = user?.profile?.name ?? 'ゲスト'`
* Nunca lance exceções na UI — ao invés disso:

  * Use `v-if`, `v-else`, ou componentes skeleton/loading
  * Desabilite botões ou inputs quando dados estiverem faltando
  * Mostre mensagens claras de validação ou aviso
* Prefira computed properties defensivas ao invés de otimistas
  → Envolva em fallbacks seguros ou guardas try/catch quando necessário
* Evite confiar profundamente em types, mesmo em TypeScript — a estrutura ainda pode ser quebrada em runtime (ex.: de API ou localStorage)

---

## Padrões de Arquitetura

### Paradigma Black Box

* Evite estado global ou estruturas similares a classes a menos que absolutamente necessário
* Prefira composição ao invés de lógica baseada em classes
* Tudo é uma função, objeto, componente ou composable. Sem herança de classe
* Evite estado global ou estruturas similares a classes a menos que absolutamente necessário

### Estrutura de Utilitários

Organize lógica de propósito geral em `utils/`:

* `arrays.ts`
* `objects.ts`
* `japanese.ts`
* etc.

Verifique antes de implementar novos utilitários para evitar duplicação.

### Composables

Evite a convenção `useX()`. Use composables globais prefixados com `$`:

```ts
export default const $myComposable = {
  foo() {
    return 'bar'
  }
} as const
```

* Deve ser declarado como `const` exportado por default
* Deve começar com `$`

---

## Zod como SST (Single Source of Truth)

### Princípio

Zod define cada interface no sistema:

* Validação
* Types
* Props
* Lógica baseada em shape

### Tipos de Interfaces

| Tipo     | Caso de Uso                                  | Exemplo                   |
|----------|----------------------------------------------|---------------------------|
| System   | Páginas, componentes, composables            | `z.system.pageSchema`     |
| Database | Estrutura PostgreSQL, validação, migrações   | `z.database.userSchema`   |

### Benefícios

* Extraia types e props do mesmo schema
* Local central para lógica consistente
* Elimina duplicação de interfaces
* Pode construir estrutura de banco de dados a partir de interfaces do sistema e aplicar a filosofia de Steve Jobs (`"Comece o desenvolvimento da perspectiva do usuário, só então desenvolvemos a tecnologia"`)

Armazene schemas compartilhados em uma pasta globalmente acessível e reutilize-os em todas as camadas.

### Tamanhos de Arquivo

* Devemos manter arquivos concisos, pequenos e focados. Se um arquivo for muito grande, deve ser dividido em arquivos menores. `Idealmente`, cada arquivo deve ter um único propósito e menos de 2000 linhas. `Idealmente`.

### Convenções de Nomenclatura

* Use `I` para interfaces, `T` para types e `P` para props
* Use `camelCase` para interfaces, types e props
* Use `snake_case` para colunas de banco de dados, tabelas e migrações
* Use `snake_case` para variáveis de ambiente e arquivos de configuração
* Use prefixo `ENV_` para variáveis de ambiente e prefixo `CONFIG_` para arquivos de configuração

---

## Princípios de Execução

> Planejamento sempre antes de codificar
> "Primeiro, resolva o problema. Depois, escreva o código." — John Johnson
> "Programadores ruins se preocupam com código. Bons programadores se preocupam com estruturas de dados e seus relacionamentos." — Linus Torvalds

## CLI

* Sempre use Deno para CLI
* Use os `npm specifiers` do Deno para CLI para evitar problemas de gerenciamento de dependências (https://deno.com/blog/not-using-npm-specifiers-doing-it-wrong)

## Testes

* **Sempre escreva testes** para ferramentas CLI, utilitários e funcionalidade core quando forem concisos e fizerem sentido
* Testes devem ser simples, focados e cobrir os principais casos de uso
* Use o framework de testes integrado do Deno com `Deno.test()`
* **Organização de Testes**:
  - Crie uma pasta `tests/` na raiz do projeto
  - Arquivos de teste devem ser nomeados `*.test.ts` e colocados na pasta `tests/`
  - Espelhe a estrutura fonte: `src/foo.ts` → `tests/foo.test.ts`
  - Para projetos CLI, testes principais vão em `tests/main.test.ts`
* Foque em testar:
  - Parsing e validação de argumentos CLI
  - Tratamento de erros e casos extremos
  - Carregamento de variáveis de ambiente
  - Funções de lógica de negócio core
* Mantenha testes sustentáveis - se um teste se tornar complexo, considere refatorar o código sendo testado
* Testes devem ser rápidos e independentes - sem dependências externas ou modificações no sistema de arquivos quando possível

---

## Outros Recursos

* use `./DJIN-standards.md` para referência
* use `./SYSTEM_SPECS.md` para referência
* use `./EXECUTION_PLAN.md` para referência
