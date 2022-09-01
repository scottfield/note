###splunk compoents:
- Search Head
- Indexer
- Forwarder
- Deployment Server
- Cluster Master
- License Master
###Default Metadata Settings
- source
- sourcetype
- host 
- index default to main
###common functions:
- table
- rename
- dedup
- fields(only include field can improve performance)
- sort
- top
- rare
- stats
	+ count  use as clause to rename the count field
	+ dc(distinct_count)
	+ sum
	+ avg
	+ list
	+ values