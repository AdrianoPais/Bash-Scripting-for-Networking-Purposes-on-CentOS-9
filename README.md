Este repositório contém um conjunto de scripts Bash desenvolvidos para automatizar a instalação, configuração e segurança de serviços críticos numa infraestrutura de rede baseada em CentOS Stream 9. [cite_start]O foco principal é a eficiência operacional e a robustez da segurança através de automação.  

# Resumo do Projeto

O projeto consiste na criação de uma infraestrutura segmentada entre WAN e LAN, onde um servidor central gere a conectividade, segurança e transferência de ficheiros.  

FTP (VSFTPD): Configuração de um servidor de transferência de ficheiros seguro, suportando acessos anónimos e de utilizadores locais.   
SSH (Secure Shell): Implementação de acesso remoto seguro com endurecimento (hardening) de políticas de acesso.
DHCP (ISC): Gestão de endereçamento dinâmico para a rede local (LAN Segment) usando o motor tradicional ISC DHCP.  
Segurança Integrada: Utilização de firewalld, SELinux em modo enforcing e proteção contra intrusões com fail2ban.  

## Funcionalidades Principais
Script SSH

- Alteração da porta padrão para a porta 2222 para reduzir ataques de força bruta.
- Desativação do login direto como utilizador root.
- Configuração de um Banner de aviso legal para acessos não autorizados.
- Integração com Fail2Ban para monitorização de logs e banimento automático de IPs suspeitos.

Script FTP (VSFTPD)

- Instalação e ativação do serviço VSFTPD.
- Configuração de acesso para utilizadores locais com permissões de escrita.
- Ativação de Modo Passivo para compatibilidade com firewalls.
- Ajuste automático de booleanos do SELinux para permitir a transferência de ficheiros sem comprometer a segurança do sistema.

Script DHCP

- Atribuição de endereços IP estáticos à interface de rede local via nmcli.
- Configuração do escopo (pool) de IPs, gateway, máscara de rede e servidores DNS para os clientes.
- Ativação de IP Forwarding e regras de Masquerading (NAT) para fornecer acesso à Internet à rede interna.   

## Tecnologias Utilizadas

SO: CentOS Stream 9.   
Linguagem: Bash Scripting.  
Serviços: VSFTPD, OpenSSH, ISC DHCPD.
Segurança: Fail2Ban, Firewalld, SELinux (Enforcing).  
Rede: NetworkManager (nmcli), Iptables (NAT).  

## Como Utilizar

1. Clonar o repositório

git clone https://github.com/AdrianoPais/Bash-Scripting-for-Networking-Purposes-on-CentOS-9.git
cd Bash-Scripting-for-Networking-Purposes-on-CentOS-9

2. Dar permissões de execução

chmod +x config_ftp.sh config_ssh.sh config_dhcp.sh

3. Executar os Scripts (como Root/Sudo)

Cada script é independente e deve ser executado conforme a necessidade:

sudo ./config_ftp.sh
sudo ./config_ssh.sh
sudo ./config_dhcp.sh

Nota: Para o funcionamento do DHCP e NAT, é necessário que o servidor possua duas interfaces de rede (WAN e LAN) devidamente identificadas durante a execução do script.   

## Checklist de Segurança Implementada

[x] SELinux: Ativo e configurado para todos os serviços.   
[x] Firewall: Apenas portas necessárias abertas (21, 2222, 67/UDP).  
[x] Proteção de Brute-Force: Fail2Ban ativo no SSH e FTP.
[x] Persistence: Regras de NAT e serviços configurados para iniciar no boot.  

## Autor

Sérgio Correia
Projeto desenvolvido no âmbito da formação técnica na ATEC.
