# README.t1110
# --------------------------------------------------------------------
# MITRE ATT&CK: T1110 - Brute Force: SSH
# Documentação de cobertura e funcionamento do filtro Fail2Ban
# --------------------------------------------------------------------

## Objetivo
Este filtro foi criado para detectar tentativas de autenticação não autorizadas via SSH,
incluindo usuários inválidos, falhas de senha e desconexões antes do login (pré-auth).

## Testes realizados
Comando de teste:
    fail2ban-regex /var/log/auth.log /etc/fail2ban/filter.d/mitre-t1110.conf

Resultado obtido:
    Total de linhas processadas: 22.177
    Linhas correspondentes (matched): 12.161
    Linhas ignoradas: 0
    Linhas não correspondentes (missed): 10.016

## Cobertura
Cálculo da cobertura:
    cobertura = linhas correspondentes / total de linhas
    cobertura = 12.161 / 22.177 ≈ 54.8 %

Interpretação:
- Cerca de 55% das linhas do log são capturadas pelo filtro.
- Isso é esperado, pois nem todas as linhas de /var/log/auth.log representam tentativas de login.
- O filtro está focado em capturar **tentativas de acesso SSH maliciosas ou inválidas**.

## Considerações
- Cobertura de ~55% é **normal e adequada**, considerando que grande parte do log contém eventos legítimos.
- O filtro captura:
    - Falhas de autenticação PAM
    - Tentativas de senha inválidas (usuário válido ou inválido)
    - Usuários inválidos
    - Desconexões pré-auth
- Nenhum `ignoreregex` foi definido, garantindo que todas as tentativas suspeitas sejam analisadas.

## Status atual
 - Filtro válido (sem erros de sintaxe).  
 - Captura de ataques SSH confirmada.  
 - Cobertura estimada em ~55% do log analisado (27/Set/2025).  
 - Chain MITRE-T1110 no iptables recebendo corretamente os IPs banidos.

## Roadmap de evolução
1. **Monitoramento contínuo**  
   - Verificar periodicamente `fail2ban-client status mitre-t1110` para garantir bloqueio de novos IPs.

2. **Aprimoramento do filtro**  
   - Adicionar padrões adicionais se forem identificadas novas formas de ataque (ex.: tentativas com usuários comuns "ubuntu", "admin", "test", etc.).

3. **Exceções e Ignore**  
   - Definir `ignoreregex` se houver IPs confiáveis ou faixas internas que não devem ser bloqueadas.

4. **Métricas contínuas**  
   - Executar testes semanais com `fail2ban-regex` para monitorar evolução da cobertura.
   - Documentar percentual de cobertura ao longo do tempo (histórico).

