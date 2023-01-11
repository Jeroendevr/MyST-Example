#python #JeroendeVries 
*Owner Jeroen de Vries*
[Website](https://requests.readthedocs.io/en/latest/)
# Logging van de library
[YouTube](https://youtu.be/ULv9x0GQFbw)
[[Error Handling#^1afd71]]
## Zonder error handling
```Python
r = requests.get(
	url='http://url.com',
	)
return r
```
## Met error handling
```Python
try:
	r = requests.get(
		url='http://url.com',
	)
	r.raise_for_status()
except exceptions.RequestException as err:
	# Handel hier de Request errors af
return r

```
## Error logging
```Python
try:
	r = requests.get(
		url='http://url.com',
	)
	r.raise_for_status()
except exceptions.RequestException as err:
	# Handel hier de Request errors af
return r
```

