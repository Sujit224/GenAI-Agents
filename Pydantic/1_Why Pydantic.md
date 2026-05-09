Suppose you are building a hospital management system and want to store the name and age of a patient.

So we build something like this where we create a function
```python
def insert_patient_data(name,age):
    print(name)
    print(age)
    print("Entered into the database")
```

Three different people have entered the data differently and the function successfully accepts data from them. 
```python
insert_patient_data("Ramesh",40)
insert_patient_data("Suresh",'30')
insert_patient_data("Mahesh",'thirty')
```

Thus we need a Data Validation mechanism to do this


## Custom Data Validation

We can try doing something like this
```python
def insert_patient_data(name: str,age:int):
    if type(name)==str and type(age)==int:
        print(name)
        print(age)
        print("Entered into the database")

    else:
        raise TypeError("Incorrect data")
```

But seems good but becomes too difficult when you have to manage complex data like url, emailid and links

Thus we make use of Pydantic