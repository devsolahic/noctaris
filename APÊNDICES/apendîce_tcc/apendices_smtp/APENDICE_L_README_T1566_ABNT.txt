APÊNDICE L – README T1566 – POSTFIX LOG ANALYSIS

Título: MITRE ATT&CK: T1566 - Phishing
Autor: root@smtp
Data: 09 de October de 2025
Local: /etc/fail2ban/filter.d/mitre-t1566.conf
Sistema Operacional: Arch Linux

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro Fail2Ban
referente à técnica MITRE ATT&CK T1566, aplicado sobre o log do serviço
Postfix. O objetivo foi validar a capacidade do filtro em detectar tentativas
de phishing ou envio para destinatários inválidos, rejeições de RCPT ou relays
não permitidos.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /tmp/postfix.log /etc/fail2ban/filter.d/mitre-t1566.conf

Resultados obtidos:
    Failregex: 54 total
        - 54 hits: postfix/smtpd - NOQUEUE: reject RCPT (User unknown / Relay access denied)
    Ignoreregex: 0 total
    Linhas processadas: 12510
    Linhas correspondentes (matched): 54
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 12456
    Tempo de processamento: 6,43 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (54 / 12510) × 100 ≈ 0,43 %

Interpretação:
- O coeficiente de cobertura de 0,43% indica que o filtro identificou poucos
  eventos relacionados a rejeições de destinatário ou tentativas de phishing.
- O valor é coerente, considerando que a maior parte do log contém operações
  legítimas do Postfix.
- O filtro capturou eventos relevantes para monitoramento de segurança SMTP.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O filtro está funcional e apresenta efetividade inicial.
- As expressões regulares aplicadas detectaram:
      ^.*postfix/smtpd\[\d+\]: NOQUEUE: reject: RCPT from (?:\S+)\[<HOST>\]: (550|554) (5\.[0-9]+\.[0-9]+) .* (User unknown|Relay access denied).*
- Nenhum erro de sintaxe ou inconsistência foi identificado no filtro.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- O backend utilizado no Fail2Ban foi `systemd`, compatível com Arch Linux.
- Para testes, os logs do `journalctl` foram exportados para /tmp/postfix.log.
- Recomenda-se monitoramento contínuo e ajustes finos para incluir novos
  padrões de tentativas de envio inválidas ou phishing.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional e com correspondências válidas.  
✔️ Execução sem erros de sintaxe.  
ℹ️ Captura de eventos relacionados a rejeições RCPT e phishing.  
📊 Coeficiente de cobertura: **0,43 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Continuar monitoramento contínuo do serviço Postfix.
2. Ajustar expressões regulares para novos padrões de phishing ou RCPT inválido.
3. Documentar futuros eventos T1566 detectados para análise histórica.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O filtro `mitre-t1566.conf` detectou eventos de rejeição de destinatário e
possíveis tentativas de phishing no log do Postfix, com coeficiente de cobertura
de 0,43%. O filtro está funcional e deve ser monitorado continuamente.

-------------------------------------------------------------------------------
FIM DO APÊNDICE L
-------------------------------------------------------------------------------
