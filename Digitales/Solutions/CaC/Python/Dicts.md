# Python Solutions

### Serialize AWS Tag into Python Dictionaries

AWS usually returns its Tags this way and other solutions do too.

```python
tags = {
    'TagList': [
        {
            'Key': 'Name',
            'Value': 'John'
        },{
            'Key': 'Surname',
            'Value': 'Contre'
        },
    ]
}
```

Here's a simple python **oneliner** that turns that into a nice Python dictionary.

```python
tags_nice = {d["Key"]: d["Value"] for d in tags.get('TagList')}
print(tags_nice)
--
>>> {'Name': 'John', 'Surname': 'Contre'}

```
