# 🛡️ Desafio DIO: Ataques de Força Bruta com Medusa

Esse projeto faz parte do módulo de Segurança Ofensiva da DIO. O objetivo foi aprender como funcionam os ataques de força bruta (brute force) e como as ferramentas de auditoria, como o Medusa, trabalham para identificar senhas fracas.

## 🛠️ O que eu usei:
* **Kali Linux:** Minha máquina principal de ataque.
* **Metasploitable 2:** A máquina "vítima" que deixei rodando com serviços vulneráveis.
* **VirtualBox:** Usei para criar a rede interna entre as duas VMs.
* **Medusa:** A ferramenta que fez o trabalho sujo de testar as senhas.

## 🚀 O que foi feito (Passo a Passo)

### 1. Configuração do Lab
Primeiro, tive que configurar a rede no VirtualBox como "Rede Interna" para as duas máquinas se enxergarem sem expor meu PC real à internet. 
- IP da Vítima: `192.168.x.x` (mudei conforme o DHCP entregou).

### 2. Scan Inicial
Antes de atacar, usei o `nmap` para confirmar se os serviços estavam abertos:
`nmap -sV 192.168.x.x`
Vi que o FTP (porta 21) e o SMB (porta 445) estavam rodando.

### 3. Ataque ao FTP com Medusa
Usei uma wordlist simples que eu mesmo criei (`minha_wordlist.txt`) para testar o usuário "msfadmin".
O comando que rodei foi mais ou menos esse:
`medusa -h 192.168.x.x -u msfadmin -P minha_wordlist.txt -M ftp`

### 4. Teste em SMB
Também testei o módulo de SMB, que é muito comum em redes Windows, para ver como a ferramenta se comporta tentando descobrir a senha de acesso ao compartilhamento de arquivos.

## 📝 Minhas Wordlists
Não usei aquelas listas gigantes de GBs. Para o desafio, criei listas curtas com senhas comuns (123456, admin, password, etc) só para validar se o Medusa encontrava o acerto quando a senha correta estava lá no meio.

## 🛡️ Como se proteger disso?
Depois de ver como é rápido testar centenas de senhas, as lições que ficam são:
1. **Senhas Fortes:** Não adianta ter firewall se a senha é "123456".
2. **Bloqueio de Tentativas:** Configurar o sistema para travar o login depois de 3 ou 5 erros. Isso mata o ataque do Medusa na hora.
3. **Mudar Portas Padrão:** Não é a solução definitiva, mas ajuda a tirar o alvo do radar de scripts automáticos.
4. **Usar Chaves SSH:** Para serviços como FTP/SSH, chaves são infinitamente mais seguras que senhas.

---
*Projeto realizado para fins educacionais no curso de Segurança da Informação da DIO.*
