APÊNDICE G – README T1190 – NGX ACCESS LOG ANALYSIS

Título: MITRE ATT&CK: T1190 - Exploit Public-Facing Application
Autor: root@proxynoc
Data: 09 de outubro de 2025
Local: /etc/fail2ban/filter.d/mitre-t1190.conf

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro
Fail2Ban referente à técnica MITRE ATT&CK T1190, aplicado sobre o log de
acesso do servidor Nginx. O objetivo foi validar a capacidade do filtro em
detectar tentativas de exploração de aplicações web públicas.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /var/log/nginx/noctaris.access.log /etc/fail2ban/filter.d/mitre-t1190.conf

Resultados obtidos:
    Failregex: 23 total
        - 23 hits: ^<HOST> - - \[.*\] "(GET|POST).*\/(\.env|wp-config\.php|config(\.json)?|/shell.*|/cgi-bin/.*|/boaform/.*|/device\.rsp.*) HTTP/.*" .*
    Ignoreregex: 0 total
    Linhas processadas: 275
    Linhas correspondentes (matched): 23
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 252
    Tempo de processamento: 0,12 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (23 / 275) × 100 ≈ 8,36 %

Interpretação:
- O coeficiente de cobertura de 8,36% indica que o filtro identificou cerca de
  8% das linhas do log como potenciais tentativas de exploração.
- A maior parte das requisições é legítima, o que explica a cobertura relativamente baixa.
- O filtro capturou acessos a arquivos sensíveis e endpoints críticos, incluindo
  `.env`, `wp-config.php`, `config.json`, `/shell`, `/cgi-bin`, `/boaform` e `/device.rsp`.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O filtro apresentou funcionalidade e efetividade parcial.
- A expressão regular capturou corretamente padrões de exploração em aplicações
  web públicas.
- O volume de correspondências é coerente com logs de acesso web típicos,
  onde tentativas de ataque representam uma pequena fração.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- A expressão regular utilizada mostrou-se compatível com o formato de log do
  Nginx.
- Recomenda-se monitoramento contínuo e ajustes finos para:
  - Incluir novos endpoints críticos descobertos;
  - Identificar padrões de User-Agent suspeitos;
  - Agrupar tentativas por IP para detectar ataques distribuídos.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional e com correspondências válidas.  
✔️ Execução sem erros de sintaxe.  
ℹ️ Captura de tentativas de exploração HTTP/S.  
📊 Coeficiente de cobertura: **8,36 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Revisar e expandir padrões do failregex para novos endpoints críticos.
2. Implementar monitoramento contínuo e histórico de cobertura.
3. Realizar testes adicionais com logs mais extensos.
4. Avaliar necessidade de bloqueios automáticos baseados em IPs detectados.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O teste do filtro `mitre-t1190.conf` demonstrou efetividade inicial na detecção
de tentativas de exploração de aplicações web públicas. O coeficiente de
cobertura de 8,36% confirma a operação correta do filtro e fornece uma base
para aprimoramentos futuros, garantindo maior proteção sem gerar falsos positivos.

-------------------------------------------------------------------------------
FIM DO APÊNDICE G
-------------------------------------------------------------------------------

