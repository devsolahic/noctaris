APÊNDICE J – README T1071 – POSTFIX LOG ANALYSIS

Título: MITRE ATT&CK: T1071 - Application Layer Protocol
Autor: root@smtp
Data: 09 de October de 2025
Local: /etc/fail2ban/filter.d/mitre-t1071.conf
Sistema Operacional: Arch Linux

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro Fail2Ban
referente à técnica MITRE ATT&CK T1071, aplicado sobre o log do serviço
Postfix. O objetivo foi validar a capacidade do filtro em detectar atividades
suspeitas em protocolos de aplicação SMTP, incluindo conexões anômalas e
padrões de pipelining incorretos.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /tmp/postfix.log /etc/fail2ban/filter.d/mitre-t1071.conf

Resultados obtidos:
    Failregex: 1051 total
        - 911 hits: postfix/smtpd - connect from unknown
        - 137 hits: postfix/smtpd - improper command pipelining after CONNECT
        - 3 hits: postfix/smtpd - improper command pipelining after EHLO
    Ignoreregex: 0 total
    Linhas processadas: 12510
    Linhas correspondentes (matched): 1051
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 11459
    Tempo de processamento: 14,30 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (1051 / 12510) × 100 ≈ 8,40 %

Interpretação:
- O coeficiente de cobertura de 8,40% indica que o filtro identificou cerca de
  8% das linhas do log como eventos SMTP relevantes.
- O valor é coerente, considerando que a maior parte do log contém operações
  legítimas de entrega de emails.
- O filtro capturou eventos importantes como conexões de clientes desconhecidos
  e pipelining incorreto.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O filtro está funcional e apresenta efetividade inicial.
- As expressões regulares aplicadas detectaram:
      ^.*postfix/smtpd\[\d+\]: connect from unknown\[<HOST>\].*$
      ^.*postfix/smtpd\[\d+\]: improper command pipelining after CONNECT from unknown\[<HOST>\].*$
      ^.*postfix/smtpd\[\d+\]: improper command pipelining after EHLO from unknown\[<HOST>\].*$
- O volume de 8,40% de correspondências é aceitável para logs de serviços SMTP ativos.
- Nenhum erro de sintaxe ou inconsistência foi identificado no filtro.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- O backend utilizado no Fail2Ban foi `systemd`, compatível com Arch Linux.
- Para testes, os logs do `journalctl` foram exportados para /tmp/postfix.log.
- Recomenda-se monitoramento contínuo e ajustes finos para incluir:
  - Novos padrões de comportamento suspeito de clientes SMTP;
  - Agrupamento por IP para detectar tentativas distribuídas;
  - Correlação com outros filtros (T1046, T1190) para análise de ataques múltiplos.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional e com correspondências válidas.  
✔️ Execução sem erros de sintaxe.  
ℹ️ Captura de eventos relevantes do protocolo SMTP.  
📊 Coeficiente de cobertura: **8,40 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Realizar testes com logs maiores e históricos mais longos.
2. Ajustar expressões regulares para novos padrões detectados.
3. Implementar alertas automáticos baseados em IPs suspeitos.
4. Manter histórico da cobertura para monitoramento da evolução do filtro.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O filtro `mitre-t1071.conf` demonstrou efetividade na detecção de eventos do
protocolo SMTP, com coeficiente de cobertura de 8,40%. O filtro está pronto
para monitoramento contínuo.

-------------------------------------------------------------------------------
FIM DO APÊNDICE J
-------------------------------------------------------------------------------
