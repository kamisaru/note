
### Mysql 5,x 재귀쿼리

문자열로 된 트리구조의 데이터를 뽑아햐 하는 이슈.

WITH RECURSIVE는 Mysql 5.X버전에서는 지원되지 않는 문법이었음.

```
SELECT source, destination, @param as allparam
FROM
	(SELECT * FROM data_table ) AS lineage,
	(SELECT @param := '시작값') AS first_param
WHERE
	FIND_IN_SET(source, @param)
	AND length(@param := concat(@param, ',', destination))
;
```

검색으로 쿼리를 찾음.
