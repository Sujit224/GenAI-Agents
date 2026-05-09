Sometimes a field may not be explicitly specified by the user but it should be computed dynamically based on values of other fields

Eg: We may have to compute the value if BMI

```python
from pydantic import BaseModel,Field, field_validator, model_validator,computed_field

from typing import List,Dict,Optional,Annotated  

class Patient(BaseModel):
    name:str
    age: int
    weight: float
    height: float
    allergies: List[str]
    contact_details: Dict[str,str]
  

    @computed_field
    @property
    def calculate_bmi(self) -> float:
        bmi = round(self.weight/(self.height**2),2)
        return bmi  
  

def insert_patient_data(patient:Patient):
    print(patient.name)
    print(patient.age)
    print(patient.weight)
    print(patient.allergies)
    print(patient.contact_details)
    print('BMI',patient.calculate_bmi) # Note that the attribute name must be same                                         as the method
    print("Updated into the database")  

insert_patient_data(Patient(name='Ramesh', age=32, weight=34.60,height=20.2,allergies=['pollen'],contact_details={'mobile':'9999999999'}))
```

OUTPUT
```
Ramesh
32
34.6
['pollen']
{'mobile': '9999999999'}
BMI 0.08
Updated into the database
```

