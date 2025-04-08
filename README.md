# xianqi kindergarten management system stu_list.php SQL injection
## Official website: 
http://soft.xqkj.com.cn/p14.html
## Affected version:
v2.0 bulid20190808
## Download link:
https://zdown.chinaz.com/201908/xqyeyzxglxt_v2.0.zip
## Vulnerability description: 
There is a SQL injection vulnerability in stu_list.php of the Xianqi kindergarten management system. The affected functions are "child management" - "child archive" - ​​"query". The URL is http://10.211.55.3/cve/xq/stu_list.php. Malicious attackers can obtain database permissions through this vulnerability after logging in to the system, and further exploitation can obtain server permissions.
Vulnerability analysis: The "sex" parameter in stu_list.php is not filtered, and there is a SQL injection vulnerability.
<img width="1505" alt="image" src="https://github.com/user-attachments/assets/dd3d234c-e5e8-43c8-ae59-d0f888e95f49" />
## Vulnerability verification:
```
GET /cve/xq/stu_list.php?action=search&time0=2025-04-01&time1=2025-04-02&sex=%E5%A5%B3&nation=%E5%A3%AE%E6%97%8F&banji=1&isok=2&time00=2025-04-01&time11=2025-04-02&keywords=1111 HTTP/1.1
Host: 10.211.55.3
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:137.0) Gecko/20100101 Firefox/137.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Referer: http://10.211.55.3/cve/xq/stu_list.php?action=search&time0=2025-04-01&time1=2025-04-02&sex=%E5%A5%B3&nation=%E5%A3%AE%E6%97%8F&banji=1&isok=2&time00=&time11=&keywords=
Cookie: PHPSESSID=g5g68mc4d66u792jdlvia1cso4
Upgrade-Insecure-Requests: 1
Priority: u=4
```
<img width="1165" alt="image" src="https://github.com/user-attachments/assets/6e3b5f25-3cd4-4a87-be08-9b47280d4e82" />
## Repair suggestions:

Use Prepared Statements (Parameterized Queries): Always use prepared statements with parameterized queries to separate SQL code from data inputs, ensuring user inputs are treated strictly as data.
Input Validation and Sanitization: Validate and sanitize all user inputs by enforcing strict rules (e.g., regex or type checking) to ensure they conform to expected formats and remove harmful characters.
Implement Least Privilege Principle: Configure database accounts with minimal permissions to reduce the impact of a potential SQL injection attack, ensuring no excessive privileges are granted.
