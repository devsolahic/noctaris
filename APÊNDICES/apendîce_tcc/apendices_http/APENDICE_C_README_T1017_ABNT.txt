from datetime import datetime

# Conteúdo revisado do apêndice com coeficiente de cobertura incluído
apendice_c_v2 = f"""
APÊNDICE C – README T1017 – NGX ACCESS LOG ANALYSIS

Título: MITRE ATT&CK: T1017 - Application Layer Protocol (Nginx Access Log)
Autor: root@proxynoc
Data: {datetime.now().strftime("%d de %B de %Y")}
Local: /etc/fail2ban/filter.d/mitre-t1017.conf

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice documenta o resultado dos testes realizados com o filtro
Fail2Ban referente à técnica MITRE ATT&CK T1017, aplicado sobre o log de acesso
do servidor Nginx. O objetivo foi avaliar se o filtro está apto a identificar
tentativas de exploração ou comportamento anômalo via requisições HTTP.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /var/log/nginx/noctaris.access.log /etc/fail2ban/filter.d/mitre-t1017.conf

Resultados obtidos:
    Failregex: 0 total
    Ignoreregex: 0 total
    Linhas processadas: 238
    Linhas correspondentes (matched): 0
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 238
    Tempo de processamento: 0,11 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (0 / 238) × 100 = 0,0 %

Interpretação:
- O coeficiente de cobertura de 0,0% indica que nenhuma linha do log foi
  reconhecida pelo padrão definido no filtro.
- Embora o teste tenha sido executado corretamente, o resultado demonstra que o
  filtro ainda **não está operacional** para o formato atual de log do Nginx.
- Esse valor serve como linha de base para futuras medições, permitindo avaliar
  a evolução da eficácia do filtro após ajustes.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- Nenhuma linha do log correspondeu ao padrão definido no filtro (0 correspondências).
- Isso indica que o filtro ainda **não possui expressões regulares configuradas**
  para capturar eventos relevantes no log do Nginx.
- Todas as 238 linhas processadas foram consideradas "não correspondentes",
  o que reforça a necessidade de revisão da expressão `failregex`.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- O resultado não indica erro de sintaxe, mas sim **falta de efetividade**.
- É necessário adaptar o `failregex` ao formato padrão de log do Nginx, que
  geralmente segue o modelo:
      $remote_addr - $remote_user [$time_local] "$request" $status $body_bytes_sent
- Recomenda-se incluir padrões para identificar:
  - Requisições maliciosas (ex.: tentativas de injeção SQL, LFI, RFI);
  - Tentativas de acesso a rotas administrativas não autorizadas;
  - Padrões de scanners web (User-Agent suspeitos).

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
1. Revisar o `failregex` para adequá-lo ao formato do access log Nginx.
2. Testar novamente com `fail2ban-regex` após ajustes.
3. Adicionar padrões específicos para tentativas de exploração HTTP.
4. Registrar o novo coeficiente de cobertura a cada execução para acompanhamento.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O filtro `mitre-t1017.conf` foi testado com sucesso técnico (sem falhas de
execução), porém sem efetividade de detecção. O coeficiente de cobertura de 0,0%
confirma a ausência de correspondências, indicando a necessidade de desenvolvimento
de expressões regulares específicas para o log de acesso do Nginx. Após ajustes,
espera-se que o valor de cobertura aumente progressivamente até atingir níveis
similares aos filtros T1046 e T1110.

-------------------------------------------------------------------------------
FIM DO APÊNDICE C
-------------------------------------------------------------------------------
"""

# Caminho de saída do arquivo
file_path_c_v2 = "/mnt/data/APENDICE_C_README_T1017_ABNT_v2.txt"

# Gravação do arquivo
with open(file_path_c_v2, "w", encoding="utf-8") as file:
    file.write(apendice_c_v2)

file_path_c_v2

