firstly create an app and write some code on the views.py which maybe function based or class based
then on the same app create a urls.py file including the url patterns using the path function 
then our app level is done

and then for the project level 
navigate to the urls.py and include the app urls and also give the mount dir
and finally add the app to the installed apps part on the settings.py

Request and responses 

Models for database
simply create a models.py file on the app  and create models by importing from django.db and makemigrations and then migrate
we can check models on the db.sqlite3 by default (serverless)

and also create a forms.py fiile to get input from the user to the file
importing is done form the form class and import from the model from the models file and the model is registered via the admin.site.register() functionality 

then we populate the db using the form via admin/ but first create a superuser for the database
and then we manage the db using admin/ creds

and we can also do it via another db that is mysql
just create a db using mysql on the device and then create a new db in my case django_db; and then just create a new user for that 
- Created a new MySQL user `namura@127.0.0.1` with password login (`mysql_native_password`).
- Created a database (`django_db`) and granted this user full access.
- Updated Django to connect to MySQL using `HOST='127.0.0.1'` and the correct credentials.
which are namura:Namur@!23
and then I had to create a superuser again for the new db as my admin page was fucked up so created a new admin/ creds and logged in and as of roght now I'm using mysql as the db yay~

Now for the templates
In Django templates, {% ... %} is used for template tags, and {{ ... }} is used for template variables.


Mini project : lemon juice 
restaurant folder is app level and  lillemon is project level folder

so venv activate first then 
quick fix interpreter issue
create a menu model on models.py app level and then import and register model on admin.py app level
migrate the db and url map on app level and project level

create super user for the project and then run the server and login as admin and add some values on the model and 
 on the models we can dask the menu class to call self.name
 like:
```
 def __str__(self):
	 return self.name
```

create a menu view app level and render the data as a dict from the Menu.objects.all() method

lol project ta banaye 2 hrs jati lagayera template pailai thiyo 
tara basics nai ramro xaina raixa so feri python sikna aateko 
using http://scrimba.com/ lol hawa raixa lastai basic

