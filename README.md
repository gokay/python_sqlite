# Python 3.7.x and SqLite 3 examples

## For [SqLite3](https://docs.python.org/3/library/sqlite3.html) documentation

## [Padao](https://pandao.github.io/editor.md/en.html) markdown editor used for this file


![](https://github.com/gokay/python_sqlite/blob/master/python.png)(https://github.com/gokay/python_sqlite/blob/master/sqlite.png)


#### Python code

```python
import sqlite3

try:
    conn = sqlite3.connect('db.sqlite')
    cursor = conn.cursor()
    print("Opened database successfully")
except sqlite3.Error as err:
    print('Error : ' + err.args[0])
finally:
    conn.close()
    print("Closed database successfully")

# Create table
conn = sqlite3.connect('db.sqlite')
cursor = conn.cursor()

cursor.execute('''  CREATE TABLE SCHOOL
                    (ID INT PRIMARY KEY     NOT NULL,
                    NAME           TEXT    NOT NULL,
                    AGE            INT     NOT NULL,
                    ADDRESS        CHAR(50),
                    MARKS          INT);''')
cursor.close()

# Inserting records
conn = sqlite3.connect('db.sqlite')
cursor = conn.cursor()

cursor.execute("INSERT INTO SCHOOL (ID,NAME,AGE,ADDRESS,MARKS) vALUES (1, 'Rohan', 14, 'Delhi', 200)")
cursor.execute("INSERT INTO SCHOOL (ID,NAME,AGE,ADDRESS,MARKS) VALUES (2, 'Allen', 14, 'Bangalore', 150 )")
cursor.execute("INSERT INTO SCHOOL (ID,NAME,AGE,ADDRESS,MARKS) VALUES (3, 'Martha', 15, 'Hyderabad', 200 )")
cursor.execute("INSERT INTO SCHOOL (ID,NAME,AGE,ADDRESS,MARKS) VALUES (4, 'Palak', 15, 'Kolkata', 650)")
conn.commit()
conn.close()

# Selecting records
conn = sqlite3.connect('db.sqlite')
cursor = conn.cursor()

for row in cursor.execute("SELECT id, name, marks from SCHOOL"):    
    print("ID = ", row[0])
    print("NAME = ", row[1])
    print("MARKS = ", row[2], "\n")
conn.commit()
conn.close()

# Update records
conn = sqlite3.connect('db.sqlite')
cursor = conn.cursor()

conn.execute("UPDATE SCHOOL set MARKS = 250 where ID = 3")
conn.commit()
for row in cursor.execute("SELECT id, name, address, marks from SCHOOL"):    
    print("ID = ", row[0])
    print("NAME = ", row[1])
    print("MARKS = ", row[2], "\n")
conn.commit()
conn.close()

# Delete records
conn = sqlite3.connect('db.sqlite')
cursor = conn.cursor()

conn.execute("DELETE from  SCHOOL where ID = 2")
conn.commit()
for row in cursor.execute("SELECT id, name, address, marks from SCHOOL"):
    print("ID = ", row[0])
    print("NAME = ", row[1])
    print("ADDRESS = ", row[2])   
    print("MARKS = ", row[3], "\n")
conn.commit()
conn.close()
```