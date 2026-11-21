# CentipedeOS

<p>
  <strong>Uma distribuição Linux baseada em Fedora para desenvolvimento, segurança ofensiva e laboratórios experimentais controlados.</strong>
</p>


O CentipedeOS é um projeto de distribuição Linux baseado em Fedora, utilizando Kickstart e pacotes RPM. Sua proposta é combinar liberdade operacional com ambientes isolados capazes de ser criados, usados, restaurados e descartados sem comprometer o sistema principal.

> “Leia mais em /docs/CentipedeOS.”

## Objetivo

Criar uma estação de trabalho que permita:

- Desenvolvimento de software com ferramentas e linguagens diversas.
- Pesquisa e experimentação em segurança cibernética.
- Execução de atividades potencialmente perigosas em ambientes isolados.
- Restauração rápida de estados conhecidos.
- Personalização por perfis e camadas.

O projeto não pretende substituir distribuições como Kali Linux. O objetivo é oferecer uma infraestrutura confortável para desenvolver software e suportar ferramentas de análise e segurança em uma mesma base.

## Filosofia

A filosofia **RFL — Reversibilidade, Flexibilidade e Liberdade** representa os três princípios principais do projeto:

- **Reversibilidade:** permitir voltar a estados conhecidos.
- **Flexibilidade:** não impor uma única forma de trabalhar ou uma única ferramenta.
- **Liberdade:** oferecer capacidade operacional sem bloquear atividades do usuário.

O sistema deve permitir que o usuário construa software, investigue sistemas, teste redes, analise código, teste código, e experimente configurações com segurança operacional, garantindo que ele possa personalizar completamente todo o sistema operacional.

## Documentação

- [Arquitetura em português](docs/CentipedeOS_BR.md)
- [Architecture in English](docs/CentipedeOS_EN.md)
- [Архитектура на русском](docs/CentipedeOS_RU.md)
- [中文架构文档](docs/CentipedeOS_中文.md)
- [Roteiro de implementação](docs/implementacao-mvp.md)
- [Guia de instalação](docs/instalacao.md)

## Estado atual

O projeto está na fase inicial. A arquitetura e parte da documentação já estão definidas, mas os scripts de build, Kickstarts, pacotes RPM e workflows ainda precisam ser implementados. O objetivo final é que essa distro tenha a possibilidade de se tornar um sistema operacional completo e personalizado, sendo essencialmente diferente do Linux tradicional. 

A prioridade atual é estabelecer uma primeira ISO funcional, apresentando protótipos e construindo uma comunidade sólida em cima do que temos atualmente. Quaisquer tipos de feedbacks são absolutamente bem-vindos. 


## Segurança

O CentipedeOS é projetado para executar atividades de segurança. Isso não torna essas atividades seguras por padrão. Entretanto, um dos objetivos principais do sistema é permitir que o usuário não tenha preocupações quanto ao estado do OS e de seus dados, criando uma barreira forte

## Licença

Consulte o arquivo [LICENSE](LICENSE) para obter os termos de uso.