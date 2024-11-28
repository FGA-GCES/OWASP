# Relatório Sprint 1

Arthur Grandão de Mello - 211039250

Grupo OWASP - Sub-grupo 1

Para esta sprint eu procurei realizar os módulos do HTB Academy recomendados pelo monitor para poder realizar os testes de SQLi nas rotas da API do Mec Energia designadas pelo mesmo.

## Dificuldades

Tive dificuldades em me organizar para estudar.

## Próximos passos

Me aprofundar mais no curso do HTB Academy para conseguir melhores resultados nos futuros testes.

## Resultados

Eu realizei testes com o `SQLMap` nas rotas `/api/users`, `/api/users/?id` e `api/users/change-user-password/`.

## /api/users/

```
┌──(grandao㉿kali)-[~/Projetos]
└─$ sqlmap -u http://localhost:8000/api/users --headers="Cookie: csrftoken=uJi4syyAb4ZP6VOoIMefBMYY5ZMWH61K; sessionid=wj9ia2d13e962lah172txboazulrmmf4"
        ___
       __H__
 ___ ___[(]_____ ___ ___  {1.8.7#stable}
|_ -| . [)]     | .'| . |
|___|_  [)]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 23:35:48 /2024-11-27/

[23:35:49] [WARNING] you've provided target URL without any GET parameters (e.g. 'http://www.site.com/article.php?id=1') and without providing any POST parameters through option '--data'
do you want to try URI injections in the target URL itself? [Y/n/q] y
[23:35:50] [INFO] testing connection to the target URL
got a 301 redirect to 'http://localhost:8000/api/users/'. Do you want to follow? [Y/n] y
[23:35:57] [INFO] testing if the target URL content is stable
[23:35:57] [WARNING] URI parameter '#1*' does not appear to be dynamic
[23:35:58] [WARNING] heuristic (basic) test shows that URI parameter '#1*' might not be injectable
[23:35:58] [INFO] testing for SQL injection on URI parameter '#1*'
[23:35:58] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[23:35:59] [WARNING] reflective value(s) found and filtering out
[23:36:03] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[23:36:03] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[23:36:04] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[23:36:05] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[23:36:05] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[23:36:06] [INFO] testing 'Generic inline queries'
[23:36:06] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[23:36:06] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[23:36:07] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[23:36:07] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[23:36:08] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[23:36:09] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[23:36:09] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] y
[23:36:14] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[23:36:15] [WARNING] URI parameter '#1*' does not seem to be injectable
[23:36:15] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'
[23:36:15] [WARNING] HTTP error codes detected during run:
404 (Not Found) - 69 times, 500 (Internal Server Error) - 3 times

[*] ending @ 23:36:15 /2024-11-27/
```

## /api/users/?id/

```
┌──(grandao㉿kali)-[~/Projetos]
└─$ sqlmap -u http://localhost:8000/api/users/?id=1 --headers="Cookie: csrftoken=uJi4syyAb4ZP6VOoIMefBMYY5ZMWH61K; sessionid=wj9ia2d13e962lah172txboazulrmmf4"
        ___
       __H__
 ___ ___[.]_____ ___ ___  {1.8.7#stable}
|_ -| . [.]     | .'| . |
|___|_  [.]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 23:32:54 /2024-11-27/

[23:32:54] [INFO] testing connection to the target URL
[23:32:54] [INFO] checking if the target is protected by some kind of WAF/IPS
[23:32:54] [INFO] testing if the target URL content is stable
[23:32:55] [INFO] target URL content is stable
[23:32:55] [INFO] testing if GET parameter 'id' is dynamic
[23:32:56] [WARNING] GET parameter 'id' does not appear to be dynamic
[23:32:56] [WARNING] heuristic (basic) test shows that GET parameter 'id' might not be injectable
[23:32:56] [INFO] testing for SQL injection on GET parameter 'id'
[23:32:56] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[23:32:57] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[23:32:57] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[23:32:57] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[23:32:58] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[23:32:58] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[23:32:59] [INFO] testing 'Generic inline queries'
[23:32:59] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[23:32:59] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[23:32:59] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[23:33:00] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[23:33:00] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[23:33:01] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[23:33:01] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] y
[23:33:05] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[23:33:06] [WARNING] GET parameter 'id' does not seem to be injectable
[23:33:06] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'

[*] ending @ 23:33:06 /2024-11-27/
```

```
┌──(grandao㉿kali)-[~/Projetos]
└─$ sqlmap -u http://localhost:8000/api/users/?*id=1 --headers="Cookie: csrftoken=uJi4syyAb4ZP6VOoIMefBMYY5ZMWH61K; sessionid=wj9ia2d13e962lah172txboazulrmmf4"
        ___
       __H__
 ___ ___[)]_____ ___ ___  {1.8.7#stable}
|_ -| . ["]     | .'| . |
|___|_  [)]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 23:39:18 /2024-11-27/

custom injection marker ('*') found in option '-u'. Do you want to process it? [Y/n/q] y
[23:39:23] [INFO] testing connection to the target URL
[23:39:23] [INFO] checking if the target is protected by some kind of WAF/IPS
[23:39:24] [INFO] testing if the target URL content is stable
[23:39:24] [INFO] target URL content is stable
[23:39:24] [INFO] testing if URI parameter '#1*' is dynamic
[23:39:24] [WARNING] URI parameter '#1*' does not appear to be dynamic
[23:39:24] [WARNING] heuristic (basic) test shows that URI parameter '#1*' might not be injectable
[23:39:24] [INFO] testing for SQL injection on URI parameter '#1*'
[23:39:24] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[23:39:25] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[23:39:25] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[23:39:25] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[23:39:26] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[23:39:26] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[23:39:26] [INFO] testing 'Generic inline queries'
[23:39:26] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[23:39:27] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[23:39:27] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[23:39:27] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[23:39:28] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[23:39:28] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[23:39:28] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] y
[23:39:31] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[23:39:31] [WARNING] URI parameter '#1*' does not seem to be injectable
[23:39:31] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'

[*] ending @ 23:39:31 /2024-11-27/
```

## api/users/change-user-password

```
┌──(grandao㉿kali)-[~/Projetos]
└─$ sqlmap -r request1.txt
        ___
       __H__
 ___ ___[)]_____ ___ ___  {1.8.7#stable}
|_ -| . ["]     | .'| . |
|___|_  [,]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 23:49:00 /2024-11-27/

[23:49:00] [INFO] parsing HTTP request from 'request1.txt'
Multipart-like data found in POST body. Do you want to process it? [Y/n/q] y
Cookie parameter 'csrftoken' appears to hold anti-CSRF token. Do you want sqlmap to automatically update it in further requests? [y/N] n
[23:49:11] [INFO] testing connection to the target URL
[23:49:12] [WARNING] the web server responded with an HTTP error code (403) which could interfere with the results of the tests
[23:49:12] [INFO] checking if the target is protected by some kind of WAF/IPS
you provided a HTTP Cookie header value, while target URL provides its own cookies within HTTP Set-Cookie header which intersect with yours. Do you want to merge them in further requests? [Y/n] y
[23:49:15] [WARNING] reflective value(s) found and filtering out
[23:49:15] [INFO] testing if the target URL content is stable
[23:49:16] [WARNING] target URL content is not stable (i.e. content differs). sqlmap will base the page comparison on a sequence matcher. If no dynamic nor injectable parameters are detected, or in case of junk results, refer to user's manual paragraph 'Page comparison'
how do you want to proceed? [(C)ontinue/(s)tring/(r)egex/(q)uit] c
[23:49:37] [INFO] ignoring (custom) POST parameter 'MULTIPART csrfmiddlewaretoken'
[23:49:37] [INFO] testing if (custom) POST parameter 'MULTIPART first_name' is dynamic
[23:49:38] [WARNING] (custom) POST parameter 'MULTIPART first_name' does not appear to be dynamic
[23:49:38] [WARNING] heuristic (basic) test shows that (custom) POST parameter 'MULTIPART first_name' might not be injectable
[23:49:39] [INFO] testing for SQL injection on (custom) POST parameter 'MULTIPART first_name'
[23:49:39] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[23:49:43] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[23:49:43] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[23:49:44] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[23:49:45] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[23:49:45] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[23:49:46] [INFO] testing 'Generic inline queries'
[23:49:46] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[23:49:46] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[23:49:47] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[23:49:47] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[23:49:47] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[23:49:48] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[23:49:48] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] y
[23:49:52] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[23:49:53] [WARNING] (custom) POST parameter 'MULTIPART first_name' does not seem to be injectable
[23:49:53] [INFO] testing if (custom) POST parameter 'MULTIPART last_name' is dynamic
[23:49:54] [WARNING] (custom) POST parameter 'MULTIPART last_name' does not appear to be dynamic
[23:49:54] [WARNING] heuristic (basic) test shows that (custom) POST parameter 'MULTIPART last_name' might not be injectable
[23:49:54] [INFO] testing for SQL injection on (custom) POST parameter 'MULTIPART last_name'
[23:49:54] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[23:49:57] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[23:49:57] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[23:49:58] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[23:49:58] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[23:49:59] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[23:49:59] [INFO] testing 'Generic inline queries'
[23:49:59] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[23:50:00] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[23:50:00] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[23:50:01] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[23:50:01] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[23:50:02] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[23:50:02] [INFO] testing 'Oracle AND time-based blind'
[23:50:03] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[23:50:04] [WARNING] (custom) POST parameter 'MULTIPART last_name' does not seem to be injectable
[23:50:04] [INFO] testing if (custom) POST parameter 'MULTIPART password' is dynamic
[23:50:04] [WARNING] (custom) POST parameter 'MULTIPART password' does not appear to be dynamic
[23:50:04] [WARNING] heuristic (basic) test shows that (custom) POST parameter 'MULTIPART password' might not be injectable
[23:50:05] [INFO] testing for SQL injection on (custom) POST parameter 'MULTIPART password'
[23:50:05] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[23:50:07] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[23:50:08] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[23:50:08] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[23:50:09] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[23:50:09] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[23:50:10] [INFO] testing 'Generic inline queries'
[23:50:10] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[23:50:10] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[23:50:11] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[23:50:11] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[23:50:11] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[23:50:12] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[23:50:12] [INFO] testing 'Oracle AND time-based blind'
[23:50:13] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[23:50:14] [WARNING] (custom) POST parameter 'MULTIPART password' does not seem to be injectable
[23:50:14] [INFO] testing if (custom) POST parameter 'MULTIPART email' is dynamic
[23:50:15] [WARNING] (custom) POST parameter 'MULTIPART email' does not appear to be dynamic
[23:50:15] [WARNING] heuristic (basic) test shows that (custom) POST parameter 'MULTIPART email' might not be injectable
[23:50:15] [INFO] testing for SQL injection on (custom) POST parameter 'MULTIPART email'
[23:50:15] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[23:50:17] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[23:50:18] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[23:50:18] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[23:50:19] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[23:50:19] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[23:50:20] [INFO] testing 'Generic inline queries'
[23:50:20] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[23:50:20] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[23:50:21] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[23:50:21] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[23:50:22] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[23:50:22] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[23:50:23] [INFO] testing 'Oracle AND time-based blind'
[23:50:23] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[23:50:25] [WARNING] (custom) POST parameter 'MULTIPART email' does not seem to be injectable
[23:50:25] [INFO] testing if (custom) POST parameter 'MULTIPART type' is dynamic
[23:50:25] [WARNING] (custom) POST parameter 'MULTIPART type' does not appear to be dynamic
[23:50:25] [WARNING] heuristic (basic) test shows that (custom) POST parameter 'MULTIPART type' might not be injectable
[23:50:25] [INFO] testing for SQL injection on (custom) POST parameter 'MULTIPART type'
[23:50:25] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[23:50:28] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[23:50:28] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[23:50:29] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[23:50:29] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[23:50:30] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[23:50:30] [INFO] testing 'Generic inline queries'
[23:50:31] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[23:50:31] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[23:50:31] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[23:50:32] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[23:50:32] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[23:50:33] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[23:50:33] [INFO] testing 'Oracle AND time-based blind'
[23:50:34] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[23:50:35] [WARNING] (custom) POST parameter 'MULTIPART type' does not seem to be injectable
[23:50:35] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'
[23:50:35] [WARNING] HTTP error codes detected during run:
403 (Forbidden) - 423 times

[*] ending @ 23:50:35 /2024-11-27/
```
