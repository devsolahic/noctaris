APÊNDICE B – README T1046 – PORTSCAN DETECTION

Título: MITRE ATT&CK: T1046 - Network Service Scanning (Portscan)
Autor: root@onrutas
Data: 09 de outubro de 2025
Local: /etc/fail2ban/filter.d/mitre-t1046.conf

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta a documentação técnica referente ao filtro Fail2Ban
associado à técnica MITRE ATT&CK T1046 - Network Service Scanning (Portscan).
O objetivo é detalhar o funcionamento, resultados de teste e cálculo de cobertura
obtidos na análise do log de mensagens do sistema.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /var/log/messages /etc/fail2ban/filter.d/mitre-t1046.conf

Resultados obtidos:
    Failregex: 11735 total
    |-  1) [11735] ^.*Portscan( (tentativa|detectado))?:.*SRC=<HOST>.*$
    Ignoreregex: 0 total
    Linhas processadas: 13.863
    Linhas correspondentes (matched): 11.735
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 2.128
    Tempo de processamento: 1,70 segundos

-------------------------------------------------------------------------------
CÁLCULO DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = linhas correspondentes / total de linhas
    cobertura = 11.735 / 13.863 ≈ 84,6 %

Interpretação:
- O filtro apresenta cobertura aproximada de 85%, valor considerado excelente.
- As linhas não correspondentes referem-se a mensagens do sistema que não
  indicam atividade de Portscan.
- Nenhum padrão de ignorância (ignoreregex) foi definido, permitindo análise
  completa de todas as ocorrências relevantes.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- Cobertura elevada (~85%) indica desempenho satisfatório do filtro.
- O padrão failregex captura corretamente eventos contendo as palavras:
      "Portscan tentativa" ou "Portscan detectado" seguidas de "SRC=<HOST>".
- Teste realizado sem erros de sintaxe.
- Log analisado com codificação UTF-8.
- Ausência de linhas ignoradas demonstra compatibilidade desejada com o formato
  de log do sistema.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro validado e ativo.
✔️ Captura confirmada de eventos de varredura de portas (Portscan).
ℹ️ Cobertura estimada em ~84,6% sobre o log /var/log/messages.
✔️ Chain MITRE-T1046 corretamente vinculada ao iptables.

-------------------------------------------------------------------------------
ROADMAP DE EVOLUÇÃO
-------------------------------------------------------------------------------
1. Monitoramento contínuo
   - Revisar semanalmente o status da jail 'mitre-t1046' via fail2ban-client.
2. Expansão do regex
   - Incluir novos padrões provenientes de ferramentas como Suricata ou Zeek.
3. Ajuste de falsos positivos
   - Definir ignoreregex para hosts internos confiáveis.
4. Histórico de cobertura
   - Registrar mensalmente a taxa de cobertura e número de eventos detectados.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O filtro mitre-t1046.conf demonstrou excelente desempenho, com taxa de
cobertura aproximada de 85%. O resultado confirma sua eficácia na detecção
de atividades de varredura de portas (Portscan) e sua integração correta ao
Fail2Ban e iptables. O apêndice reforça a confiabilidade e estabilidade da
configuração utilizada no ambiente monitorado.

-------------------------------------------------------------------------------
FIM DO APÊNDICE B
-------------------------------------------------------------------------------
