# The ideal directory structure for FastAPI projects

* Template references
* The project folder 
* How to create the project folder 


## Option 1 : Type of files and then create 


```
main.py
routers.py 
database.py
models.py 
schemas.py
config.py
services.py
```

Note : 
If the single file is becoming too big, break the file into folders.
e.g. instead of 
`routers.py`
have 
```
routers/
	auth.py 
	users.py 
	books.py
```

## Option 2 : Django type of structure. Common project files. Then app files and have various type of files in the individual apps


TODO: 
* How to manage templates, media and static files to be served. 
