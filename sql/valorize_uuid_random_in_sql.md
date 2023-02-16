# Valorize uuid_generate functions in .sql files

I had a bunch of .sql files containing inserts with the uid generated using `uuid_generate_v4()`.
To make them idempotent, I wanted to valorize them all before runtime, so on consequent runs the uid would collide.
To do so I wrote a simple python script.
```python
import uuid  
import re

source = open("source.sql", "r")
new_string = re.sub("uuid_generate_v4\(\)", lambda m: "'" + str(uuid.uuid4()) + "'", source.read())

out = open("out.sql", "w")
out.write(new_string)

source.close()
out.close()
```