## Performing a custom Validation

Suppose you want to validate that if the person is from hdfc or icici bank from their email you can include the following methos in the class

```python
class Patient(BaseModel):
    name:str
    email:EmailStr
    age: int
    weight: float
    married: bool
    allergies: List[str]
    contact_details: List[Dict] 
     

    @field_validator('email')
    @classmethod
    def email_validator(cls,value):
        valid_domains = ['hdfc.com','icici.com']
        domain_name = value.split('@')[-1]
        
        if domain_name not in valid_domains:
            raise ValueError('Not a valid domain')

        return value
```
---
### Performing a Transformation

Suppose you want all the names to be entered in capital by default.
```python
class Patient(BaseModel):
    name:str
    email:EmailStr
    age: int
    weight: float
    married: bool
    allergies: List[str]
    contact_details: List[Dict] 
     

    @field_validator('name')
    @classmethod
    def email_validator(cls,value):
       return value.upper()
```



> [!NOTE] mode parameter
> 	If mode=before then the field_validator method recieves value before type coercion
> 	 If mode=after then it recieves value after type coercion

