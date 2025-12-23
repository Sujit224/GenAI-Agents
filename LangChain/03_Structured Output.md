LangChain also provides the feature to customize your output. Few LLM's directly provide the option of structuring your output. While few LLM's do not. In this case we might have to use Output Parsers.

![[Drawing 2025-12-09 12.35.22.excalidraw]]

## Structured Output using LangChain

In order to use Structured<span style="color:rgb(0, 0, 0)"> Output from Lan</span>gChain we need to create certain formats for outputs.
Lets see the various ways of creating Outputs.

### 1.Using TypedDict

We use TypedDict to provide an output format to the LLM.
```python
from os import name
from typing import TypedDict
```

Suppose you want to make an LLM analyze the review of a movie and provide you an overall summary and sentiment of the movie

```python
# Here we have created a typed dictionary specifying the format in which the output is going to be
class Review(TypedDict):
  summary:str
  sentiment:str
```

Storing the entire review in a variable
```python
review_input = """I have to try and review this without comparing it to anything directly, because it's not really comparable to other action blockbusters that have disappointed me recently. But I can say that for large-scale, big-budget action movies, this is how you do it right. Hollywood isn't incapable of making movies that deliver excitement and emotion, but many pale in comparison to RRR. Again without pointing out any movies in particular (because I don't know what's directly comparable), Hollywood should take notes.
RRR has many familiar tropes and beats that you get out of historical epics/action movies, but it uses those tropes well. Things we've seen on-screen dozens of times before can still be exciting and entertaining if they're used properly, and RRR is a testament to that.
The amazing action is probably what stands out the most, but at its core, this film also has a really good story with heroes you want to see win and villains you want to see defeated. There's some extra conflict between the two main heroes for much of the movie, but ultimately it's a good vs evil story that's pretty straightforward and honest about that, and thanks to the great characters and strong performances, that ends up being enough. 

There's very little by way of slow scenes or dead air, and another reason the three hour runtime flies by is because the action is so good. I complain about lacklustre action in modern action movies a lot, and so I was really happy to find that RRR does its action so well. Amazing stunts, great setups for the big set piece scenes, a level of brutality that makes you feel the impact of the combat (but not too much that it feels gratuitous), and a way of making things over-the-top in the best way possible (so not to the point where it feels like there are no rules or consequences for the good guys). The two main heroes in this are almost superheroes, which arguably makes RRR the best superhero film in years.
Excellent stuff. A couple of lesser performances from minor characters and some occasionally clunky English dialogue from the British characters is all I could criticise it for, and they're nitpicks. This is a great action movie and an epic that more than warrants its three hour runtime."""
```

```python
# This will now give an output in your desired format
smodel = model.with_structured_output(Review)
result = smodel.invoke(review_input)
print(result)
```

You can also use your custom names and annotate what they mean.
```python
from typing import Annotated
class ReviewCustom(TypedDict):
  abc:Annotated[str,"Summary of the review"]
  xyz:Annotated[str,"Overall sentiment of the review
```

Suppose we want the overall sentiment in one word(Hit/Flop) then we can make use of Literals
```python
from typing import Literal

class ReviewCustom1(TypedDict):
  abc:Annotated[str,"Summary of the review"]
  xyz:Annotated[Literal["hit","flop"],"Overall sentiment of the review"]
```


### 2. Using Pydantic

```python
from pydantic import BaseModel
class ReviewPydantic(BaseModel):
  summary:str
  sentiment:str
```

```python
smodelpy = model.with_structured_output(ReviewPydantic)
resultpy = smodelpy.invoke(review_input)
print(resultpy)
```

We can also make use of Literals and Fields
```python
from pydantic import Field
class Review1(BaseModel):
  abc:str = Field(description="Summary of the review")
  xyz:Literal["hit","flop"] = Field(description="Overall sentiment of the review")
```

### 3. JSON
This method only works with those models that support JSON Format.

```python
json_review_schema = {
    "title":"Schema for Movie Reviews",
    "type":"object",
    "properties":{
        "summary":{
            "type":"string",
            "description":"Summary of the review"
        },
        "sentiment":{
            "type":"string",
            "enum":["hit","flop"],
            "description":"Overall sentiment of the review"
        }
    },
    "required":[
        "summary",
        "sentiment"
    ]
}
```

```python
smodel_json = model.with_structured_output(json_review_schema)
result3 = smodel_json.invoke(review_input)
print(result3)
```
