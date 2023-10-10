---
tags:
  - SCG
  - HTML
  - CSS
  - Python
  - Flask
---
*Entry written on September 9th, 2023*

The idea for the continuation of project is best introduced using the prototypical image:

![[the-plan.png]]
There are quite a few things to consider with this and before I take on the actual project I need to think about how to organize this in terms of whether I want to use Git Issues at all, or go purely through Obsidian Tasks. For now I will use Obsidian Tasks but will keep the idea open.

#### Clean Code
- [ ] #SCG #cleancode Need to rework a driver method for `render_template()`
- [ ] #SCG #cleancode #inprogress Unit testing.
- [ ] #SCG #cleancode Handle `previously_checked_properties` in constructor.
- [ ] #SCG #cleancode #inprogress Should only need one URL right now ... rework.
- [x] #SCG #cleancode Add configuration properties file. ✅ 2023-09-17
	Implement default values.

https://stackoverflow.com/questions/14503973/python-global-keyword-vs-pylint-w0603
#### Suggestions
It is best that the ideas for this website come from not only me, but the internet and as such I will allow users (users which don't exist yet ...) to add suggestions to the website. Users will be able to vote on other suggestions, of which the top 5 will be shown on the website and they'll have the option to check for more.

**Specific Tasks**
- [x] #SCG #suggestions Add ability to add your own suggestion. ✅ 2023-09-16
- [ ] #SCG #suggestions Add ranking of already existing suggestions.
- [ ] #SCG #suggestions Add view more button.

#### Users
I will add the ability for people to make accounts with which they can:
1) keep track of their previous characters,
2) add suggestions on what I can improve / add on the website,
3) add their own reviews of certain character builds,
4) add their own challenges / recommended mods / modlists.

#### Character Generation
- [ ] #SCG #chargen I need to add the ability to put in custom values for each entry.
- [ ] #SCG #chargen Add a `save character` button which will add the character to the `my characters` screen.
- [ ] #SCG #chargen  Add a `publish character` button on `my characters`.

### Database Integration
Recently had some breakthroughs, refer to this for where to proceed:
```python
import mysql.connector
mysql_config = {
    "host": "applefrogs.mysql.pythonanywhere-services.com",
    "user": "applefrogs",
    "password": "Sopdoo123!",
    "database": "applefrogs$skyrim-character-generator",
}
def check_database_exists(database_name):
    conn = mysql.connector.connect(**mysql_config)
    cursor = conn.cursor()
    # Check if the database exists
    cursor.execute(f"SHOW DATABASES LIKE '{database_name}'")
    result = cursor.fetchone()
    cursor.close()
    conn.close()
    if result:
        return True
    else:
        return False
```

```bash
01:28 ~ $ python
Python 3.10.5 (main, Jul 22 2022, 17:09:35) [GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import dat
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'dat'
>>> import database
>>> database.check_database_exists("default")
False
>>> database.check_database_exists("applefrogs$default")
True
```