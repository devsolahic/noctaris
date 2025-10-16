APÊNDICE M – README T1589 – POSTFIX LOG ANALYSIS

Título: MITRE ATT&CK: T1589 - Gather Victim Network Information
Autor: root@smtp
Data: 09 de October de 2025
Local: /etc/fail2ban/filter.d/mitre-t1589.conf
Sistema Operacional: Arch Linux

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro Fail2Ban
referente à técnica MITRE ATT&CK T1589, aplicado sobre o log do serviço
Postfix. O objetivo foi validar a capacidade do filtro em detectar tentativas
de envio para destinos não permitidos, incluindo rejeições de RCPT com
mensagem “Relay access denied”.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /tmp/postfix.log /etc/fail2ban/filter.d/mitre-t1589.conf

Resultados obtidos:
    Failregex: 24 total
        - 24 hits: postfix/smtpd - NOQUEUE: reject RCPT (Relay access denied)
    Ignoreregex: 0 total
    Linhas processadas: 12510
    Linhas correspondentes (matched): 24
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 12486
    Tempo de processamento: 6,57 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (24 / 12510) × 100 ≈ 0,19 %

Interpretação:
- O coeficiente de cobertura de 0,19% indica que o filtro identificou poucos
  eventos de tentativas de envio não autorizado.
- O valor é coerente, considerando que a maioria das mensagens do Postfix são
  legítimas.
- O filtro capturou eventos relevantes para monitoramento de segurança SMTP.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O filtro está funcional e apresenta efetividade inicial.
- A expressão regular aplicada detectou:
      ^.*postfix/smtpd\[\d+\]: NOQUEUE: reject: RCPT from .*?\[<HOST>\]: 554 5\.7\.1 <.*>: Relay access denied
- Nenhum erro de sintaxe ou inconsistência foi identificado no filtro.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- O backend utilizado no Fail2Ban foi `systemd`, compatível com Arch Linux.
- Para testes, os logs do `journalctl` foram exportados para /tmp/postfix.log.
- Recomenda-se monitoramento contínuo e ajustes finos para incluir novos
  padrões de Relay access denied ou tentativas de envio não autorizado.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional e com correspondências válidas.  
✔️ Execução sem erros de sintaxe.  
ℹ️ Captura de eventos relacionados a tentativas de envio não autorizadas.  
📊 Coeficiente de cobertura: **0,19 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Continuar monitoramento contínuo do serviço Postfix.
2. Ajustar expressões regulares para novos padrões de Relay access denied.
3. Documentar futuros eventos T1589 detectados para análise histórica.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O filtro `mitre-t1589.conf` detectou eventos de tentativas de envio não
autorizadas no log do Postfix, com coeficiente de cobertura de 0,19%. O filtro
está funcional e deve ser monitorado continuamente para identificar futuras
tentativas suspeitas.

-------------------------------------------------------------------------------
FIM DO APÊNDICE M
-------------------------------------------------------------------------------
