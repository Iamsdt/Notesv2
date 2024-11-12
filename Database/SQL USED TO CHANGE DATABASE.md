---
Created by: Shudipto Trafder
Created time: 2023-12-23T22:13
Last edited by: Shudipto Trafder
Last edited time: 2024-01-31T18:04
tags:
  - pgsql
  - sql
---
### t_jd_task → template id as foreign key

```JavaScript
ALTER TABLE t_jd_task ALTER COLUMN template_id DROP NOT NULL;

UPDATE t_jd_task SET template_id = NULL WHERE template_id = 0 OR template_id = -1;
select * from t_jd_task
```

  

## `t_jd_linkedin_matching` remove cid

```JavaScript
DELETE FROM t_jd_linkedin_matching tjlm
WHERE NOT EXISTS (
    SELECT 1
    FROM t_candidate_cvs tcc
    WHERE tjlm.cid = tcc.cid
);
```

  

t_jd_contact_analytics remove cid

```JavaScript
DELETE FROM t_jd_contact_analytics tjlm
WHERE NOT EXISTS (
    SELECT 1
    FROM t_candidate_cvs tcc
    WHERE tjlm.cid = tcc.cid
);
```

  

t_candiate_cvs:

```JavaScript
ALTER TABLE t_candidate_cvs ALTER COLUMN cloud_processing_id DROP NOT NULL;

UPDATE t_candidate_cvs SET cloud_processing_id = NULL WHERE cloud_processing_id = 0 OR cloud_processing_id = -1;
```

```JavaScript
ALTER TABLE t_candidate_cvs ALTER COLUMN ocr_labels_id DROP NOT NULL;
UPDATE t_candidate_cvs SET ocr_labels_id = NULL WHERE ocr_labels_id = 0 OR ocr_labels_id = -1
```

- now save below filed one new columns

```JavaScript
ALTER TABLE t_candidate_cvs
ADD COLUMN cloud_processing_id2 INT NULL;

UPDATE t_candidate_cvs
SET cloud_processing_id2 = cloud_processing_id;



ALTER TABLE t_candidate_cvs
ADD COLUMN ocr_labels_id2 INT NULL;

UPDATE t_candidate_cvs
SET ocr_labels_id2 = ocr_labels_id;
```

  

  

## t_cv_jd_mappings

```JavaScript
DELETE FROM t_cv_jd_mappings tjlm
WHERE NOT EXISTS (
    SELECT 1
    FROM t_candidate_cvs tcc
    WHERE tjlm.cid = tcc.cid
);
```

```JavaScript
ALTER TABLE t_cv_jd_mappings ALTER COLUMN jd_id DROP NOT NULL;

UPDATE t_cv_jd_mappings SET jd_id = NULL WHERE jd_id = 0 OR jd_id = -1;
```

  

## t_candidate_detail_acquired

```JavaScript
ALTER TABLE t_candidate_detail_acquired ALTER COLUMN jd_id DROP NOT NULL;

UPDATE t_candidate_detail_acquired SET jd_id = NULL WHERE jd_id = 0 OR jd_id = -1;
```

  

## `t_candidate_status`

```JavaScript
ALTER TABLE t_candidate_status ALTER COLUMN jd_id DROP NOT NULL;

UPDATE t_candidate_status SET jd_id = NULL WHERE jd_id = 0 OR jd_id = -1;
```

  

  

  

I apologize for the confusion. Here is the chart using Mermaid syntax:

```Mermaid
graph LR
    Task1 --> Task2
    Task1 --> Task3
```

Please note that the chart represents the relationship between Task 1, Task 2, and Task 3 as mentioned in the selected text.

T chats

```SQL
select cid, channel_id, jd_id, array_agg(id) from t_chats
group by cid, channel_id, jd_id
HAVING array_length(array_agg(id), 1) > 1;
```

```SQL
WITH RankedChats AS (
    SELECT
        cid,
        channel_id,
        jd_id,
        id,
        ROW_NUMBER() OVER (PARTITION BY cid, channel_id, jd_id ORDER BY id DESC) AS rnk
    FROM
        t_chats
)
DELETE FROM t_chat_details
WHERE chat_id IN (
    SELECT id
    FROM RankedChats
    WHERE rnk > 1
);
```

```SQL
WITH RankedChats AS (
    SELECT
        cid,
        channel_id,
        jd_id,
        id,
        ROW_NUMBER() OVER (PARTITION BY cid, channel_id, jd_id ORDER BY id DESC) AS rnk
    FROM
        t_chats
)
delete FROM t_chats
WHERE (cid, channel_id, jd_id, id) IN (
    SELECT cid, channel_id, jd_id, id
    FROM RankedChats
    WHERE rnk > 1
);
```

```SQL
UPDATE t_chats
SET company_id = tcc.company_id
FROM t_chats tc
LEFT JOIN t_candidate_cvs tcc ON tcc.cid = tc.cid;
```

```SQL
SELECT
tcs.cid,
tj.jd_id,
COALESCE(tcmwj.ranking_score, 0) as ranking_score,
tcs.candidate_status AS status_id,
tcj.value AS status_value,
tj.jd_name AS title
FROM t_candidate_status tcs
LEFT JOIN t_cv_matching_with_jd tcmwj ON tcmwj.cid = tcs.cid and tcs.jd_id = tcmwj.jd_id
LEFT JOIN t_candidate_journey tcj ON tcj.id = tcs.candidate_status
LEFT JOIN t_jds tj ON tj.jd_id = tcs.jd_id
WHERE tcs.cid = 26106



26106
25663 -> 1
25758
29496 -> latest

select * from t_cv_jd_mappings
where cid = 26106



select * from t_candidate_cvs where cid = 26106
order by cid desc
				
select cid, array_agg(jd_id), array_length(array_agg(jd_id), 1) from t_cv_matching_with_jd
group by cid
having array_length(array_agg(jd_id), 1) > 2
order by cid desc


select cid, array_agg(jd_id), array_length(array_agg(jd_id), 1) from t_candidate_status
group by cid
having array_length(array_agg(jd_id), 1) > 2
order by cid desc
```