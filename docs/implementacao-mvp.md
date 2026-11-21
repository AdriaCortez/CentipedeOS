# Guia de implementação inicial

Este documento transforma a arquitetura de referência do projeto em uma sequência prática de implementação.

## Situação atual

A arquitetura está documentada em `CentipedeOS_BR.md`, mas a maior parte da estrutura técnica ainda não foi implementada:

- Os scripts de build estão vazios. [] -> Deixar como 'afazer'
- Os Kickstarts estão vazios. [] -> Deixar como 'afazer'
- Os pacotes RPM estão vazios. [] -> Deixar como 'afazer'
- A configuração está vazia. [] -> Deixar como 'afazer'
- Os workflows estão vazios. [] -> Deixar como 'afazer'
- O `README.md` ainda não descreve o processo de uso. [] -> Deixar como 'afazer'

Por isso, a prioridade não é implementar todas as ferramentas das camadas da arquitetura. O objetivo inicial é produzir uma ISO Fedora inicializável, reproduzível e verificável em uma máquina virtual.

## Objetivo do primeiro marco

Ao final do primeiro marco, o projeto deve ser capaz de:

- Gerar uma ISO a partir de um Kickstart versionado.
- Inicializar essa ISO no QEMU.
- Instalar um ambiente mínimo ou básico.
- Executar um teste automatizado de inicialização.
- Permitir a reversão mínima de um ambiente experimental.

## Etapa 1: definir o perfil base mínimo

Começar pelo `kickstart/base.ks`.

Nesta etapa, definir:

- Uma versão específica do Fedora.
- Uma interface gráfica base, inicialmente GNOME.
- Idioma, teclado e fuso horário.
- Configuração mínima de rede.
- Usuário e credenciais iniciais.
- Configuração básica de disco.
- Um conjunto pequeno de ferramentas essenciais.

O objetivo é obter uma estação funcional, não um sistema completo. Pacotes e ferramentas opcionais devem ser adicionados após o processo básico de build estar estável.

O `kickstart/bare.ks` pode representar uma variante ainda menor da base. Os perfis `studio.ks` e `lab.ks` devem ser implementados posteriormente.

## Etapa 2: implementar o build da ISO

Preencher `build.sh` com o fluxo necessário para:

- Receber ou selecionar o arquivo Kickstart.
- Ler a configuração do projeto.
- Resolver os repositórios Fedora necessários.
- Construir a ISO.
- Salvar artefatos em um diretório previsível.
- Gravar logs detalhados.
- Exibir mensagens claras de sucesso ou falha.

O script deve aceitar parâmetros simples para perfis e destinos de saída. O processo precisa ser reproduzível antes que os pacotes específicos sejam ampliados.

## Etapa 3: criar o repositório local

Implementar `scripts/make-repo.sh` para:

- Organizar os pacotes RPM gerados pelo projeto.
- Criar a estrutura de metadados necessária.
- Permitir que o Kickstart ou os pacotes consumam esse repositório.
- Validar quais pacotes foram encontrados.

Os pacotes internos devem ser utilizados pelo build da ISO assim que o repositório estiver configurado.

## Etapa 4: testar o boot no QEMU

Implementar `scripts/qemu-test.sh` para validar automaticamente pelo menos os seguintes pontos:

- A ISO é inicializável.
- O instalador ou o sistema alcança o estado esperado.
- A interface gráfica ou o console fica disponível.
- O usuário consegue autenticar.
- `NetworkManager` está ativo.
- Não existem falhas críticas durante o boot.

O teste deve retornar uma saída clara e um código de erro apropriado. Ele pode ser ampliado depois para testes de rede, pacotes e serviços.

## Etapa 5: criar o primeiro pacote próprio

Começar pelo pacote `packages/centipede-config`.

Seu primeiro uso pode incluir:

- Arquivos de perfil do CentipedeOS.
- Configurações básicas do sistema.
- Perfis de desktop.
- Integrações iniciais com `systemd`.
- Estrutura básica do tema.

A configuração reutilizável deve ser empacotada em RPM. O Kickstart deve chamar esses componentes sem duplicar regras ou configurações em vários lugares.

## Etapa 6: implementar os componentes mínimos de sandbox

Antes de adicionar o catálogo completo de ferramentas de segurança, criar um laboratório mínimo que permita:

- Criar uma VM isolada.
- Utilizar uma rede virtual privada.
- Criar um snapshot básico.
- Restaurar o snapshot.
- Remover a VM e os recursos temporários.
- Validar que o estado do host não foi comprometido.

Os componentes iniciais estão previstos em:

- `systemd/centipede-sandbox.service`
- `packages/centipede-tools/src/your-distro-sandbox`
- `packages/centipede-tools/src/your-distro-reset`
- `packages/centipede-tools/src/your-distro-profile`

Para o MVP, não é necessário implementar todas as políticas da Camada 4 ao mesmo tempo. O núcleo deve fazer uma operação completa de criar, experimentar e restaurar.

## Etapa 7: criar o perfil de desenvolvimento

Depois que o build, o teste de boot e o pacote de configuração estiverem funcionando, implementar `kickstart/studio.ks`.

Adicionar inicialmente:

- Ferramentas essenciais de terminal.
- Editores ou IDEs selecionados.
- Compiladores e runtimes definidos pelo projeto.
- Containers e ambientes reproduzíveis.
- Git e ferramentas de integração.
- Ferramentas de depuração prioritárias.

Os pacotes opcionais devem seguir perfis diferentes, evitando que todas as linguagens e ferramentas sejam instaladas obrigatoriamente.

## Etapa 8: criar o perfil de laboratório

Com o núcleo de isolamento funcionando, implementar `kickstart/lab.ks`.

O perfil pode iniciar com um único modelo voltado a testes controlados. Esse laboratório deve incluir:

- Virtualização.
- Rede isolada.
- Limitação de recursos.
- Snapshots.
- Limitação de compartilhamento de arquivos.
- Restrição de dispositivos.
- Regras claras de acesso à rede.

Atividades ofensivas ou potencialmente perigosas devem permanecer dentro desses ambientes experimentais.

## Etapa 9: ampliar os pacotes RPM

O repositório próprio pode crescer depois da primeira ISO funcionar:

1. Pacote de configuração.
2. Tema e recursos visuais.
3. Ferramentas próprias do CentipedeOS.
4. Perfis de desktop.
5. Perfis de laboratório.
6. Pacotes de integração e automação.

Cada pacote deve possuir um propósito claro, depender do menor número possível de outros componentes e poder ser testado separadamente.

## Etapa 10: adicionar assinatura e CI/CD

Quando o fluxo local estiver estável:

- Configurar assinatura GPG dos pacotes.
- Implementar `scripts/sign-iso.sh`.
- Criar o workflow de build da ISO.
- Criar o workflow de teste de boot.
- Publicar a ISO e os logs somente após os testes mínimos.
- Tratar qualquer falha de boot como bloqueante.

Os workflows existentes podem ser preenchidos nesta ordem:

1. Build da ISO.
2. Teste no QEMU.
3. Assinatura dos artefatos.
4. Publicação do repositório e da ISO.

## Ordem recomendada

1. `base.ks` — sistema Fedora mínimo inicializável.
2. `build.sh` — ISO reproduzível.
3. `qemu-test.sh` — teste automatizado de boot.
4. `centipede-config` — identidade e configurações básicas.
5. `bare.ks` — variante mínima reutilizando o perfil base.
6. `centipede-tools` — reset e sandbox mínimos.
7. `studio.ks` — perfil de desenvolvimento.
8. `lab.ks` — perfil experimental isolado.
9. Repositório RPM, assinatura GPG e validação dos pacotes.
10. CI/CD para builds e testes.

## Critério de conclusão do MVP

O MVP deve ser considerado pronto somente quando for possível executar o fluxo completo sem intervenção manual intermediária:

```text
Kickstart -> Pacotes RPM -> ISO -> Instalação no QEMU -> Teste de boot -> Sandbox -> Reset
```

A maior lacuna atual não é a ausência de ferramentas da arquitetura, mas a ausência de uma primeira ISO confiável. Por isso, o projeto deve priorizar esse fluxo completo antes de aumentar o catálogo de aplicações das camadas de Desenvolvimento, Segurança e Laboratórios.
