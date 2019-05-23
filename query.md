# Database Query Cheat Sheet

## Duplicated data counting
```sql
select a.*,
	(case when a.item_id = @pre then @nums := @nums + 1
	  when a.item_id != @pre then @nums := 0 end) as num, 
    @pre := a.item_id
from items a, (select @pre := 0, @nums := 0 from dual) ordering
order by item_id 
```
