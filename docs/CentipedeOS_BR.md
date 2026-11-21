# CentipedeOS

CentipedeOS (ou Centipede Operational System) é um projeto que visa a criação, a curto-médio prazo, de uma distribuição Linux baseada em Fedora com Kickstart e pacotes RPM.

## Filosofia

> "Construa tudo… Ou destrua! O que você achar mais divertido." – Reversibilidade, flexibilidade e liberdade. (RFL)

## Qual o objetivo?

O objetivo inicial do CentipedeOS é ser flexível e operável para desenvolvedores de software e entusiastas de cibersegurança, tornando o ambiente acessível e seguro. Então, a distribuição deve…

- Atuar com ferramentas que facilitem a vida do dev, do Júnior ao Arquiteto de Software;
- Permitir a pesquisa e experimentação em segurança cibernética.

Oferecendo, assim, uma estação de trabalho que permita o desenvolvimento de aplicações e, ao mesmo tempo, crie ambientes isolados para experimentos de segurança, incluindo experimentos potencialmente destrutivos do SO até o hardware, tornando a liberdade operacional a ideia central da filosofia do Centipede, criando assim a caixa de areia da engenharia da computação: o usuário pode construir software, desmontar sistemas, criar redes, testar código hostil, experimentar configurações – e depois ter a liberdade de voltar para um estado conhecido pré-estabelecido.

A ideia aqui é não bloquear as ações do usuário, como outros sistemas operacionais, como Windows e macOS, fazem, e sim dar a liberdade de escolha para que o usuário possa escolher entre não fazer e fazer o que ele quer com segurança operacional, criando automaticamente um ambiente isolado para seus testes.

## Contextualização

O sistema tem também, por objetivo primário, trazer uma nova solução para aqueles que têm preferência por Kali Linux. A documentação do Kali explicita que ele foi projetado para pentest, e já suporta ambientes de execução como Bare Metal, VM, Containers, cloud, WSL, etc. É importante ressaltar que o Centipede não tem pretensão de substituí-lo, e sim criar uma infraestrutura que seja confortável e, ao mesmo tempo, ofereça o suporte necessário para suportar todo o arsenal do Kali.

## Simbologia

"Centipede" é o nome em inglês para "Centopeia". Centopeias são artrópodes, carnívoras, e muitas espécies são grandes e peçonhentas. A ideia de trazer um quilópode tão perigoso é representar que o sistema pode ser igualmente adaptativo e modular e, do mesmo jeito que a centopeia possui veneno e mecanismos capazes de imobilizar presas, a distro dispõe de ferramentas capazes de realizar operações potencialmente agressivas.

---

## Divisão de ambientes

A divisão de ambientes, para esse caso em específico, seria uma peça fundamental da arquitetura do SO, afinal, quanto mais liberdade é oferecida ao usuário, mais sofisticado é necessário o mecanismo que permite a segurança de seu ambiente. E isso também combina com a robustez. No caso, a robustez é a capacidade de permitir a experimentação agressiva sem transformar uma falha local em uma falha sistêmica. O sistema também **NÃO** deve impor uma única forma de trabalhar.

Todos os usuários podem utilizar ferramentas diversas utilizando a mesma base. A personalização será feita em camadas, por exemplo:

---

## Camada 0 — Núcleo (Core)

**Base do sistema operacional**

Responsável por fornecer os mecanismos fundamentais para o funcionamento da distribuição. Todas as demais camadas dependem dela, direta ou indiretamente.

### 0.1. Kernel e gerenciamento de hardware

Responsável pela comunicação entre o sistema operacional e os componentes físicos da máquina.

- Gerenciamento de CPU, memória RAM e processos.
- Gerenciamento de dispositivos USB, PCI e periféricos.
- Gerenciamento de drivers e módulos do kernel.
- Controle de energia e estados de suspensão.
- Suporte à virtualização por hardware.
- Gerenciamento de IOMMU para controle de acesso a dispositivos.

**Tecnologias:** Linux Kernel, KVM, udev, systemd-udevd, firmware e microcode.

### 0.2. Gerenciamento de serviços e inicialização

Responsável pela inicialização do sistema e pelo controle dos serviços executados em segundo plano.

- Inicialização e encerramento do sistema.
- Gerenciamento de serviços e daemons.
- Controle de dependências entre serviços.
- Gerenciamento de usuários, grupos e sessões.
- Recuperação e reinicialização de serviços.
- Execução de tarefas programadas.

**Tecnologias:** systemd, systemd-logind, systemd-tmpfiles e systemd-resolved.

### 0.3. Gerenciamento de rede

Responsável por fornecer conectividade e controlar a comunicação entre o sistema e outras redes.

- Gerenciamento de interfaces Ethernet e Wi-Fi.
- Configuração de endereços IPv4 e IPv6.
- Gerenciamento de DNS e DHCP.
- Roteamento de pacotes.
- Gerenciamento de VPNs.
- Criação e gerenciamento de interfaces virtuais.
- Controle de tráfego e regras de firewall.

**Tecnologias:** NetworkManager, iproute2, nftables, firewalld e WireGuard.

### 0.4. Gerenciamento de armazenamento

Responsável pelo controle dos dispositivos de armazenamento e pela organização dos dados.

- Gerenciamento de discos e partições.
- Montagem e desmontagem de sistemas de arquivos.
- Criptografia de volumes.
- Gerenciamento de volumes lógicos.
- Controle de integridade dos dados.
- Gerenciamento de permissões e cotas de armazenamento.
- Suporte a snapshots e mecanismos de recuperação.

**Tecnologias:** LUKS, LVM, Btrfs, XFS, ext4 e Stratis.

### 0.5. Segurança do sistema

Responsável por fornecer os mecanismos de proteção e controle de acesso utilizados pelas demais camadas.

- Controle de privilégios e permissões.
- Isolamento de processos.
- Controle de acesso obrigatório (MAC).
- Gerenciamento de Linux Capabilities.
- Auditoria de eventos.
- Proteção de credenciais.
- Verificação de integridade.
- Suporte a Secure Boot.

**Tecnologias:** SELinux, seccomp, Linux Capabilities, auditd, PAM, polkit e Secure Boot.

### 0.6. Gerenciamento de pacotes e atualizações

Responsável pela instalação, manutenção e atualização dos componentes do sistema.

- Instalação e remoção de pacotes.
- Gerenciamento de dependências.
- Gerenciamento de repositórios.
- Verificação de assinaturas e integridade.
- Controle de versões.
- Histórico de atualizações.
- Possibilidade de reversão de alterações, conforme os mecanismos adotados.

**Tecnologias:** RPM, DNF5, repositórios próprios e assinaturas GPG.

### 0.7. Logs, diagnóstico e observabilidade

Responsável por registrar eventos e disponibilizar informações sobre o comportamento do sistema.

- Registro de eventos do sistema.
- Monitoramento de serviços.
- Identificação de falhas.
- Registro de inicialização e encerramento.
- Auditoria de alterações.
- Coleta de informações para diagnóstico.

**Tecnologias:** journald, auditd e systemd-coredump.

### 0.8. Compatibilidade e integração

Responsável por fornecer interfaces e bibliotecas necessárias para a comunicação entre os componentes do sistema.

- Bibliotecas compartilhadas.
- Comunicação entre serviços.
- Integração entre aplicações e componentes do sistema.
- Gerenciamento de certificados.
- Configurações regionais e de horário.

**Tecnologias:** glibc, D-Bus, OpenSSL e componentes do ecossistema Fedora.

---

## Camada 1 — Estação de trabalho (Workstation)

**Ambiente de interação**

Responsável por fornecer a interface de utilização da distribuição. É a camada com a qual o usuário interage diretamente durante suas atividades cotidianas.

### 1.1. Interface gráfica

Responsável pela apresentação visual e pela interação com o sistema.

- Gerenciamento de janelas.
- Organização de áreas de trabalho.
- Temas, ícones e fontes.
- Configuração de múltiplos monitores.
- Atalhos de teclado.
- Recursos de acessibilidade.
- Personalização da aparência.

**Tecnologias:** GNOME, KDE Plasma, Xfce, Wayland, X11, Mutter e KWin.

### 1.2. Terminal e interpretadores de comandos

Responsável por disponibilizar interfaces de linha de comando para interação com o sistema.

- Emuladores de terminal.
- Interpretadores de comandos (shells).
- Gerenciamento de sessões.
- Histórico de comandos.
- Autocompletar e sugestões.
- Multiplexação de sessões.
- Personalização de prompts.

**Tecnologias:** Bash, Zsh, Fish, Kitty, Alacritty, tmux e Starship.

### 1.3. Aplicações essenciais

Conjunto de aplicações necessárias para as atividades cotidianas.

- Navegadores.
- Gerenciadores de arquivos.
- Editores de texto.
- Aplicações de documentos.
- Ferramentas de compactação.
- Gerenciadores de senhas.
- Clientes de e-mail e comunicação.

### 1.4. Gerenciamento da experiência do usuário

Responsável por centralizar as configurações e preferências da estação de trabalho.

- Gerenciamento de perfis de desktop.
- Configuração de atalhos.
- Definição de aplicações padrão.
- Controle de inicialização automática.
- Sincronização de configurações.
- Gerenciamento de preferências visuais e comportamentais.

**Tecnologias:** GTK, Qt, dconf, gsettings e KDE KConfig.

---

## Camada 2 — Desenvolvimento (Development)

**Ambiente de desenvolvimento**

Responsável por disponibilizar ferramentas, bibliotecas, linguagens e serviços necessários ao desenvolvimento de software.

A proposta é oferecer uma estação de desenvolvimento abrangente, permitindo trabalhar com diferentes tecnologias sem exigir que todas estejam permanentemente instaladas ou em execução.

### 2.1. Linguagens de programação e toolchains

- Python.
- C e C++.
- Rust.
- Go.
- Java.
- JavaScript e TypeScript.
- PHP.
- Ruby.
- .NET.

Inclui compiladores, interpretadores, linkers, sistemas de build e ferramentas de gerenciamento de versões.

**Tecnologias:** GCC, Clang/LLVM, Rustup, Go, OpenJDK, Node.js, .NET SDK, CMake, Make e Ninja.

### 2.2. IDEs e editores

- Ambientes integrados de desenvolvimento.
- Editores de código.
- Extensões e plugins.
- Integração com controle de versão.
- Suporte a Language Server Protocol (LSP).
- Depuração integrada.

**Tecnologias:** VS Code, VSCodium, Neovim, Emacs, JetBrains IDEs e clangd.

### 2.3. Depuração e testes

- Depuração de aplicações.
- Análise de consumo de memória.
- Identificação de vazamentos.
- Profiling de aplicações.
- Testes unitários.
- Testes de integração.
- Testes de carga.
- Análise de cobertura de testes.

**Tecnologias:** GDB, LLDB, Valgrind, AddressSanitizer, perf, pytest e GoogleTest.

### 2.4. Containers e ambientes de desenvolvimento

- Criação e gerenciamento de containers.
- Gerenciamento de imagens.
- Volumes e redes.
- Ambientes de desenvolvimento descartáveis.
- Ambientes reproduzíveis.
- Orquestração local.
- Integração com ferramentas de desenvolvimento.

**Tecnologias:** Podman, Buildah, Skopeo, Docker Compose e Distrobox.

### 2.5. DevOps e infraestrutura

- Automação de infraestrutura.
- Integração e entrega contínua (CI/CD).
- Gerenciamento de configurações.
- Orquestração de containers.
- Provisionamento de ambientes.
- Automação de deploy.

**Tecnologias:** Ansible, Terraform/OpenTofu, Kubernetes, Helm, Jenkins e GitLab Runner.

### 2.6. Bancos de dados e mensageria

- Bancos de dados relacionais.
- Bancos de dados não relacionais.
- Bancos de dados locais.
- Sistemas de cache.
- Filas de mensagens.
- Sistemas de comunicação entre serviços.

**Tecnologias:** PostgreSQL, MariaDB, SQLite, MongoDB, Redis, RabbitMQ e Kafka.

### 2.7. Desenvolvimento em nuvem

- Gerenciamento de serviços em nuvem.
- Interfaces de linha de comando para provedores.
- SDKs de serviços.
- Emulação de serviços de nuvem.
- Integração com infraestrutura remota.

**Tecnologias:** AWS CLI, Azure CLI, Google Cloud CLI, MinIO e LocalStack.

### 2.8. Inteligência artificial e aprendizado de máquina

- Frameworks de aprendizado de máquina.
- Execução de modelos locais.
- Gerenciamento de modelos.
- Ferramentas de inferência.
- Desenvolvimento de aplicações baseadas em IA.

**Tecnologias:** PyTorch, TensorFlow, Hugging Face, Ollama e ONNX Runtime.

A instalação e execução desses componentes podem ser opcionais, evitando consumo desnecessário de armazenamento, memória e processamento.

### 2.9. Documentação e produtividade

- Documentação de linguagens e bibliotecas.
- Geração automática de documentação.
- Diagramas de arquitetura.
- Gerenciamento de dependências.
- Ferramentas de produtividade.

**Tecnologias:** Zeal, DevDocs, Doxygen, Sphinx, MkDocs e Mermaid.

---

## Camada 3 — Segurança (Security)

**Ferramentas de segurança cibernética**

Responsável por disponibilizar ferramentas especializadas em análise, auditoria, investigação e avaliação de segurança.

Diferentemente da Camada 0, que fornece os mecanismos de proteção do sistema operacional, esta camada disponibiliza ferramentas que utilizam esses mecanismos e permitem realizar atividades de segurança.

### 3.1. Análise de redes

- Captura e análise de pacotes.
- Inspeção de protocolos.
- Descoberta de dispositivos.
- Mapeamento de redes.
- Análise de tráfego.
- Monitoramento de comunicações.

**Tecnologias:** Wireshark, TShark, tcpdump, Zeek, Suricata e Nmap.

### 3.2. Segurança de aplicações web

- Análise de vulnerabilidades web.
- Testes de segurança em APIs.
- Inspeção de requisições HTTP.
- Identificação de configurações inadequadas.
- Avaliação de mecanismos de autenticação.

**Tecnologias:** OWASP ZAP, Burp Suite e Nikto.

### 3.3. Pentest e segurança ofensiva

- Reconhecimento de sistemas.
- Enumeração de serviços.
- Avaliação de vulnerabilidades.
- Testes de configuração.
- Validação de mecanismos de proteção.
- Simulação de ataques em ambientes autorizados.

**Tecnologias:** Metasploit, Nmap, sqlmap e ferramentas do ecossistema OWASP.

### 3.4. Engenharia reversa

- Análise de arquivos binários.
- Desmontagem de executáveis.
- Descompilação.
- Análise de código.
- Depuração de baixo nível.
- Investigação do comportamento de aplicações.

**Tecnologias:** Ghidra, Radare2, Cutter, Binary Ninja e GDB.

### 3.5. Análise de malware

- Análise estática.
- Análise dinâmica.
- Identificação de indicadores de comprometimento (IOCs).
- Investigação de comportamento.
- Análise de persistência.
- Identificação de mecanismos de comunicação.

**Tecnologias:** YARA, capa, Ghidra e Volatility.

> A execução de amostras potencialmente perigosas deve ocorrer na Camada 4, dentro de ambientes isolados.

### 3.6. Forense digital

- Aquisição de evidências.
- Análise de discos.
- Recuperação de arquivos.
- Investigação de sistemas de arquivos.
- Análise de memória.
- Construção de linhas do tempo.
- Investigação de logs.

**Tecnologias:** Autopsy, The Sleuth Kit, Volatility, Plaso e Wireshark.

### 3.7. Segurança de sistemas e infraestrutura

- Auditoria de configurações.
- Análise de permissões.
- Avaliação de hardening.
- Identificação de serviços expostos.
- Verificação de conformidade.
- Análise de políticas de segurança.

**Tecnologias:** Lynis, OpenSCAP e osquery.

### 3.8. Segurança de aplicações e código

- Análise estática de código (SAST).
- Análise de dependências (SCA).
- Identificação de credenciais expostas.
- Verificação de vulnerabilidades.
- Inspeção de imagens de containers.
- Integração com pipelines de desenvolvimento.

**Tecnologias:** Semgrep, Gitleaks, Trivy, Grype e OWASP Dependency-Check.

### 3.9. Monitoramento e resposta a incidentes

- Monitoramento de atividades.
- Detecção de comportamentos suspeitos.
- Correlação de eventos.
- Investigação de incidentes.
- Monitoramento de processos.
- Coleta de evidências.

**Tecnologias:** Wazuh, osquery, Falco e Elastic Stack.

### 3.10. Criptografia e identidade

- Gerenciamento de chaves criptográficas.
- Criação e validação de certificados.
- Gerenciamento de identidades.
- Infraestrutura de chaves públicas (PKI).
- Proteção de segredos.
- Autenticação multifator.

**Tecnologias:** OpenSSL, GnuPG, age e Vault.

---

## Camada 4 — Laboratórios (Labs)

**Ambientes experimentais isolados**

Responsável por disponibilizar a infraestrutura necessária para criar, executar, monitorar, restaurar e destruir ambientes experimentais.

Esta camada representa um dos principais diferenciais da distribuição: permitir que atividades potencialmente perigosas sejam executadas em ambientes controlados, reduzindo a possibilidade de comprometimento do sistema principal.

### 4.1. Virtualização

- Criação de máquinas virtuais.
- Gerenciamento de CPU e memória.
- Gerenciamento de discos virtuais.
- Emulação de hardware.
- Clonagem de máquinas.
- Virtualização aninhada (nested virtualization).
- Gerenciamento de dispositivos virtuais.

**Tecnologias:** KVM, QEMU e libvirt.

### 4.2. Redes virtuais

- Criação de redes isoladas.
- Gerenciamento de interfaces virtuais.
- Segmentação de redes.
- Simulação de topologias.
- Criação de roteadores e switches virtuais.
- Controle de comunicação entre máquinas.
- Simulação de latência e perda de pacotes.

**Tecnologias:** libvirt networks, Linux bridges, Open vSwitch, nftables e tc.

### 4.3. Snapshots e gerenciamento de estados

- Criação de pontos de restauração.
- Restauração de estados anteriores.
- Clonagem de ambientes.
- Comparação de estados.
- Versionamento de configurações.
- Preservação de estados experimentais.

**Tecnologias:** snapshots do QEMU/libvirt e Btrfs.

> É importante ressaltar que snapshots não substituem backups. Eles permitem retornar a determinados estados, mas não garantem proteção contra perda ou corrupção do armazenamento físico.

### 4.4. Ambientes isolados

- Criação de ambientes descartáveis.
- Separação entre host e ambiente experimental.
- Isolamento de sistemas de arquivos.
- Controle de compartilhamento de arquivos.
- Restrição de acesso a dispositivos.
- Gerenciamento de credenciais independentes.
- Limitação de recursos computacionais.

**Tecnologias:** Podman, KVM, namespaces, cgroups e SELinux.

### 4.5. Templates e provisionamento

- Modelos de máquinas virtuais.
- Imagens-base.
- Configurações predefinidas.
- Instalação automatizada.
- Provisionamento de redes.
- Reprodução de ambientes experimentais.
- Criação de laboratórios sob demanda.

**Tecnologias:** cloud-init, Kickstart, Ansible, Packer e imagens OCI.

### 4.6. Laboratórios especializados

Possibilidade de disponibilizar ambientes previamente configurados para diferentes áreas de segurança e desenvolvimento.

- Web Security Lab.
- Network Security Lab.
- Malware Analysis Lab.
- Reverse Engineering Lab.
- Digital Forensics Lab.
- Red Team Lab.
- Blue Team Lab.
- Vulnerable Applications Lab.
- OS Research Lab.
- Kernel Development Lab.

Cada laboratório pode possuir ferramentas, configurações de rede, políticas de acesso e recursos computacionais específicos.

### 4.7. Simulação de ameaças e ataques

- Simulação de tráfego malicioso.
- Simulação de comprometimento de sistemas.
- Testes de exploração em ambientes controlados.
- Simulação de indisponibilidade.
- Simulação de movimentação entre máquinas virtuais.
- Testes de detecção e resposta.
- Investigação de comportamentos semelhantes aos de malware.

> Essas atividades devem ser executadas exclusivamente em ambientes experimentais devidamente isolados e autorizados.

### 4.8. Observabilidade dos laboratórios

- Monitoramento de CPU e memória.
- Monitoramento de tráfego de rede.
- Registro de processos.
- Coleta de eventos.
- Histórico de atividades.
- Preservação de evidências.
- Análise do comportamento dos ambientes.

**Tecnologias:** journald, Wireshark, tcpdump, Prometheus e Grafana.

### 4.9. Recuperação e descarte

- Restauração de snapshots.
- Destruição de ambientes.
- Reconstrução automatizada.
- Limpeza de discos virtuais.
- Remoção de redes temporárias.
- Preservação de evidências antes do descarte.
- Validação do estado do host após os experimentos.

### 4.10. Políticas de segurança dos laboratórios

- Controle de acesso ao sistema principal.
- Controle de acesso à rede local.
- Restrição de acesso à Internet.
- Gerenciamento de pastas compartilhadas.
- Controle de dispositivos USB.
- Controle de clipboard.
- Restrição de comunicação entre laboratórios.
- Limitação de recursos computacionais.

---

> **Importante ressaltar:** esse modelo de arquitetura não é absoluto e talvez possa não condizer absolutamente com o objetivo final, então há uma possibilidade de este documento ser alterado de acordo com o que for necessário.
