
### Mysql 5,x 재귀쿼리

문자열로 된 트리구조의 데이터를 뽑아햐 하는 이슈.

WITH RECURSIVE는 Mysql 5.X버전에서는 지원되지 않는 문법이었음.

```
SELECT source, destination, @param as allparam
FROM
	(SELECT * FROM data_table ) AS data_table,
	(SELECT @param := '시작값') AS first_param
WHERE
	FIND_IN_SET(source, @param)
	AND length(@param := concat(@param, ',', destination))
;
```

검색으로 쿼리를 찾음.

음.. 잘 나오는 군..

역방향으로 쿼리를 돌림.

```
SELECT source, destination, @param as allparam
FROM
	(SELECT * FROM data_table ) AS data_table,
	(SELECT @param := '시작값') AS first_param
WHERE
	FIND_IN_SET(destination, @param)
	AND length(@param := concat(@param, ',', source))
;
```

앗. 데이터가 정상적으로 나오지 않음.

왜 데이터가 나오지 않는지에 대해 분석.. 

검색 중 위의 쿼리는 데이터의 값을 보장할 수 없다는 글도 봄. 아까운 시간을 많이 버림.

```
SELECT source, destination, @param as allparam
FROM
  (SELECT * FROM data_table ORDER BY source ASC, destination ASC) AS data_table,
  -- (SELECT * FROM data_table ORDER BY source ASC, destination DESC) AS data_table,
  -- (SELECT * FROM data_table ORDER BY source DESC, destination ASC) AS data_table,
  -- (SELECT * FROM data_table ORDER BY source DESC, destination DESC) AS data_table,
  (SELECT @param := '시작값') AS first_param
WHERE
	FIND_IN_SET(destination, @param)
	AND length(@param := concat(@param, ',', source))
;
```

왜 값이 제대로 나오지 않는지는 정렬값을 바꿔보면 눈치 챌 수 있음.

일단 Full JOIN을 걸고 조합된 결과셋에서 값에 맞는 데이터셋을 찾다보니 정렬에 따라 값이 바뀜.

전체 데이터에 대해서 





