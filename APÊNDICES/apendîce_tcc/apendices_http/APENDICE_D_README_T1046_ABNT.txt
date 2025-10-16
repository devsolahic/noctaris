APÊNDICE D – README T1046 – NGX ACCESS LOG ANALYSIS

Título: MITRE ATT&CK: T1046 - Network Service Scanning (Nginx Access Log)
Autor: root@proxynoc
Data: 09 de outubro de 2025
Local: /etc/fail2ban/filter.d/mitre-t1046.conf

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice documenta o resultado dos testes realizados com o filtro
Fail2Ban referente à técnica MITRE ATT&CK T1046, aplicado sobre o log de acesso
do servidor Nginx. O objetivo foi avaliar se o filtro é capaz de identificar
padrões de port scan ou tentativas de sondagem de rede a partir de requisições
HTTP registradas no access log.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /var/log/nginx/noctaris.access.log /etc/fail2ban/filter.d/mitre-t1046.conf

Resultados obtidos:
    Failregex: 0 total
    Ignoreregex: 0 total
    Linhas processadas: 240
    Linhas correspondentes (matched): 0
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 240
    Tempo de processamento: 0,11 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (0 / 240) × 100 = 0,0 %

Interpretação:
- O coeficiente de cobertura de 0,0% indica que nenhuma linha do log foi
  reconhecida pelo padrão definido no filtro.
- Embora o teste tenha sido executado com sucesso técnico, o resultado demonstra
  que o filtro ainda **não está operacional** para o formato atual de log do
  servidor Nginx.
- Este valor serve como base de referência (baseline) para futuras medições de
  eficácia após ajustes nas expressões regulares.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O log foi processado corretamente, sem erros de sintaxe ou codificação.
- Nenhuma correspondência foi registrada, o que sugere que o `failregex` não
  está compatível com o formato de linhas do access log do Nginx.
- Todas as 240 linhas foram classificadas como "missed" (não correspondentes),
  evidenciando ausência de detecção.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- O filtro `mitre-t1046.conf` provavelmente foi projetado para logs do tipo
  `/var/log/messages` ou `/var/log/syslog`, não para access logs HTTP.
- É necessário ajustar as expressões regulares para identificar:
  - Requisições repetitivas e anômalas em curtos intervalos de tempo;
  - Tentativas de varredura de portas HTTP (por exemplo, 8080, 8443, 22 via proxy);
  - User-Agents característicos de scanners e ferramentas de enumeração.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
⚠️ Filtro sem correspondências (0%).  
ℹ️ Necessita ajustes no `failregex`.  
✔️ Execução sem erros de sintaxe.  
✔️ Log processado corretamente (UTF-8).  
📊 Coeficiente de cobertura: **0,0 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Revisar e adaptar o `failregex` ao formato do access log do Nginx.
2. Adicionar padrões específicos para varreduras HTTP e tentativas de exploração.
3. Testar novamente com `fail2ban-regex` e registrar o novo coeficiente.
4. Comparar o desempenho com o filtro T1110 (SSH) e T1017 (Web Protocols).
5. Criar histórico de cobertura para acompanhamento da evolução do filtro.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O teste do filtro `mitre-t1046.conf` em logs do Nginx foi executado com êxito
técnico, mas sem eficácia de detecção. O coeficiente de cobertura calculado
em 0,0% confirma que o filtro não possui compatibilidade com o formato de log
analisado. Recomenda-se a reformulação das expressões regulares de captura
para adequação ao contexto HTTP, permitindo que futuras execuções apresentem
índices de cobertura mais representativos.

-------------------------------------------------------------------------------
FIM DO APÊNDICE D
-------------------------------------------------------------------------------

