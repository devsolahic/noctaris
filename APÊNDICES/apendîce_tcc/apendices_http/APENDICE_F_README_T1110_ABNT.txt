APÊNDICE F – README T1110 – NGX ACCESS LOG ANALYSIS

Título: MITRE ATT&CK: T1110 - Brute Force (HTTP/S Admin Panels)
Autor: root@proxynoc
Data: 09 de outubro de 2025
Local: /etc/fail2ban/filter.d/mitre-t1110.conf

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro
Fail2Ban referente à técnica MITRE ATT&CK T1110, aplicado sobre o log de
acesso do servidor Nginx. O objetivo foi validar a capacidade do filtro em
detectar tentativas de força bruta em painéis administrativos via HTTP/S.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /var/log/nginx/noctaris.access.log /etc/fail2ban/filter.d/mitre-t1110.conf

Resultados obtidos:
    Failregex: 33 total
        - 32 hits: ^<HOST> .*"(?:POST|GET)\s+/boaform/admin/formLogin\b
        - 1 hit:  ^<HOST> .*"(?:POST|GET)\s+/admin/config\.php\b
    Ignoreregex: 0 total
    Linhas processadas: 274
    Linhas correspondentes (matched): 33
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 241
    Tempo de processamento: 0,12 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (33 / 274) × 100 ≈ 12,04 %

Interpretação:
- O coeficiente de cobertura de 12,04% indica que o filtro identificou cerca de
  12% das linhas do log como potenciais tentativas de ataque.
- A maior parte das linhas do log corresponde a requisições legítimas.
- O filtro capturou tentativas de acesso a páginas administrativas críticas,
  como `/boaform/admin/formLogin` e `/admin/config.php`.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O filtro está funcional e apresentou efetividade inicial.
- A expressão regular utilizada foi capaz de detectar tentativas de força bruta
  em painéis administrativos via HTTP/S.
- O volume de 12,04% de correspondências é coerente com logs de acesso web, onde
  a maioria das requisições é legítima.
- Nenhum erro de sintaxe ou inconsistência foi detectado durante o processamento
  do log.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- As expressões regulares aplicadas pelo `failregex`:
      ^<HOST> .*"(?:POST|GET)\s+/boaform/admin/formLogin\b
      ^<HOST> .*"(?:POST|GET)\s+/admin/config\.php\b
  mostraram-se compatíveis com o formato de log padrão do Nginx.
- A cobertura obtida é adequada para a identificação de ataques direcionados
  a painéis administrativos.
- Recomenda-se monitoramento contínuo e ajustes finos para incluir:
  - Outros endpoints administrativos comuns;
  - Tentativas automatizadas repetitivas;
  - Padrões de User-Agent suspeitos.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional e com correspondências válidas.  
✔️ Execução sem erros de sintaxe.  
ℹ️ Captura de tentativas de força bruta HTTP/S.  
📊 Coeficiente de cobertura: **12,04 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Realizar novos testes com logs ampliados e maior diversidade de requisições.
2. Expandir failregex para outros endpoints administrativos.
3. Implementar agrupamento por IP para detectar ataques distribuídos.
4. Registrar histórico do coeficiente de cobertura para monitoramento da evolução
   do filtro.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O teste do filtro `mitre-t1110.conf` demonstrou efetividade inicial na detecção
de tentativas de força bruta via HTTP/S. O coeficiente de cobertura de 12,04%
confirma a operação correta do filtro e sua adequação parcial ao ambiente Nginx.
A expectativa é aumentar a cobertura com ajustes incrementais sem gerar
falsos positivos.

-------------------------------------------------------------------------------
FIM DO APÊNDICE F
-------------------------------------------------------------------------------

