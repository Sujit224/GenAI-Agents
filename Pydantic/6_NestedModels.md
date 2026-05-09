Placing a model inside another model for better readability

```python
from pydantic import BaseModel

class Address(BaseModel):
    city:str
    state:str
    pin:str  

class Patient(BaseModel):
    name:str
    gender:str
    age:int
    address:Address
```

```python
address_dict = {'city':'Bengaluru','state':'Karnataka','pin':'560103'}

patient1 = Patient(name='John',gender='male',age=44,address=address_dict)
print(patient1.address.state)
```

OUTPUT
```
Karnataka
```
