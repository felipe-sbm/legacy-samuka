# Legacy - AULA ZERO

> Uma plataforma Open Source interativa de aprendizado gamificado.

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-green?logo=nodejs)](https://nodejs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0%2B-blue?logo=typescript)](https://www.typescriptlang.org)
[![SvelteKit](https://img.shields.io/badge/SvelteKit-2.49-red?logo=svelte)](https://kit.svelte.dev)
[![License](https://img.shields.io/badge/license-MIT-green)](#-licença)
[![Open Source](https://img.shields.io/badge/Open%20Source-Yes-brightgreen)](https://opensource.org)

## Sobre

A **Legacy** é uma aplicação web **open source** que oferece uma experiência de aprendizado gamificada e interativa. A plataforma permite que estudantes pratiquem habilidades matemáticas através de diferentes modos de jogo (Velocidade, Sabedoria, Poder, Resistência) com feedback visual em tempo real, ranking de pontuação e progresso rastreado.

Desenvolvido com as melhores práticas de engenharia de software, o projeto utiliza tecnologias modernas e está 100% pronto para produção.

## Características Principais

- 🎮 **Modos de Jogo Múltiplos**: Velocidade, Sabedoria, Poder e Resistência
- 📊 **Dashboard de Progresso**: Rastreie seu desempenho com gráficos em tempo real
- 🌍 **Suporte Multilíngue**: Português (BR/PT), Espanhol e Inglês via Paraglide.js
- 🔐 **Autenticação Segura**: Implementada com Argon2 para hashing de senhas
- 📱 **Responsivo**: Interface adaptável para desktop, tablet e mobile
- ⚡ **Performance Otimizada**: Build rápido com Vite e Tailwind CSS v4
- 🧪 **Testes Completos**: Unit tests (Vitest) e E2E tests (Playwright)
- ♿ **Acessível**: Segue padrões WCAG e boas práticas de a11y
- 🔄 **CI/CD Integrado**: GitHub Actions para testes, linting e build automático

## 🛠️ Stack Tecnológico

### Frontend
- **[SvelteKit](https://kit.svelte.dev)** (v2.49) - Framework full-stack reativo
- **[Svelte](https://svelte.dev)** (v5) - Componentes interativos
- **[TypeScript](https://www.typescriptlang.org)** - Type safety
- **[Tailwind CSS](https://tailwindcss.com)** (v4) - Estilização utilitária
- **[Skeleton](https://www.skeleton.dev)** - Componentes UI
- **[Lucide Icons](https://lucide.dev)** - Ícones SVG

### Backend & Data
- **[Node.js](https://nodejs.org)** (18–22) - Runtime
- **[Drizzle ORM](https://orm.drizzle.team)** (v0.40) - ORM type-safe
- **[LibSQL](https://github.com/tursodatabase/libsql)** - SQLite serverless
- **[Argon2](https://github.com/RustCrypto/passwords)** - Hashing de senhas

### Dev & Testing
- **[Vite](https://vitejs.dev)** (v7) - Build tool
- **[Vitest](https://vitest.dev)** (v3) - Unit tests
- **[Playwright](https://playwright.dev)** (v1.53) - E2E tests
- **[ESLint](https://eslint.org)** (v9) - Linting
- **[Prettier](https://prettier.io)** - Code formatting

## Quick Start

### Pré-requisitos

- **Node.js**: versão 18, 20 ou 22 (use [nvm](https://github.com/nvm-sh/nvm) ou [asdf](https://asdf-vm.com) para gerenciar versões)
- **npm**: v10+ (incluído no Node.js)
- **Git**: para clonar o repositório

### Instalação

1. **Clone o repositório**
   ```bash
   git clone https://github.com/felipe-sbm/legacy-samuka.git
   cd legacy-samuka
   ```

2. **Instale as dependências**
   ```bash
   npm ci
   ```
   > Use `npm ci` (clean install) em vez de `npm install` para garantir versões exatas em CI/produção.

3. **Configure variáveis de ambiente**
   ```bash
   cp .env.example .env
   # Edite .env e preencha os valores necessários
   ```

4. **Inicie o servidor de desenvolvimento**
   ```bash
   npm run dev
   ```
   A aplicação estará disponível em `http://localhost:5173`.

## Comandos Disponíveis

### Desenvolvimento
```bash
npm run dev          # Inicia servidor Vite em modo dev
npm run build        # Build para produção
npm run preview      # Preview do build de produção
npm run start        # Roda o servidor de produção
```

### Code Quality
```bash
npm run check        # Svelte check + TypeScript check
npm run check:watch  # Check em modo watch
npm run lint         # Prettier check + ESLint
npm run lint:fix     # Corrige issues de formatting e linting
npm run format       # Formata código com Prettier
```

### Testes
```bash
npm run test:unit    # Roda testes unitários com Vitest
npm run test:e2e     # Roda testes end-to-end com Playwright
npm run test         # Roda todos os testes
npm run ci           # Simula pipeline de CI (lint + build + test:unit)
```

### Database
```bash
npm run db:push      # Push schema para database
npm run db:migrate   # Executa migrations
npm run db:studio    # Abre Drizzle Studio (UI para gerenciar BD)
```

## 📁 Estrutura do Projeto

```
src/
├── lib/
│   ├── components/       # Componentes Svelte reutilizáveis
│   ├── server/          # Lógica de servidor (auth, db)
│   ├── types/           # TypeScript interfaces globais
│   ├── utils/           # Funções utilitárias (math, text, etc.)
│   ├── game/            # Lógica de gamificação
│   ├── pages/           # Componentes de página reutilizáveis
│   ├── modals/          # Componentes de modal
│   ├── snippets/        # Snippets Svelte para template reuse
│   ├── Tasks/           # Componentes de tarefas/quests
│   ├── data/            # Dados estáticos (livros, capítulos)
│   └── ...
├── routes/              # SvelteKit routes (file-based routing)
│   ├── (app)/          # Layout principal da aplicação
│   ├── backup/         # Rotas em backup/arquivadas
│   └── ...
├── hooks.ts            # SvelteKit hooks (client-side)
├── hooks.server.ts     # SvelteKit hooks (server-side)
└── app.html            # HTML base da aplicação

static/                 # Arquivos estáticos (fonts, áudio, imagens)
e2e/                    # Testes E2E com Playwright
.github/workflows/      # GitHub Actions CI/CD
```

## Contribuindo

Contributions are welcome! Este é um projeto **open-source** e aceitamos pull requests de toda a comunidade.

### Como Contribuir

1. **Faça um Fork** do repositório
   ```bash
   # No GitHub, clique em "Fork"
   ```

2. **Clone seu fork**
   ```bash
   git clone https://github.com/seu-username/legacy-samuka.git
   cd legacy-samuka
   ```

3. **Crie uma branch para sua feature**
   ```bash
   git checkout -b feature/minha-feature
   # ou para fix
   git checkout -b fix/meu-bugfix
   ```

4. **Faça alterações e commit**
   ```bash
   npm run lint:fix        # Corrige formatting
   git add .
   git commit -m "feat: adiciona nova feature"
   ```
   > Siga convenções [Conventional Commits](https://www.conventionalcommits.org)

5. **Push para seu fork**
   ```bash
   git push origin feature/minha-feature
   ```

6. **Abra um Pull Request**
   - Descreva sua mudança claramente
   - Linke issues relacionadas (ex: `Closes #123`)
   - Aguarde review dos mantenedores

### Diretrizes de Contribuição

- **Código**: Siga o style definido em `.prettierrc` e `eslint.config.js`
- **Testes**: Adicione testes para novas features (use `npm run test:unit`)
- **Commits**: Use mensagens descritivas em inglês
- **PRs**: Keep them focused e pequenas quando possível
- **Documentation**: Atualize README se necessário

## 🐛 Reportando Issues

Encontrou um bug? Abra uma [issue](https://github.com/felipe-sbm/legacy-samuka/issues) com:
- Descrição clara do problema
- Passos para reproduzir
- Comportamento esperado vs. observado
- Screenshots (se aplicável)
- Versão do Node.js e SO

## Licença

Este projeto é licenciado sob a **MIT License** — veja o arquivo [LICENSE](LICENSE) para detalhes.

### MIT License Summary
Você é livre para:
- Usar comercialmente
- Modificar
- Distribuir
-  Usar privadamente

Com a única condição:
- Incluir a licença e copyright!

## Suporte

- **Documentação**: [Veja nossa wiki](https://github.com/felipe-sbm/legacy-samuka/wiki) (quando disponível)
- **Discussions**: [GitHub Discussions](https://github.com/felipe-sbm/legacy-samuka/discussions)
- **Issues**: [GitHub Issues](https://github.com/felipe-sbm/legacy-samuka/issues)

## Roadmap

- [ ] Dashboard administrativo
- [ ] API pública para integração
- [ ] Mobile app nativa (React Native)
- [ ] Suporte a mais idiomas
- [ ] Sistema de badges e achievements
- [ ] Multiplayer/Competitive mode

## Autores & Mantenedores

- ([@YZhLu](https://github.com/YZhLu/)) - Creator & Lead Maintainer
- ([@felipe-sbm](https://github.com/felipe-sbm)) - Frontend Developer

## Changelog

Veja [CHANGELOG.md](CHANGELOG.md) para histórico de mudanças em cada release.

## Links Úteis
- [SvelteKit Documentation](https://kit.svelte.dev)
- [Drizzle ORM Guide](https://orm.drizzle.team)
- [Tailwind CSS v4](https://tailwindcss.com)
- [GitHub Open Source Guide](https://opensource.guide)

---

**Made with ❤️ for the Open Source community**
