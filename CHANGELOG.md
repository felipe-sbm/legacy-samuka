# Changelog

Todas as mudanças notáveis neste projeto serão documentadas neste arquivo.

O formato é baseado em [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
e este projeto segue [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Workflow de CI/CD com GitHub Actions
- `.env.example` para configuração de ambiente
- Scripts `lint:fix` e `ci` em `package.json`
- Suporte oficial para Node.js 18, 20 e 22
- Documentação melhorada de contribuição

### Fixed
- Vulnerabilidades de segurança em dependências (11 → 0 vulnerabilidades)
  - `@sveltejs/kit`: 0.0.30 → 2.49.0 (corrige CSRF/XSS)
  - `@sveltejs/adapter-vercel`: 0.0.3 → 5.0.0
  - Overrides: `cookie` (0.7.0), `esbuild` (>=0.25.0)

### Changed
- Estrutura do repositório para seguir boas práticas

## [0.0.1] - 2025-12-02

### Added
- Plataforma inicial de gamificação com 4 modos de jogo
- Suporte multilíngue (PT-BR, PT, ES, EN)
- Autenticação com Argon2
- Dashboard de progresso com gráficos (D3.js)
- Componentes matemáticos interativos (Mathlive, Desmos)
- Testes unitários e E2E
- Build otimizado com SvelteKit + Tailwind CSS v4
