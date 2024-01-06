###pagination query
```
/**first dataset to only focus on business data, you can also assign row_number to get this value  */
with raw_data(demand_type,demand_type_desc)
as (
       select distinct  code_value,code_desc from cis.hyve_list_box_detail where list_box_code ='DMTP' 
),
/**second dataset to include row_id */
data_with_row_id(row_id,demand_type,demand_type_desc,row_cnt)
as (
       select row_number() over() as row_id , demand_type,demand_type_desc,count(1) over()  as row_cnt from raw_data
)
select row_id,demand_type,demand_type_desc,row_cnt
from data_with_row_id 
 where row_id > 2 and row_id <= 4 --(page size is 2, here need second page )
  -- where row_id >0 and row_id <=10  -- (page size is 10, here show first page )
```
