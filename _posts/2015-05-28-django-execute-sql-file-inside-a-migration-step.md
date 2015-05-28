---
layout: post
title: "Django: execute sql file inside a migration step"
description: "How to execute a sql file in a migration step, for initial data or data migration"
category: django
tags: [django, migration, initial-data, sql, file, migration-step, programming, web, backend]
---
{% include JB/setup %}

If we come from django < 1.7 and we have some initial data, or in a particular migration step we want to run some sql code from a file to do a data migration. here's they way:

for example if we have the following directory structure, of a django app:


<pre>
  <code>
  - app_name/
    - sql/
      - initial_data.sql
      - migrate_data.sql
    - migrations/
      - __init__.py
      - 0001_initial.py
    - models.py
    - views.py
    - urls.py
    - __init__.py
  </code>
</pre>

then run:


```
python manage.py makemigrations --empty app_name
```

where ```app_name``` is  the name of our application. Then we can rename the new generated file to to ```0002_intial_data.py``` or whatever other name is good for us.
If we are using django >= 1.8 we can do just this (I didn't try it yet):


````
python manage.py makemigrations --name inital_data --empty app_name
```

now our directory structure will be like this (with a new migration file)


<pre>
  <code>
  - app_name/
    - sql/
      - initial_data.sql
      - migrate_data.sql
    - migrations/
      - __init__.py
      - 0001_initial.py
      - 0001_initial_data.py
    - models.py
    - views.py
    - urls.py
    - __init__.py
  </code>
</pre>

if we open our new migration file we will see something like this:


<pre>
  <code class="python">
from django.db import models, migrations

class Migration(migrations.Migration):

    dependencies = [
        ('app_name', '0001_initial'),
    ]

    operations = [
    ]
  </code>
</pre>

now we have to add operations to the operations list, and we should be able to run python code. So what we need is the method ```RunPython``` from the django migrations module.


```Python
import os

from django.db import connection, migrations

def load_data_from_sql(filename):
    file_path = os.path.join(os.path.dirname(__file__), '../sql/', filename)
    sql_statement = open(file_path).read()
    with connection.cursor() as c:
        c.execute(sql_statement)

initial_data = lambda: load_data_from_sql('initial_data.sql')
migrate_data = lambda: load_data_from_sql('migrate_data.sql')


class Migration(migrations.Migration):

    dependencies = [
        ('app_name', '0001_initial'),
    ]

    operations = [
        migrations.RunPython(initial_data),
        migrations.RunPython(migrate_data),
    ]

```

  * First we create a function that given a file name, reads that file from the app's migrations directory and execute the sql code of that file in the database.
  * then we create some "on the fly" functions or "lambda" functions for every file that we need to execute.
  * finally we add those functions to the operations list using the method ```RunPython```.

May be you can set the funcion ```load_data_from_sql``` inside another file to re-use it in different places/migrations.

After that all we need to do is run the migrations:

```
python manage.py  migrate app_name
```

and we are done!
