
### Mysql 5,x 재귀쿼리 (실패!)

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

전체 데이터의 구조에 대해서 순서를 보장해주는 order 값을 데이터 들이 가지고 있다면 원하는 쿼리를 목적에 맞게 뽑을 수 있겠지만 

해당값이 없이 참조값만으로 재귀를 돌리려는 목적에는 맞지 않음.


결국 function을 만듬.

```
CREATE FUNCTION find_lineage(_src VARCHAR(128)) RETURNS TEXT
NOT DETERMINISTIC
READS SQL DATA
BEGIN
	DECLARE _param TEXT;	-- 조건 변수
	DECLARE _tbls TEXT;		-- 리턴할 테이블 모음

	IF start_tbl IS NOT NULL AND LENGTH(start_tbl) > 0 THEN

		SET _param := start_tbl;
		SET _tbls := start_tbl;

		lineage_loop : LOOP

			SELECT GROUP_CONCAT(dest) INTO @res
			FROM table
			WHERE FIND_IN_SET(src, _param);

			IF @res IS NOT NULL AND LENGTH(@res) > 0 THEN

				SET _tbls := CONCAT(_tbls, ',', @res);
				SET _param := @res;
			ELSE

				LEAVE lineage_loop;
			END IF;

		END LOOP lineage_loop;

    RETURN _tbls;
	ELSE

		RETURN _tbls;
	END IF ;
END
```

그후 table return 이 되지 않는 관계로 불편하고 구려서 결국 사용은 하지 않는걸로...






