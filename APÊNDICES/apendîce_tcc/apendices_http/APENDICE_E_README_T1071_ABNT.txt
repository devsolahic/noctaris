from datetime import datetime

# Conteúdo do Apêndice E - T1071 com coeficiente de cobertura calculado
apendice_e = f"""
APÊNDICE E – README T1071 – NGX ACCESS LOG ANALYSIS

Título: MITRE ATT&CK: T1071 - Application Layer Protocol (HTTP/S)
Autor: root@proxynoc
Data: {datetime.now().strftime("%d de %B de %Y")}
Local: /etc/fail2ban/filter.d/mitre-t1071.conf

-------------------------------------------------------------------------------
OBJETIVO
-------------------------------------------------------------------------------
Este apêndice apresenta o resultado do teste realizado com o filtro
Fail2Ban referente à técnica MITRE ATT&CK T1071, aplicado sobre o log de
acesso do servidor Nginx. O propósito foi validar a capacidade do filtro em
detectar comunicações HTTP/S anômalas, respostas de erro recorrentes e possíveis
indícios de comportamento malicioso em nível de aplicação.

-------------------------------------------------------------------------------
TESTES REALIZADOS
-------------------------------------------------------------------------------
Comando executado:
    fail2ban-regex /var/log/nginx/noctaris.access.log /etc/fail2ban/filter.d/mitre-t1071.conf

Resultados obtidos:
    Failregex: 22 total
    Ignoreregex: 0 total
    Linhas processadas: 274
    Linhas correspondentes (matched): 22
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 252
    Tempo de processamento: 0,12 segundos

-------------------------------------------------------------------------------
CÁLCULO DO COEFICIENTE DE COBERTURA
-------------------------------------------------------------------------------
Fórmula aplicada:
    cobertura = (linhas correspondentes / total de linhas) × 100
    cobertura = (22 / 274) × 100 = 8,03 %

Interpretação:
- O coeficiente de cobertura de 8,03% indica que o filtro identificou cerca de
  8% das linhas do log como potenciais incidentes relevantes.
- Esse índice é compatível com logs de acesso web, onde a maioria dos registros
  corresponde a requisições legítimas.
- O filtro capturou ocorrências de erros HTTP comuns (400, 401, 403, 404, 499,
  500, 502 e 503), que podem representar falhas ou tentativas automatizadas de
  exploração.

-------------------------------------------------------------------------------
ANÁLISE DOS RESULTADOS
-------------------------------------------------------------------------------
- O filtro demonstrou funcionalidade e efetividade parcial.
- A expressão regular utilizada capturou corretamente requisições HTTP e HTTPS
  com status de erro, atendendo ao objetivo da técnica T1071.
- O volume de 8,03% de correspondências sugere operação adequada sem excesso de
  falsos positivos.
- A análise de logs não identificou erros de sintaxe ou inconsistências no
  processo de correspondência.

-------------------------------------------------------------------------------
CONSIDERAÇÕES TÉCNICAS
-------------------------------------------------------------------------------
- O padrão aplicado pelo `failregex`:
      ^<HOST> - - \\[.*\\] "(GET|POST).*HTTP/.*" (400|401|403|404|499|500|502|503) .*
  mostrou-se compatível com o formato de log padrão do Nginx.
- A cobertura obtida é aceitável, considerando que apenas uma pequena fração dos
  acessos ao servidor tende a gerar códigos de erro HTTP.
- Recomenda-se realizar ajustes finos para incluir também:
  - Respostas HTTP 429 (Too Many Requests);
  - Tentativas repetitivas de POST em endpoints sensíveis;
  - Requisições com parâmetros suspeitos (ex.: injeções SQL ou LFI).

-------------------------------------------------------------------------------
STATUS ATUAL
-------------------------------------------------------------------------------
✔️ Filtro funcional e com correspondências válidas.  
✔️ Execução sem erros de sintaxe.  
ℹ️ Captura seletiva de códigos HTTP de erro.  
📊 Coeficiente de cobertura: **8,03 %**

-------------------------------------------------------------------------------
PLANO DE AÇÃO
-------------------------------------------------------------------------------
1. Realizar novos testes com logs ampliados e maior diversidade de requisições.
2. Adicionar padrões para detecção de erros HTTP 429 e 451.
3. Implementar mecanismos de agrupamento por IP para identificar ataques
   distribuídos (ex.: DoS via múltiplas origens).
4. Manter histórico de variação do coeficiente de cobertura ao longo do tempo.

-------------------------------------------------------------------------------
CONCLUSÃO
-------------------------------------------------------------------------------
O teste do filtro `mitre-t1071.conf` demonstrou efetividade inicial na detecção
de falhas e requisições anômalas via HTTP/S. O coeficiente de cobertura de
8,03% confirma o funcionamento correto do filtro e sua adequação parcial ao
ambiente Nginx. Com ajustes incrementais, espera-se ampliar a capacidade de
detecção sem comprometer o desempenho ou gerar falsos positivos.

-------------------------------------------------------------------------------
FIM DO APÊNDICE E
-------------------------------------------------------------------------------
"""

# Caminho de saída
file_path_e = "/mnt/data/APENDICE_E_README_T1071_ABNT.txt"

# Gravação do arquivo
with open(file_path_e, "w", encoding="utf-8") as file:
    file.write(apendice_e)

file_path_e

