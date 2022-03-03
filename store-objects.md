# Storing objects

We can store a session objects by `shelve`. For instance:

```python
import shelve

## Save the session
with shelve.open('./my-objects', 'n') as my_shelve:
    for key in dir():
        if key not in ['my_shelve'] and not key.startswith('_') and type(globals()[key]) is not type(__builtins__):
            try:
                my_shelve[key] = globals()[key]
            except Exception as err:
                pass
```

To read the objects:

```python
## Read objects
with shelve.open('./my-objects') as my_shelve:
    for key in my_shelve:
        try:
            globals()[key] = my_shelve[key]
        except Exception as err:
            print(err)
            pass
```
