# Relatório da Sprint 1 - SQL Injection e SQLMap

## Arthur de Melo Viana - 211029147

Após configurar o Kali Linux no VMWare, subi os contêineres da API e do WEB e fiz a integração. Contudo, para os testes realizados com o SQLMap, utilizei apenas do back-end.
Os testes realizados, como precisavam de autenticação, foram feitos em cima de um header capturado por meio da ferramenta OWASP Zap ao realizar login no Browser Mozilla Firefox. 

### api/universities/

Header (request.txt):

```
GET http://localhost:8000/api/universities/ HTTP/1.1
host: localhost:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Connection: keep-alive
Cookie: csrftoken=xkZ6wrqgni2vgRMBamztJRNqegkN7oIp; sessionid=es1hh1ya7kznolvjmub5l4c9nmsjw7ro
Upgrade-Insecure-Requests: 1
```

Comando utilizado: sqlmap -r request.txt --batch

Output:
```
[*] starting @ 11:13:39 /2024-11-27/

[11:13:39] [INFO] parsing HTTP request from 'request.txt'
[11:13:40] [WARNING] you've provided target URL without any GET parameters (e.g. 'http://www.site.com/article.php?id=1') and without providing any POST parameters through option '--data'
do you want to try URI injections in the target URL itself? [Y/n/q] Y
Cookie parameter 'csrftoken' appears to hold anti-CSRF token. Do you want sqlmap to automatically update it in further requests? [y/N] N
[11:13:40] [INFO] testing connection to the target URL
[11:13:40] [INFO] testing if the target URL content is stable
you provided a HTTP Cookie header value, while target URL provides its own cookies within HTTP Set-Cookie header which intersect with yours. Do you want to merge them in further requests? [Y/n] Y
[11:13:40] [WARNING] target URL content is not stable (i.e. content differs). sqlmap will base the page comparison on a sequence matcher. If no dynamic nor injectable parameters are detected, or in case of junk results, refer to user's manual paragraph 'Page comparison'
how do you want to proceed? [(C)ontinue/(s)tring/(r)egex/(q)uit] C
[11:13:40] [INFO] testing if URI parameter '#1*' is dynamic
got a 301 redirect to 'http://localhost:8000/api/universities/5831/'. Do you want to follow? [Y/n] Y
[11:13:41] [WARNING] URI parameter '#1*' does not appear to be dynamic
[11:13:41] [WARNING] heuristic (basic) test shows that URI parameter '#1*' might not be injectable
[11:13:41] [INFO] testing for SQL injection on URI parameter '#1*'
[11:13:41] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[11:13:42] [WARNING] reflective value(s) found and filtering out
[11:13:44] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[11:13:45] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[11:13:46] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[11:13:47] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[11:13:47] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[11:13:48] [INFO] testing 'Generic inline queries'
[11:13:48] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[11:13:48] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[11:13:49] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[11:13:49] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[11:13:49] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[11:13:50] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[11:13:51] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] Y
[11:13:51] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[11:13:53] [WARNING] URI parameter '#1*' does not seem to be injectable
[11:13:53] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'
[11:13:53] [WARNING] HTTP error codes detected during run:
404 (Not Found) - 10 times, 500 (Internal Server Error) - 4 times

[*] ending @ 11:13:53 /2024-11-27/
```
Comando utilizado: sqlmap -r request.txt --batch --level=5 --risk=3
Output:
```
[*] starting @ 11:24:38 /2024-11-27/

[11:24:38] [INFO] parsing HTTP request from 'request.txt'
[11:24:38] [WARNING] you've provided target URL without any GET parameters (e.g. 'http://www.site.com/article.php?id=1') and without providing any POST parameters through option '--data'
do you want to try URI injections in the target URL itself? [Y/n/q] Y
Cookie parameter 'csrftoken' appears to hold anti-CSRF token. Do you want sqlmap to automatically update it in further requests? [y/N] N
[11:24:38] [INFO] testing connection to the target URL
[11:24:38] [INFO] testing if the target URL content is stable
you provided a HTTP Cookie header value, while target URL provides its own cookies within HTTP Set-Cookie header which intersect with yours. Do you want to merge them in further requests? [Y/n] Y
[11:24:38] [WARNING] target URL content is not stable (i.e. content differs). sqlmap will base the page comparison on a sequence matcher. If no dynamic nor injectable parameters are detected, or in case of junk results, refer to user's manual paragraph 'Page comparison'
how do you want to proceed? [(C)ontinue/(s)tring/(r)egex/(q)uit] C
[11:24:38] [INFO] testing if URI parameter '#1*' is dynamic
got a 301 redirect to 'http://localhost:8000/api/universities/5742/'. Do you want to follow? [Y/n] Y
[11:24:39] [WARNING] URI parameter '#1*' does not appear to be dynamic
[11:24:39] [WARNING] heuristic (basic) test shows that URI parameter '#1*' might not be injectable
[11:24:39] [INFO] testing for SQL injection on URI parameter '#1*'
[11:24:39] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[11:24:40] [WARNING] reflective value(s) found and filtering out
[11:24:40] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[11:24:41] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[11:24:41] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[11:24:41] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[11:24:41] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[11:24:41] [INFO] testing 'Generic inline queries'
[11:24:42] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[11:24:42] [WARNING] time-based comparison requires larger statistical model, please wait................ (done)
[11:24:43] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[11:24:43] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[11:24:43] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[11:24:43] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[11:24:43] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[11:24:43] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] Y
[11:24:43] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[11:24:44] [WARNING] URI parameter '#1*' does not seem to be injectable
[11:24:44] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'
[11:24:44] [WARNING] HTTP error codes detected during run:
404 (Not Found) - 3 times, 500 (Internal Server Error) - 1 times

[*] ending @ 11:24:44 /2024-11-27/
```

### /api/university-user/
Header (request.txt):

```
GET http://localhost:8000/api/university-user/ HTTP/1.1
host: localhost:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Connection: keep-alive
Cookie: csrftoken=zYqIyZtXO4TtjvEJUTtigM2rAnFAL71o; sessionid=j82fxq43osmvn5c7ikuqmwfrylcxh8ya
Upgrade-Insecure-Requests: 1
```

Comando utilizado: sqlmap -r request.txt --batch

Output:

```
[*] starting @ 13:24:40 /2024-11-27/

[13:24:40] [INFO] parsing HTTP request from 'request.txt'
[13:24:40] [WARNING] you've provided target URL without any GET parameters (e.g. 'http://www.site.com/article.php?id=1') and without providing any POST parameters through option '--data'
do you want to try URI injections in the target URL itself? [Y/n/q] Y
Cookie parameter 'csrftoken' appears to hold anti-CSRF token. Do you want sqlmap to automatically update it in further requests? [y/N] N
[13:24:40] [INFO] testing connection to the target URL
[13:24:41] [INFO] testing if the target URL content is stable
you provided a HTTP Cookie header value, while target URL provides its own cookies within HTTP Set-Cookie header which intersect with yours. Do you want to merge them in further requests? [Y/n] Y
[13:24:41] [WARNING] target URL content is not stable (i.e. content differs). sqlmap will base the page comparison on a sequence matcher. If no dynamic nor injectable parameters are detected, or in case of junk results, refer to user's manual paragraph 'Page comparison'
how do you want to proceed? [(C)ontinue/(s)tring/(r)egex/(q)uit] C
[13:24:41] [INFO] testing if URI parameter '#1*' is dynamic
got a 301 redirect to 'http://localhost:8000/api/university-user/1540/'. Do you want to follow? [Y/n] Y
[13:24:42] [WARNING] URI parameter '#1*' does not appear to be dynamic
[13:24:42] [WARNING] heuristic (basic) test shows that URI parameter '#1*' might not be injectable
[13:24:42] [INFO] testing for SQL injection on URI parameter '#1*'
[13:24:42] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[13:24:43] [WARNING] reflective value(s) found and filtering out
[13:24:46] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[13:24:46] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[13:24:47] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[13:24:47] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[13:24:48] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[13:24:48] [INFO] testing 'Generic inline queries'
[13:24:49] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[13:24:49] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[13:24:50] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[13:24:50] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[13:24:50] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[13:24:51] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[13:24:52] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] Y
[13:24:52] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[13:24:54] [WARNING] URI parameter '#1*' does not seem to be injectable
[13:24:54] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'
[13:24:54] [WARNING] HTTP error codes detected during run:
500 (Internal Server Error) - 4 times, 404 (Not Found) - 9 times

[*] ending @ 13:24:54 /2024-11-27/
```

A fim de aumentar um pouco a quantidade de testes, realizei mais testes com um comando modificado:

Comando utilizado: sqlmap -r request.txt --batch --level=3 --risk=2

Output:

```
[*] starting @ 13:11:26 /2024-11-27/

[13:11:26] [INFO] parsing HTTP request from 'request.txt'
[13:11:26] [WARNING] you've provided target URL without any GET parameters (e.g. 'http://www.site.com/article.php?id=1') and without providing any POST parameters through option '--data'
do you want to try URI injections in the target URL itself? [Y/n/q] Y
Cookie parameter 'csrftoken' appears to hold anti-CSRF token. Do you want sqlmap to automatically update it in further requests? [y/N] N
[13:11:26] [INFO] testing connection to the target URL
[13:11:27] [INFO] testing if the target URL content is stable
you provided a HTTP Cookie header value, while target URL provides its own cookies within HTTP Set-Cookie header which intersect with yours. Do you want to merge them in further requests? [Y/n] Y
[13:11:27] [WARNING] target URL content is not stable (i.e. content differs). sqlmap will base the page comparison on a sequence matcher. If no dynamic nor injectable parameters are detected, or in case of junk results, refer to user's manual paragraph 'Page comparison'
how do you want to proceed? [(C)ontinue/(s)tring/(r)egex/(q)uit] C
[13:11:27] [INFO] testing if URI parameter '#1*' is dynamic
got a 301 redirect to 'http://localhost:8000/api/university-user/9844/'. Do you want to follow? [Y/n] Y
[13:11:28] [WARNING] URI parameter '#1*' does not appear to be dynamic
[13:11:28] [WARNING] heuristic (basic) test shows that URI parameter '#1*' might not be injectable
[13:11:28] [INFO] testing for SQL injection on URI parameter '#1*'
[13:11:29] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[13:11:29] [WARNING] reflective value(s) found and filtering out
[13:11:40] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause (subquery - comment)'
[13:11:46] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause (comment)'
[13:11:51] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause (MySQL comment)'
[13:11:56] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause (Microsoft Access comment)'
[13:12:03] [INFO] testing 'MySQL RLIKE boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause'
[13:12:13] [INFO] testing 'MySQL AND boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause (MAKE_SET)'
[13:12:24] [INFO] testing 'PostgreSQL AND boolean-based blind - WHERE or HAVING clause (CAST)'
[13:12:34] [INFO] testing 'Oracle AND boolean-based blind - WHERE or HAVING clause (CTXSYS.DRITHSX.SN)'
[13:12:39] [INFO] testing 'SQLite AND boolean-based blind - WHERE, HAVING, GROUP BY or HAVING clause (JSON)'
[13:12:49] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[13:12:50] [INFO] testing 'PostgreSQL boolean-based blind - Parameter replace'
[13:12:50] [INFO] testing 'Microsoft SQL Server/Sybase boolean-based blind - Parameter replace'
[13:12:50] [INFO] testing 'Oracle boolean-based blind - Parameter replace'
[13:12:51] [INFO] testing 'Informix boolean-based blind - Parameter replace'
[13:12:51] [INFO] testing 'Microsoft Access boolean-based blind - Parameter replace'
[13:12:51] [INFO] testing 'Boolean-based blind - Parameter replace (DUAL)'
[13:12:51] [INFO] testing 'Boolean-based blind - Parameter replace (DUAL - original value)'
[13:12:52] [INFO] testing 'Boolean-based blind - Parameter replace (CASE)'
[13:12:52] [INFO] testing 'Boolean-based blind - Parameter replace (CASE - original value)'
[13:12:53] [INFO] testing 'MySQL >= 5.0 boolean-based blind - ORDER BY, GROUP BY clause'
[13:12:53] [INFO] testing 'MySQL >= 5.0 boolean-based blind - ORDER BY, GROUP BY clause (original value)'
[13:12:54] [INFO] testing 'MySQL < 5.0 boolean-based blind - ORDER BY, GROUP BY clause'
[13:12:54] [INFO] testing 'PostgreSQL boolean-based blind - ORDER BY, GROUP BY clause'
[13:12:54] [INFO] testing 'Microsoft SQL Server/Sybase boolean-based blind - ORDER BY clause'
[13:12:55] [INFO] testing 'Oracle boolean-based blind - ORDER BY, GROUP BY clause'
[13:12:55] [INFO] testing 'HAVING boolean-based blind - WHERE, GROUP BY clause'
[13:13:06] [INFO] testing 'PostgreSQL boolean-based blind - Stacked queries'
[13:13:08] [INFO] testing 'Microsoft SQL Server/Sybase boolean-based blind - Stacked queries (IF)'
[13:13:14] [INFO] testing 'MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)'
[13:13:16] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[13:13:19] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (UPDATEXML)'
[13:13:23] [INFO] testing 'MySQL >= 4.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)'
[13:13:27] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[13:13:30] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[13:13:33] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (CONVERT)'
[13:13:37] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (CONCAT)'
[13:13:40] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[13:13:41] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (UTL_INADDR.GET_HOST_ADDRESS)'
[13:13:43] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (CTXSYS.DRITHSX.SN)'
[13:13:45] [INFO] testing 'Firebird AND error-based - WHERE or HAVING clause'
[13:13:48] [INFO] testing 'MonetDB AND error-based - WHERE or HAVING clause'
[13:13:52] [INFO] testing 'Vertica AND error-based - WHERE or HAVING clause'
[13:13:52] [INFO] testing 'IBM DB2 AND error-based - WHERE or HAVING clause'
[13:13:53] [INFO] testing 'ClickHouse AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause'
[13:13:56] [INFO] testing 'MySQL >= 5.1 error-based - PROCEDURE ANALYSE (EXTRACTVALUE)'
[13:13:59] [INFO] testing 'MySQL >= 5.0 error-based - Parameter replace (FLOOR)'
[13:14:00] [INFO] testing 'MySQL >= 5.1 error-based - Parameter replace (EXTRACTVALUE)'
[13:14:00] [INFO] testing 'PostgreSQL error-based - Parameter replace'
[13:14:00] [INFO] testing 'Microsoft SQL Server/Sybase error-based - Parameter replace'
[13:14:00] [INFO] testing 'Oracle error-based - Parameter replace'
[13:14:00] [INFO] testing 'MySQL >= 5.1 error-based - ORDER BY, GROUP BY clause (EXTRACTVALUE)'
[13:14:00] [INFO] testing 'MySQL >= 4.1 error-based - ORDER BY, GROUP BY clause (FLOOR)'
[13:14:01] [INFO] testing 'PostgreSQL error-based - ORDER BY, GROUP BY clause'
[13:14:01] [INFO] testing 'Microsoft SQL Server/Sybase error-based - Stacking (EXEC)'
[13:14:03] [INFO] testing 'Generic inline queries'
[13:14:03] [INFO] testing 'MySQL inline queries'
[13:14:04] [INFO] testing 'PostgreSQL inline queries'
[13:14:04] [INFO] testing 'Microsoft SQL Server/Sybase inline queries'
[13:14:04] [INFO] testing 'Oracle inline queries'
[13:14:04] [INFO] testing 'SQLite inline queries'
[13:14:04] [INFO] testing 'Firebird inline queries'
[13:14:04] [INFO] testing 'ClickHouse inline queries'
[13:14:05] [INFO] testing 'MySQL >= 5.0.12 stacked queries (comment)'
[13:14:06] [INFO] testing 'MySQL >= 5.0.12 stacked queries'
[13:14:09] [INFO] testing 'MySQL >= 5.0.12 stacked queries (query SLEEP - comment)'
[13:14:11] [INFO] testing 'MySQL < 5.0.12 stacked queries (BENCHMARK - comment)'
[13:14:12] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[13:14:14] [INFO] testing 'PostgreSQL stacked queries (heavy query - comment)'
[13:14:16] [INFO] testing 'PostgreSQL < 8.2 stacked queries (Glibc - comment)'
[13:14:17] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[13:14:18] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (DECLARE - comment)'
[13:14:20] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[13:14:21] [INFO] testing 'Oracle stacked queries (heavy query - comment)'
[13:14:23] [INFO] testing 'IBM DB2 stacked queries (heavy query - comment)'
[13:14:23] [INFO] testing 'SQLite > 2.0 stacked queries (heavy query - comment)'
[13:14:24] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[13:14:27] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (SLEEP)'
[13:14:30] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (SLEEP - comment)'
[13:14:32] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP - comment)'
[13:14:34] [INFO] testing 'MySQL < 5.0.12 AND time-based blind (BENCHMARK)'
[13:14:37] [INFO] testing 'MySQL > 5.0.12 AND time-based blind (heavy query)'
[13:14:38] [INFO] testing 'MySQL >= 5.0.12 RLIKE time-based blind'
[13:14:41] [INFO] testing 'MySQL >= 5.0.12 RLIKE time-based blind (query SLEEP)'
[13:14:44] [INFO] testing 'MySQL AND time-based blind (ELT)'
[13:14:47] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[13:14:50] [INFO] testing 'PostgreSQL AND time-based blind (heavy query)'
[13:14:53] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[13:14:57] [INFO] testing 'Microsoft SQL Server/Sybase AND time-based blind (heavy query)'
[13:15:00] [INFO] testing 'Oracle AND time-based blind'
[13:15:02] [INFO] testing 'Oracle AND time-based blind (heavy query)'
[13:15:05] [INFO] testing 'IBM DB2 AND time-based blind (heavy query)'
[13:15:07] [INFO] testing 'SQLite > 2.0 AND time-based blind (heavy query)'
[13:15:09] [INFO] testing 'Informix AND time-based blind (heavy query)'
[13:15:12] [INFO] testing 'MySQL >= 5.1 time-based blind (heavy query) - PROCEDURE ANALYSE (EXTRACTVALUE)'
[13:15:15] [INFO] testing 'MySQL >= 5.0.12 time-based blind - Parameter replace'
[13:15:15] [INFO] testing 'MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)'
[13:15:15] [INFO] testing 'PostgreSQL > 8.1 time-based blind - Parameter replace'
[13:15:15] [INFO] testing 'Oracle time-based blind - Parameter replace (DBMS_LOCK.SLEEP)'
[13:15:15] [INFO] testing 'Oracle time-based blind - Parameter replace (DBMS_PIPE.RECEIVE_MESSAGE)'
[13:15:15] [INFO] testing 'MySQL >= 5.0.12 time-based blind - ORDER BY, GROUP BY clause'
[13:15:15] [INFO] testing 'PostgreSQL > 8.1 time-based blind - ORDER BY, GROUP BY clause'
[13:15:16] [INFO] testing 'Oracle time-based blind - ORDER BY, GROUP BY clause (DBMS_LOCK.SLEEP)'
[13:15:16] [INFO] testing 'Oracle time-based blind - ORDER BY, GROUP BY clause (DBMS_PIPE.RECEIVE_MESSAGE)'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] Y
[13:15:16] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[13:15:23] [INFO] testing 'Generic UNION query (random number) - 1 to 10 columns'
[13:15:30] [INFO] testing 'MySQL UNION query (NULL) - 1 to 10 columns'
[13:15:37] [INFO] testing 'MySQL UNION query (random number) - 1 to 10 columns'
[13:15:43] [WARNING] URI parameter '#1*' does not seem to be injectable
other non-custom parameters found. Do you want to process them too? [Y/n/q] Y
[13:15:43] [INFO] ignoring Cookie parameter 'csrftoken'
[13:15:43] [WARNING] Cookie parameter 'sessionid' does not appear to be dynamic
do you want to URL encode cookie values (implementation specific)? [Y/n] Y
[13:15:43] [CRITICAL] not authorized, try to provide right HTTP authentication type and valid credentials (401). If this is intended, try to rerun by providing a valid value for option '--ignore-code'
[13:15:43] [WARNING] HTTP error codes detected during run:
404 (Not Found) - 304 times, 500 (Internal Server Error) - 66 times, 401 (Unauthorized) - 1 times

[*] ending @ 13:15:43 /2024-11-27/
```

Contudo, desta vez, ocorreu um erro que não constava nos logs da execução anterior. Que seria o 401, mesmo estando autenticado como admin.

### Dificuldades

Num primeiro momento, as principais dificuldades foram referentes ao Docker do projeto. O qual funcionou apenas na máquina virtual Kali Linux.
Após isso, estudei o básico de SQL Injection no material indicado pelo monitor e tentei fazer os testes nos caminhos api/universities e api/university-user.
Entretanto, ao tentar fazer os testes, percebi que precisava de autenticação, o que foi a maior dificuldade até então. Para isso, resolvi estudando o módulo pago de SQLMap Essentials no material recomendado do HTB. Dessa forma, percebi que era necessário captar o header, o qual eu fiz por meio do OWASP Zap, ferramenta que pretendo utilizar futuramente para complementar os testes feitos no SQLMap.

### Próximos passos

Como não encontrei nenhum tipo de falha, apenas falsos positivos. O ideal seria aprimorar os comandos utilizados, dado que foram utilizados apenas de comandos básicos. O material fornecido especifica diversos casos diferentes nos quais podem ser utilizadas outras formas de testes para lidar com idiossincrasias do projeto em questão. Ademais, seria interessante estudar a causa do erro 401 que aconteceu mesmo autenticado.