# bootcamp-riachuelo-cybersecurity-lab
Simulação de ataques de força bruta e análise de vulnerabilidades em serviços FTP, SMB e Web (DVWA) utilizando Kali Linux, Medusa e Burp Suite. Projeto prático do Bootcamp Riachuelo/DIO.

## Projeto: Simulação de Ataques de Força Bruta e Análise de Vulnerabilidades

Este repositório contém a documentação e os resultados do desafio prático de implementação de ataques de força bruta em ambientes controlados. O objetivo principal foi validar vulnerabilidades em serviços críticos e propor medidas de mitigação baseadas em frameworks de segurança.

## 🚀 Objetivo do Desafio
Implementar um laboratório de testes de intrusão para simular cenários reais de ataques de força bruta, utilizando ferramentas de auditoria e automação para comprometer serviços de rede e aplicações web.

## 🛠️ Tecnologias e Ferramentas Utilizadas
* **Sistema Operacional:** Kali Linux (Atacante) e Metasploitable 2 (Alvo).
* **Rede:** Configuração Host-Only via VirtualBox.
* **Ferramentas:** * `Medusa`: Automação de ataques de força bruta (FTP, SMB e HTTP).
    * `Burp Suite`: Interceptação e análise de tráfego web.
    * `enum4linux`: Enumeração de usuários e compartilhamentos SMB.
    * `smbclient`: Exploração de diretórios e arquivos em rede.

## 💻 Cenários de Teste

### 1. Força Bruta em FTP (Porta 21)
Execução de ataque de dicionário utilizando o módulo FTP do Medusa para obter acesso administrativo.
```bash
medusa -h 192.168.56.102 -u msfadmin -P wordlist.txt -M ftp
```bash
### 2. Password Spraying e Exploração de SMB (Porta 445)
Neste cenário, utilizou-se a técnica de Password Spraying para testar uma única senha contra uma lista de usuários, visando evitar a detecção por sistemas de proteção.

Enumeração de Usuários:
```bash
enum4linux -U 192.168.56.102
```bash
