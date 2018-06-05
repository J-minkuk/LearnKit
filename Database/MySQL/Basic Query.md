# Basic Query (SELECT)
* [SELECT (DISTINCT)](##SELECT * FROM)
* SELECT (DISTINCT)
* WHERE
* ORDER BY
* NULL, IS NOT NULL
* TOP, LIMIT
* MIN(), MAX()
* COUNT(), AVG(), SUM()
* LIKE
* [charlist] Wildcard
* IN, BETWEEN

##SELECT * FROM
SELECT DISTINCT column FROM table;
<br/><br/>
SELECT COUNT(DISTINCT column) FROM table;

## WHERE
SELECT * FROM table<br/>
WHERE NOT column='???';<br/>
> WHERE NOT column='a' AND NOT column='b';

## ORDER BY
SELECT * FROM table<br/>
ORDER BY column1, column2
> ORDER BY column1 ASC, column2 DESC;

## NULL & IS NOT NULL
SELECT column1, column2 FROM table
WHERE column2 IS NULL;
<br/><br/>
SELECT column1, column2 FROM table
WHERE column2 IS NOT NULL;

## TOP & LIMIT
SELECT TOP 3 * FROM table;
<br/><br/>
SELECT * FROM table<br/>
LIMIT 3;

## MIN() & MAX()
SELECT MIN(column) FROM table;
<br/><br/>
SELECT MAX(column) FROM table;

## COUNT() & AVG() & SUM()
SELECT COUNT(column) FROM table;
<br/><br/>
SELECT AVG(column) FROM table;
<br/><br/>
SELECT SUM(Quantity) FROM table;

## LIKE
SELECT * FROM table<br/>
WHERE column LIKE 'a%';
> a로 시작하는 것

<br/>

SELECT * FROM table<br/>
WHERE column LIKE '%a';
> a로 끝나는 것

<br/>

SELECT * FROM table<br/>
WHERE column LIKE '%or%';
> 중간 어디든 or이 포함되어 있는 것

<br/>

SELECT * FROM table<br/>
WHERE column LIKE '_a%';
> a가 두번째에 있는 것

<br/>

SELECT * FROM table<br/>
WHERE column LIKE 'a_%_%';
> a로 시작하고 최소 3글자 이상

<br/>

SELECT * FROM table<br/>
WHERE column LIKE 'a%o';
> a로 시작하고 o로 끝나는 것

<br/>

SELECT * FROM table<br/>
WHERE column NOT LIKE 'a%';
> a로 시작하지 않는 것

## [charlist] Wildcard
SELECT * FROM table<br/>
WHERE column LIKE '[bsp]%';
<br/><br/>
SELECT * FROM table<br/>
WHERE column LIKE '[a-c]%';
<br/><br/>
SELECT * FROM table<br/>
WHERE column LIKE '[!bsp]%';
<br/><br/>
SELECT * FROM table<br/>
WHERE column NOT LIKE '[bsp]%';

## IN
SELECT * FROM table<br/>
WHERE column IN ('a', 'b', 'c');
<br/><br/>
SELECT * FROM table<br/>
WHERE column NOT IN ('a', 'b', 'c');
<br/><br/>
SELECT * FROM table1<br/>
WHERE column IN (SELECT column FROM table2);

## BETWEEN
SELECT * FROM table<br/>
WHERE column BETWEEN 10 AND 20;
<br/><br/>
SELECT * FROM table<br/>
WHERE column NOT BETWEEN 10 AND 20;
<br/><br/>
SELECT * FROM table<br/>
WHERE column BETWEEN #07/04/1996# AND #07/09/1996#;
<br/><br/>
SELECT * FROM table<br/>
WHERE column BETWEEN 'text1' AND 'text2'<br/>
ORDER BY column;

## BETWEEN with IN
SELECT * FROM table<br/>
WHERE (column1 BETWEEN 10 AND 20) AND NOT column2 IN (1, 2, 3);