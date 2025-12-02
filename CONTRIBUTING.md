# Contributing to Legacy Samuka

Obrigado por considerar contribuir para **Legacy Samuka**! 🎉

Este guia fornece diretrizes e instruções para contribuir ao projeto. Leia com atenção antes de abrir uma PR ou issue.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Como Começar](#como-começar)
- [Tipos de Contribuições](#tipos-de-contribuições)
- [Processo de Pull Request](#processo-de-pull-request)
- [Guias de Estilo](#guias-de-estilo)
- [Dúvidas?](#dúvidas)

## Code of Conduct

### Nossa Promessa

No interesse de promover um ambiente aberto e acolhedor, nós, como colaboradores e mantenedores, nos comprometemos em tornar a participação em nosso projeto e comunidade uma experiência livre de assédio para todos, independentemente de idade, tamanho corporal, deficiência, etnia, identidade de gênero e expressão, nível de experiência, nacionalidade, aparência pessoal, raça, religião ou identidade e orientação sexual.

### Nossos Padrões

Exemplos de comportamento que contribuem para criar um ambiente positivo incluem:

- Usar linguagem acolhedora e inclusiva
- Ser respeitoso com pontos de vista e experiências divergentes
- Aceitar críticas construtivas gentilmente
- Focar no que é melhor para a comunidade
- Mostrar empatia com outros membros da comunidade

Exemplos de comportamento inaceitável por participantes incluem:

- Uso de linguagem ou imagens sexualizadas e atenção sexual indesejada
- Trolling, comentários insultuosos/depreciativos e ataques pessoais ou políticos
- Assédio público ou privado
- Publicação de informações privadas de outros sem permissão
- Outra conduta que possa ser razoavelmente considerada inapropriada em um contexto profissional

## Como Começar

### Pré-requisitos

- Node.js 18, 20 ou 22
- npm v10+
- Git

### Setup Local

1. **Faça um Fork** do repositório no GitHub
2. **Clone seu fork**
   ```bash
   git clone https://github.com/seu-username/legacy-samuka.git
   cd legacy-samuka
   ```

3. **Adicione upstream remote**
   ```bash
   git remote add upstream https://github.com/felipe-sbm/legacy-samuka.git
   ```

4. **Instale dependências**
   ```bash
   npm ci
   ```

5. **Crie uma branch**
   ```bash
   git checkout -b feature/minha-feature
   ```

6. **Inicie o servidor de desenvolvimento**
   ```bash
   npm run dev
   ```

## Tipos de Contribuições

### 🐛 Reportando Bugs

Antes de criar bug reports, por favor verifique a [issue list](https://github.com/felipe-sbm/legacy-samuka/issues) pois talvez o problema já tenha sido reportado.

Ao criar um bug report, inclua o máximo de detalhes possível:

- **Título descritivo** para a issue
- **Descrição exata do comportamento observado** e o que era esperado
- **Passos específicos para reproduzir** o problema
- **Screenshots e GIFs** se possível
- **Seu ambiente**: sistema operacional, versão Node.js, navegador, etc.

### 💡 Sugerindo Enhancements

Enhancement suggestions são rastreadas como GitHub issues. Ao criar uma enhancement suggestion, inclua:

- **Título descritivo**
- **Descrição detalhada** da feature sugerida
- **Exemplos de como** funcionaria
- **Por que seria útil** para usuários

### 📝 Pull Requests

- Preencha o template de PR completamente
- Siga os guias de estilo
- Inclua screenshots para mudanças na UI
- Termine todos os arquivos com uma nova linha
- Evite commits gigantes — mantenha PRs focadas

## Processo de Pull Request

1. **Atualize sua branch** com a última versão de `main`
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Rode testes e linting** localmente
   ```bash
   npm run lint:fix
   npm run test:unit
   npm run build
   ```

3. **Push sua branch**
   ```bash
   git push origin feature/minha-feature
   ```

4. **Abra a PR** no GitHub
   - Linke issues relacionadas: `Closes #123`
   - Descreva suas mudanças claramente
   - Aguarde review

5. **Address feedback** dos reviewers
   ```bash
   # Faça os ajustes
   git add .
   git commit -m "refactor: address review feedback"
   git push origin feature/minha-feature
   ```

6. **Merge**: Um mantenedor irá fazer o merge após aprovação

## Guias de Estilo

### Git Commit Messages

Use [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Type**: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`

**Scope**: `api`, `ui`, `db`, `auth`, `game`, etc. (opcional)

**Subject**: Imperativo, sem maiúscula inicial, sem ponto final

**Exemplos**:
```
feat(auth): add two-factor authentication
fix(ui): resolve button alignment issue in dashboard
docs: update contributing guide
chore(deps): upgrade drizzle-orm to v0.41
```

### TypeScript

- Use tipos explícitos, evite `any`
- Interfaces para contracts públicos, types para internos
- Documente tipos complexos com JSDoc

```typescript
/**
 * Calcula o score do usuário baseado em performance
 * @param attempt - Tentativa de quest do usuário
 * @returns Score calculado (0-100)
 */
export function calculateScore(attempt: QuestAttempt): number {
  // ...
}
```

### Svelte

- Use `<script lang="ts">` para type safety
- Reexporte do `lib/` com índices (`index.ts`)
- Nomes de componentes em PascalCase
- Props com tipos explícitos

```svelte
<script lang="ts">
  interface Props {
    title: string;
    disabled?: boolean;
  }

  let { title, disabled = false }: Props = $props();
</script>

<button {disabled}>
  {title}
</button>
```

### CSS/Tailwind

- Prefira classes Tailwind em vez de CSS customizado
- Use `@apply` apenas para padrões repetitivos
- Mantenha componentes localizados em `<style>`

```svelte
<style>
  :global(.prose) {
    @apply text-gray-700 leading-relaxed;
  }
</style>
```

### Testes

- Nomeie testes descritivamente: `test("deve calcular score corretamente")`
- Use AAA pattern: Arrange, Act, Assert
- Teste comportamento, não implementação

```typescript
test("calculateScore retorna 100 para resposta perfeita", () => {
  // Arrange
  const attempt = createMockAttempt({ correctAnswers: 10, total: 10 });

  // Act
  const score = calculateScore(attempt);

  // Assert
  expect(score).toBe(100);
});
```

### Documentação

- Escreva em Markdown
- Use inglês em comments de código
- Português em documentação pública (README, CONTRIBUTING, etc.)
- Mantenha linhas com até 100 caracteres

## Workflow de Desenvolvimento

```bash
# Desenvolvimento
npm run dev              # Inicia server + hot reload

# Antes de commitar
npm run lint:fix         # Formata + linting automático
npm run check            # TypeScript + Svelte check
npm run test:unit        # Roda testes

# Build final
npm run build            # Build de produção
npm run preview          # Preview do build

# Simular CI
npm run ci               # Lint + build + test:unit
```

## Estrutura de Código

```
src/
├── lib/
│   ├── components/    # Componentes Svelte
│   ├── server/        # Código server-side
│   ├── types/         # Interfaces TypeScript
│   ├── utils/         # Funções utilitárias
│   └── ...
├── routes/            # SvelteKit file-based routing
└── ...
```

**Não adicione código diretamente em `src/`. Use subpastas organizadas.**

## Issues Boas para Começar

Issues marcadas como `good-first-issue` são ideais para novos contribuidores. Confira a [lista](https://github.com/felipe-sbm/legacy-samuka/labels/good-first-issue).

## Dúvidas?

- 💬 Use [GitHub Discussions](https://github.com/felipe-sbm/legacy-samuka/discussions)
- 📧 Contate [@felipe-sbm](https://github.com/felipe-sbm)
- 🐛 Abra uma [issue](https://github.com/felipe-sbm/legacy-samuka/issues)

---

**Obrigado por contribuir! 🙏**
