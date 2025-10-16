APÊNDICE N – README T1595 – POSTFIX LOG ANALYSIS

Título: MITRE ATT&CK: T1595 - Active Scanning / Gather Victim Network Information
Autor: root@smtp
Data: 09 de October de 2025
Local: /etc/fail2ban/filter.d/mitre-t1595.conf
Sistema Operacional: Arch Linux

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro Fail2Ban
referente à técnica MITRE ATT&CK T1595, aplicado sobre o log do serviço
Postfix. O objetivo foi validar a capacidade do filtro em detectar eventos de
perda de conexão anormal durante comandos SMTP (EHLO, HELO, HELP, CONNECT,
STARTTLS, AUTH).

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /tmp/postfix.log /etc/fail2ban/filter.d/mitre-t1595.conf

Resultados obtidos:
    Failregex: 243 total
        - 729 hits: postfix/smtpd - NOQUEUE: lost connection after (EHLO|HELO|HELP|CONNECT|STARTTLS|AUTH)
    Ignoreregex: 0 total
    Linhas processadas: 12510
    Linhas correspondentes (matched): 243
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 12267
    Tempo de processamento: 29,94 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (243 / 12510) × 100 ≈ 1,94 %

Interpretação:
- O coeficiente de cobertura de 1,94% indica que o filtro identificou eventos
  de perda de conexão durante comandos SMTP.
- O valor é coerente, considerando que a maioria das conexões é legítima.
- O filtro capturou eventos relevantes para monitoramento de segurança SMTP.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O filtro está funcional e apresenta efetividade inicial.
- A expressão regular aplicada detectou:
      ^.*postfix/smtpd\[\d+\]: NOQUEUE: lost connection after (EHLO|HELO|HELP|CONNECT|STARTTLS|AUTH) from <HOST>.*$
- Nenhum erro de sintaxe ou inconsistência foi identificado no filtro.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- O backend utilizado no Fail2Ban foi `systemd`, compatível com Arch Linux.
- Para testes, os logs do `journalctl` foram exportados para /tmp/postfix.log.
- Recomenda-se monitoramento contínuo e ajustes finos para incluir novos
  padrões de perda de conexão ou comportamento suspeito.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional e com correspondências válidas.  
✔️ Execução sem erros de sintaxe.  
ℹ️ Captura de eventos de perda de conexão SMTP.  
📊 Coeficiente de cobertura: **1,94 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Continuar monitoramento contínuo do serviço Postfix.
2. Ajustar expressões regulares para novos padrões de perda de conexão.
3. Documentar futuros eventos T1595 detectados para análise histórica.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O filtro `mitre-t1595.conf` detectou eventos de perda de conexão durante
comandos SMTP no log do Postfix, com coeficiente de cobertura de 1,94%. O
filtro está funcional e deve ser monitorado continuamente para identificar
futuras tentativas suspeitas.

-------------------------------------------------------------------------------
FIM DO APÊNDICE N
-------------------------------------------------------------------------------
