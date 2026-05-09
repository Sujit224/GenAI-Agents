Suppose you want to perform validation involving more than 1 field.
Then we make use of Model Validator

Suppose you want to create a validation that ensures that patients greater than 60 years of age must have an emergency contact

```python
from pydantic import BaseModel,EmailStr,Field, field_validator, model_validator
from typing import List,Dict,Optional,Annotated  

class Patient(BaseModel):
    name:str
    email:EmailStr
    age: int
    weight: float
    married: bool
    allergies: List[str]
    contact_details: List[Dict]
  

    @model_validator(mode='after')
    def validate_emergency_contact(cls,model):
        if model.age>60 and 'emergency' not in model.contact_details:
            raise ValueError('Patients older than 60 must have an emergency contact')
        return model
```

