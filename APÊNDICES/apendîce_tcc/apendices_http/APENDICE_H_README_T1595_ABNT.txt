APÊNDICE H – README T1595 – NGX ACCESS LOG ANALYSIS

Título: MITRE ATT&CK: T1595 - Active Scanning
Autor: root@proxynoc
Data: 09 de outubro de 2025
Local: /etc/fail2ban/filter.d/mitre-t1595.conf

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro
Fail2Ban referente à técnica MITRE ATT&CK T1595, aplicado sobre o log de
acesso do servidor Nginx. O objetivo foi validar a capacidade do filtro em
detectar tentativas de varredura ativa e sondagem de recursos web.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /var/log/nginx/noctaris.access.log /etc/fail2ban/filter.d/mitre-t1595.conf

Resultados obtidos:
    Failregex: 11 total
        - 11 hits: ^<HOST> - - \[.*\] "(GET|POST|HEAD|OPTIONS) /.* HTTP/.*" 404 .*
    Ignoreregex: 0 total
    Linhas processadas: 275
    Linhas correspondentes (matched): 11
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 264
    Tempo de processamento: 0,12 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (11 / 275) × 100 ≈ 4,00 %

Interpretação:
- O coeficiente de cobertura de 4,00% indica que o filtro identificou cerca de
  4% das linhas do log como potenciais tentativas de varredura ativa.
- A maior parte das requisições é legítima, resultando em baixa cobertura.
- O filtro capturou requisições HTTP que retornaram código 404, típicas de
  sondagem de recursos inexistentes.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O filtro está funcional e apresentou detecção inicial.
- A expressão regular capturou corretamente padrões de sondagem ativa.
- O volume de correspondências é coerente com logs de acesso web, onde a
  maioria das requisições é legítima.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- A expressão regular utilizada mostrou-se compatível com o formato de log do
  Nginx.
- Recomenda-se monitoramento contínuo e ajustes finos para:
  - Identificar novos padrões de sondagem;
  - Agrupar tentativas por IP para detectar ataques distribuídos;
  - Correlacionar com outros filtros de segurança (T1190, T1110).

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional e com correspondências válidas.  
✔️ Execução sem erros de sintaxe.  
ℹ️ Captura de tentativas de varredura ativa HTTP/S.  
📊 Coeficiente de cobertura: **4,00 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Realizar novos testes com logs ampliados e maior diversidade de requisições.
2. Expandir failregex para identificar outros códigos de erro e endpoints
   sensíveis.
3. Implementar monitoramento contínuo e histórico de cobertura.
4. Avaliar integração com alertas automáticos para IPs suspeitos.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O teste do filtro `mitre-t1595.conf` demonstrou detecção inicial de varreduras
ativas. O coeficiente de cobertura de 4,00% confirma o funcionamento do filtro,
fornecendo base para ajustes futuros e maior eficácia na proteção do servidor
Nginx.

-------------------------------------------------------------------------------
FIM DO APÊNDICE H
-------------------------------------------------------------------------------

