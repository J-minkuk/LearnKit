# GROUP BY

---

## 예제 테이블
### users
id | name | language_id | framework_id
---|------|-------------|--------------
1 | Jo | 1 | 1
2 | Min | 1 | 10
3 | Kuk | 3 | 3
4 | Like | 4 | 4
5 | Lion | 5 | 5
6 | Dev | 6 | 6
7 | Dogs | 7 | 7

### languages
id | language
---|----------
1 | Java
3 | TypeScript
4 | Ruby
5 | Python
6 | Swift
7 | Kotlin
8 | JavaScript

### framewords
id | frameworkName
---|---------------
1 | Spring MVC
2 | Angular
3 | Rails
4 | Django

---

## SQL Example
SELECT l.languageName, COUNT(language_id) count<br/>
FROM users u<br/>
INNER JOIN languages l ON u.language_id = l.id<br/>
GROUP BY l.langaugeName;

### 결과 테이블
languageName | count
-------------|-------
Java | 2
Kotlin | 1
Python | 1
Ruby | 1
Swift | 1
TypeScript | 1

### HAVING
SELECT l.languageName, COUNT(language_id) count<br/>
FROM users u<br/>
INNER JOIN languages l ON u.language_id = l.id<br/>
GROUP BY l.langaugeName<br/>
HAVING count;

### 결과 테이블
languageName | count
-------------|-------
Java | 2