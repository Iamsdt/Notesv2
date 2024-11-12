---
Created by: Shudipto Trafder
Created time: 2024-01-18T17:05
Last edited by: Shudipto Trafder
Last edited time: 2024-01-19T01:09
Date: 2024-01-19
tags:
  - pgsql
  - sql
---
card table

```SQL
-- Generate a series of 10,000 numbers starting from 1
WITH series AS (
    SELECT generate_series(1, 1000000) AS i
)

-- Insert records into t_candidate_cv_card using the series
INSERT INTO t_candidate_cv_card (
    current_des,
    current_company,
    previous_des,
    previous_company,
    college_name,
    degree,
    graduation_year,
    summary,
    total_exp,
    source,
    created_at,
    updated_at,
    status,
    cid,
    skills,
    current_ctc,
    employment_type,
    expected_ctc,
    is_open_to_work,
    notice_periods,
    preferred_location,
    country_code,
    lat,
    lng
)
SELECT
    'Current Designation ' || i,
    'Current Company ' || i,
    'Previous Designation ' || i,
    'Previous Company ' || i,
    'College Name ' || i,
    'Degree ' || i,
    'Graduation Year ' || i,
    'Summary ' || i,
    i::double precision,  -- Assuming a numeric value for total_exp
    'Source ' || i,
    now(),
    now(),
    1,
    737283 + i,  -- Adjust starting value based on your requirement
    'Skills ' || i,
    'Current CTC ' || i,
    'Employment Type ' || i,
    'Expected CTC ' || i,
    1,  -- Assuming 1 for is_open_to_work
    'Notice Periods ' || i,
    'Preferred Location ' || i,
    'Country Code ' || i,
    -- Random latitude and longitude within India's boundaries
    8.0 + random() * (36.0 - 8.0),  -- Latitude range (8 to 36)
    68.0 + random() * (89.0 - 68.0)   -- Longitude range (68 to 89)
FROM series;
```

  

cv table

```SQL
-- Generate a series of 10,000 numbers starting from 1
WITH series AS (
    SELECT generate_series(1, 1000000) AS i
)

-- Insert records into t_candidate_cvs using the series
INSERT INTO t_candidate_cvs (
    cid,
    cloud_processing_id,
    ocr_labels_id,
    name,
    phone_number,
    email,
    image_url,
    raw_cv,
    cv_format,
    segments,
    created_at,
    updated_at,
    status,
    company_id,
    is_complete_profile
)
SELECT
    737283 + i,  -- Adjust starting value based on your requirement
    -- Add values for other columns as needed
    null::integer,
    null::bigint,
    'Sample Name ' || i,
    '123456789' || i,
    'sample_email' || i || '@example.com',
    'image_url' || i,
    'raw_cv' || i,
    'pdf',
    '{"segment1": "value1", "segment2": "value2"}'::jsonb,
    now(),
    now(),
    1,
    1,
    1
FROM series;
```