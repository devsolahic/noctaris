# 🛰️ Noctaris

**Análise de Modos Operacionais de Atacantes Cibernéticos por Meio de Logs na Exploração de Portas em Servidores**

---

### 👥 Autor

- **Elias de Jesus Miranda** – [elias.miranda@solahic.com.br](mailto:elias.miranda@solahic.com.br)  
  Faculdade Presbiteriana Gammon, Lavras-MG  

### 👥 Orientador 
- **Erasmo Evangelista de Oliveira** – [erasmo.oliveira@fagammon.edu.br](mailto:erasmo.oliveira@fagammon.edu.br)  
  Faculdade Presbiteriana Gammon, Lavras-MG  

### 👥 Coorientadores
- **Fernando Elias de Oliveira** – [fernando.oliveira@fagammon.edu.br](mailto:fernando.oliveira@fagammon.edu.br)  
  Faculdade Presbiteriana Gammon, Lavras-MG  

- **Anderson Bernardo dos Santos** – [anderson.santos@fagammon.edu.br](mailto:anderson.santos@fagammon.edu.br)  
  Faculdade Presbiteriana Gammon, Lavras-MG  

---

## 🧩 Sobre o Projeto

**Noctaris** é uma plataforma desenvolvida pela **Solahic** para **observação, classificação e análise automatizada de eventos de segurança cibernética**.  
O sistema foi concebido como parte de uma **pesquisa acadêmica aplicada** à detecção de **modos operacionais de atacantes** com base em **logs coletados de honeypots Linux** e **classificados segundo a taxonomia MITRE ATT&CK**.

A solução combina **instrumentação de serviços expostos (SSH, SMTP, HTTP e TCP/IP)** com uma **camada analítica e visual interativa**, permitindo:
- Monitoramento em tempo real das atividades maliciosas;
- Identificação de técnicas e táticas de ataque;
- Correlação geográfica e temporal de eventos;
- Apoio a estudos de **Inteligência de Ameaças (Threat Intelligence)**.

---

## 🧠 Fundamentação Técnica

O **Noctaris** foi projetado sobre uma **arquitetura modular** que integra coleta, persistência e visualização:

### 1. **Camada de Coleta**
- Honeypots implementados em contêineres **Linux isolados (Docker)**;
- Captura de eventos de rede e logs de autenticação;
- Filtragem e normalização de dados com **Python e Bash**;
- Armazenamento inicial em **MongoDB**.

### 2. **Camada de Classificação**
- Mapeamento automático de eventos conforme **MITRE ATT&CK v14**;
- Agrupamento por técnica e serviço afetado;
- Enriquecimento de IPs com informações de WHOIS, ASN e país de origem;
- Processamento distribuído e cron jobs para atualização contínua.

### 3. **Camada de Visualização**
- Painel **Noctaris Dashboard** (frontend web) para acompanhamento em tempo real;
- Gráficos dinâmicos de frequência, dispersão e origem de ataques;
- Correlação por serviço e técnica (T1595, T1110, T1190, T1566, entre outras);
- Integração com **APIs de Threat Intelligence** e logs históricos.

---

## 🔍 Resultados Obtidos

A instrumentação dos honeypots e o processamento contínuo via Noctaris revelaram:

- Predominância das técnicas:
  - **T1595 – Active Scanning**
  - **T1110 – Brute Force**
  - **T1190 – Exploit Public-Facing Application**
  - **T1566 – Phishing**

- Ações automatizadas de varredura e exploração em massa;
- Concentração geográfica de ataques na **América do Norte, Europa e Ásia**;
- Eficiência das medidas de isolamento e controle aplicadas;
- Ineficiência da simples troca de portas SSH como defesa.

---

## 🧰 Tecnologias Utilizadas

| Categoria | Ferramenta / Tecnologia |
|------------|--------------------------|
| Linguagens | Python, Bash |
| Banco de Dados | MongoDB |
| Visualização | Noctaris Dashboard (Flask + Chart.js) |
| Infraestrutura | Docker, Linux Containers |
| Monitoramento | Syslog, Journalctl, Nginx Access Logs |
| Classificação | MITRE ATT&CK |
| Enriquecimento | WHOIS / GeoIP APIs |
| Automação | Cron, Shell Scripts |

---

## 🧪 Implementação e Reprodutibilidade

Para pesquisadores que desejem reproduzir o ambiente:

```bash
git clone git@github.com:devsolahic/noctaris.git
cd noctaris
./install.sh

