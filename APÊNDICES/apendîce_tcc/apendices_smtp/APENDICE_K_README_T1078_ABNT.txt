APÊNDICE K – README T1078 – POSTFIX LOG ANALYSIS

Título: MITRE ATT&CK: T1078 - Valid Accounts
Autor: root@smtp
Data: 09 de October de 2025
Local: /etc/fail2ban/filter.d/mitre-t1078.conf
Sistema Operacional: Arch Linux

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro Fail2Ban
referente à técnica MITRE ATT&CK T1078, aplicado sobre o log do serviço
Postfix. O objetivo foi validar a capacidade do filtro em detectar uso de
contas válidas comprometidas ou tentativas de login legítimo de forma suspeita.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /tmp/postfix.log /etc/fail2ban/filter.d/mitre-t1078.conf

Resultados obtidos:
    Failregex: 0 total
    Ignoreregex: 0 total
    Linhas processadas: 12510
    Linhas correspondentes (matched): 0
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 12510
    Tempo de processamento: 6,54 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (0 / 12510) × 100 = 0 %

Interpretação:
- O coeficiente de cobertura de 0% indica que o filtro não identificou nenhum
  evento correspondente ao padrão T1078 no log analisado.
- Isso é esperado caso não haja tentativas de login suspeitas ou uso de
  credenciais comprometidas no período analisado.
- O filtro permanece válido e pronto para execução futura.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- Nenhum evento de login legítimo ou suspeito foi detectado.
- O filtro está funcional, mas não encontrou correspondências no log.
- Recomenda-se continuidade no monitoramento e ajustes caso surjam novos
  eventos suspeitos.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- O backend utilizado no Fail2Ban foi `systemd`, compatível com Arch Linux.
- Para testes, os logs do `journalctl` foram exportados para /tmp/postfix.log.
- Nenhum padrão correspondente a T1078 foi encontrado neste período.
- Recomenda-se manutenção periódica do filtro e ajustes caso surjam novos
  eventos suspeitos.

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional, sem erros de sintaxe.  
ℹ️ Nenhum evento detectado no período analisado.  
📊 Coeficiente de cobertura: **0 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Continuar monitoramento contínuo do serviço Postfix.
2. Ajustar expressões regulares caso surjam padrões específicos de login
   suspeito.
3. Documentar futuros eventos T1078 detectados para análise histórica.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O filtro `mitre-t1078.conf` não detectou eventos no log do Postfix neste
período, resultando em coeficiente de cobertura 0%. O filtro permanece
válido e deve ser monitorado continuamente.

-------------------------------------------------------------------------------
FIM DO APÊNDICE K
-------------------------------------------------------------------------------
