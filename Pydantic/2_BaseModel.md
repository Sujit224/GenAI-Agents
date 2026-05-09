We make a class representing the ideal schema. This class inherits the BaseModel
```python
from pydantic import BaseModel
class Patient(BaseModel):
    name:str
    age:int
    weight:float
    married:bool
    allergies: List[str] 
    contact_details: Dict[str,str]
```

```python
def insert_patient_data(patient:Patient):
    print(patient.name)
    print(patient.age)
    print(patient.weight)
    print(patient.married)
    print(patient.allergies)
    print(patient.contact_details)
    print("Updated into the database")
```

You can directly call the method by passing an object of the class into the function
```python
insert_patient_data(Patient(name='Ramesh', age=32, weight=34.60,married=False,allergies=['pollen'],contact_details={'mobile':'9999999999'}))
```
This automatically performs type Validation

## Setting default values
You can also set default values 

```python
class Patient(BaseModel):
    name:str
    age:int
    weight:float
    married:bool = False # Setting default values
    allergies: List[str]  = None # Setting default values
    contact_details: Dict[str,str]
```

Now when you call the method without passing these values it takes the default ones
```python
insert_patient_data(Patient(name='Ramesh', age=32, weight=34.60,contact_details={'mobile':'9999999999'}))
```

OUTPUT:
```
Ramesh
32
34.6
False
None
{'mobile': '9999999999'}
Updated into the database
```

Now we have passed the value of married field and it thus overrides the default value.
```python
insert_patient_data(Patient(name='Ramesh', age=32, weight=34.60,married=True,contact_details={'mobile':'9999999999'}))
```

---
## Some special datatypes
Pydantic also offers us some special Data types

#### 1. Email
```python
from pydantic import EmailStr
```

```python
class Patient(BaseModel):
	name:str
	email:EmailStr # Automatically performs Email Validation
```

#### 2. Url
```python
from pydantic import AnyUrl
```

```python
class Patient(BaseModel):
	name:str
	email:EmailStr # Automatically performs Email Validation
	linkedin_url:AnyUrl
```

---
## Field
Used for a more Customized Validation

```python
from pydantic import BaseModel
class Patient(BaseModel):
    name:str = Field(max_length=50) # Ensures that length of name is not more than                                       50 charecters
    age:int = Field(gt = 0,lt = 120) # Agne between 0 and 120
    weight:float = Fielf(gt=0) # Weight is always positive
    married:bool
    allergies: List[str] = Field(max_length=5) # Cant enter more than 5 allergies
    contact_details: Dict[str,str]
```


## Passing Metadata using Field
We can also pass a detailed description of each field making it more readable and developer friendly

```python
from pydantic import BaseModel, Field
from typing import List,Dict,Optional,Annotated
```

```python
class Patient(BaseModel):

    name:Annotated[str,Field(max_length=50,title='Name of the patient',description='Give the name of the patient in less than 50 chars',examples=['John','bob'])]

    age:int

    weight:Annotated[float,Field(gt=0,strict=True)]

    married:Annotated[bool,Field(default=None,description='Is the patient married or not')]

    allergies: Annotated[Optional[List[str]],Field(default=None,max_length=5)]

    contact_details: Dict[str,str]
```


> [!NOTE] strict parameter
> Notice strict=True in the weight field.
> Usually even when you pass weight as a string pydantic internally converts it into a float but however you can specify it to not do so and strictly raise an error by specifying strict=True





