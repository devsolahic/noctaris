APÊNDICE I – README T1046 – POSTFIX LOG ANALYSIS

Título: MITRE ATT&CK: T1046 - Network Service Discovery (SMTP)
Autor: root@smtp
Data: 09 de October de 2025
Local: /etc/fail2ban/filter.d/mitre-t1046.conf
Sistema Operacional: Arch Linux

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro Fail2Ban
referente à técnica MITRE ATT&CK T1046, aplicado sobre o log do serviço
Postfix. O objetivo foi validar a capacidade do filtro em detectar atividades
suspeitas de clientes SMTP, como varreduras de portas, desconexões anômalas
e tentativas de conexão incorretas.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /tmp/postfix.log /etc/fail2ban/filter.d/mitre-t1046.conf

Resultados obtidos:
    Failregex: 2318 total
        - 137 hits: postfix/smtpd - improper command pipelining after CONNECT
        - 911 hits: postfix/smtpd - disconnect from unknown
        - 636 hits: postfix/anvil - max connection rate
        - 634 hits: postfix/anvil - max connection count
    Ignoreregex: 0 total
    Linhas processadas: 12510
    Linhas correspondentes (matched): 2318
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 10192
    Tempo de processamento: 14,42 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (2318 / 12510) × 100 ≈ 18,52 %

Interpretação:
- O coeficiente de cobertura de 18,52% indica que o filtro identificou cerca de
  18% das linhas do log como eventos SMTP relevantes.
- O valor é coerente considerando que grande parte do log contém operações
  legítimas de entrega de emails.
- O filtro capturou eventos importantes para monitoramento de ataques ou
  comportamento anômalo de clientes SMTP.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O filtro está funcional e apresenta efetividade inicial.
- As expressões regulares aplicadas detectaram:
      ^.*postfix/smtpd\[\d+\]: improper command pipelining after CONNECT from unknown\[<HOST>\].*$
      ^.*postfix/smtpd\[\d+\]: disconnect from unknown\[<HOST>\].*$
      ^.*postfix/anvil\[\d+\]: statistics: max connection rate \d+/\d+s for \(smtp:<HOST>\) .*$ 
      ^.*postfix/anvil\[\d+\]: statistics: max connection count \d+ for \(smtp:<HOST>\) .*$ 
- O volume de 18,52% de correspondências é aceitável para logs de serviços SMTP ativos.
- Nenhum erro de sintaxe ou inconsistência foi identificado no filtro.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- O backend utilizado no Fail2Ban foi `systemd`, compatível com Arch Linux.
- Para testes, os logs do `journalctl` foram exportados para /tmp/postfix.log.
- Recomenda-se monitoramento contínuo e ajustes finos para incluir:
  - Novos padrões de comportamento suspeito de clientes SMTP;
  - Agrupamento por IP para detectar tentativas distribuídas;
  - Correlação com outros filtros (T1190, T1110) para análise de ataques múltiplos.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional e com correspondências válidas.  
✔️ Execução sem erros de sintaxe.  
ℹ️ Captura de eventos relevantes do serviço SMTP.  
📊 Coeficiente de cobertura: **18,52 %**

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
O teste do filtro `mitre-t1046.conf` demonstrou efetividade na detecção de
eventos suspeitos do serviço Postfix. O coeficiente de cobertura de 18,52%
confirma o funcionamento correto do filtro no Arch Linux, fornecendo base para
aprimoramentos futuros e monitoramento contínuo.

-------------------------------------------------------------------------------
FIM DO APÊNDICE I
-------------------------------------------------------------------------------
