# Changelog

Todas as mudanças relevantes do CentipedeOS serão documentadas neste arquivo.

Este projeto segue inicialmente o [Semantic Versioning](https://semver.org/lang/pt-BR/) no formato `MAJOR.MINOR.PATCH`.

## [0.1.0] - 2026-11-21

### Adicionado

- Estrutura inicial do repositório do projeto.
- Arquitetura geral do CentipedeOS organizada em cinco camadas:
  - Camada 0 — Núcleo.
  - Camada 1 — Estação de trabalho.
  - Camada 2 — Desenvolvimento.
  - Camada 3 — Segurança.
  - Camada 4 — Laboratórios.
- Diretrizes da filosofia RFL — Reversibilidade, Flexibilidade e Liberdade.
- Documentação inicial da arquitetura em português, inglês, russo e chinês.
- Estrutura preparada para Kickstarts de perfis `bare`, `base`, `studio` e `lab`.
- Estrutura preparada para pacotes RPM de configuração, tema e ferramentas.
- Estrutura preparada para build da ISO, repositório RPM, testes no QEMU e assinatura.
- Estrutura preparada para integrações com systemd e políticas SELinux.
- [Guia de implementação inicial](docs/implementacao-mvp.md), com roteiro detalhado do MVP.
- README principal em português para apresentação do projeto no GitHub.
- Regras iniciais no `.gitignore` para artefatos de build, máquinas virtuais, caches, credenciais e arquivos temporários.

### Documentação

- Criado o documento [Guia de implementação inicial](docs/implementacao-mvp.md).
- Criado o README principal com:
  - Objetivo do projeto.
  - Filosofia RFL.
  - Visão geral da arquitetura.
  - Perfis previstos.
  - Estrutura do repositório.
  - Caminho de implementação do MVP.
  - Links para a documentação disponível.
  - Estado atual e princípios de segurança.

### Segurança

- Definidas regras para não versionar chaves privadas, credenciais, arquivos `.env` e diretórios de segredos.
- Definidas regras para não versionar artefatos de build, ISOs, RPMs, imagens de VM e snapshots.
- Adicionada orientação para executar atividades ofensivas exclusivamente em ambientes isolados e autorizados.

### Estado inicial

Esta versão estabelece a documentação, os objetivos e a estrutura inicial do projeto. Os scripts de build, Kickstarts, pacotes RPM e workflows permanecem pendentes de implementação até serem preenchidos nos marcos seguintes.