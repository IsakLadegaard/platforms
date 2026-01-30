GAB data:

final_gab_5ormoreposts.csv this is the list of users with at least 5 posts. It includes min and max dates, days involved, and the variable benefactor. The latter is TRUE, FALSE, or NA. A benefactor is someone who donated, invested, or was listed as PRO in the dataset shared by David Thiel.

SS/V2Ray data:

Activity measures up until end of 2024. Forks, and commits. 

The forks-query data includes 2025 and was collected using https://console.cloud.google.com/bigquery

SELECT 
  repo.name AS source_repo,
  actor.login AS user,   -- "actor" is the person creating the fork
  created_at
FROM `githubarchive.month.*`
WHERE _TABLE_SUFFIX BETWEEN '201201' AND '202602'
  AND type = 'ForkEvent'
  AND (
    LOWER(repo.name) LIKE '%shadowsocks%' 
    OR LOWER(repo.name) LIKE '%v2ray%' 
    OR LOWER(repo.name) LIKE '%v2fly%'
  )
ORDER BY created_at ASC
