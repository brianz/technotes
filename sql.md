# Postgres

Good article on tuning Postgres on RDS:

https://aws.amazon.com/blogs/database/a-case-study-of-tuning-autovacuum-in-amazon-rds-for-postgresql/

## Analytics around dead tuples

```sql
SELECT relname, n_live_tup, n_dead_tup, trunc(100*n_dead_tup/(n_live_tup+1))::float "ratio%",
  to_char(last_autovacuum, 'YYYY-MM-DD HH24:MI:SS') as autovacuum_date, 
  to_char(last_autoanalyze, 'YYYY-MM-DD HH24:MI:SS') as autoanalyze_date
FROM pg_stat_all_tables 
ORDER BY last_autovacuum;
```
