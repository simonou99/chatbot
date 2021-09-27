# Simple ChatBot Program
***
Welcome! This is a very short and simple chatbot program I've written.

The program uses the [ChatterBot](https://chatterbot.readthedocs.io/en/stable/index.html) package and we will cover 2 options for training.<br>
The language of choice does not have to be English when training the chatbot.<br> However, in this case we will cover this program with English-based corpus data for instruction ease.

## 1.Package Check/Install


```python
!pip install chatterbot
!pip install chatterbot_corpus
```

```python
!pip install --upgrade chatterbot
!pip install --upgrade chatterbot_corpus
``` 

## 2.Import chatterbot


```python
from chatterbot import ChatBot
```

## 3.Build a Bot Model
Following are the codes for building/training the chatbot.<br>
We will use the `ChatBot()` function for building.<br>
Please check the documentation on [ChatterBot](https://chatterbot.readthedocs.io/en/stable/index.html'), but the following codes should work fine with general chats.
If you want a different or more response logic, you can add or change the `logic_adapters` list, additonal logic can be found [here](https://chatterbot.readthedocs.io/en/stable/logic/index.html).


```python
bot = ChatBot(name='MyBot', logic_adapters=[
    {
      "import_path": "chatterbot.logic.BestMatch",
      "statement_comparison_function": "chatterbot.comparisons.LevenshteinDistance",
      "response_selection_method": "chatterbot.response_selection.get_first_response"
    }
  ]
)
```

## 4.Bot Model Training

### OPTION-1: Training with lists of phrases
Add phrases for talk and response training.
The list should be ordered as: assign list[n] be the talk, then list[n+1] be the response, starting with list[0].


```python
phrases=['Hi!','Hi there.','How are you?', 'Fine, thanks.','......']
```

#### Special phrases
Add additional phrases for specific uses, i.e. scenario-based for example mathematical phrases, emotions, industrial speech etc.


```python
special_phrases=['Report sales', 'The sales today is $blablabla', '......']
```

#### Starts training with ListTrainer


```python
from chatterbot.trainers import ListTrainer
```


```python
list_trainer=ListTrainer(bot)
for list_ in (phrases, special_phrases):
  list_trainer.train(list_)
```

### OPTION-2: Training with corpus data (Recommended)
This case we train with a corpus data from the internet, which has more varieties of phrases and response and hopefully will make the chatbot more realistic.<br>
We will use corpus data provided by ChatterBot. However, you can choose a prefered corpus library of your own.


```python
from chatterbot.trainers import ChatterBotCorpusTrainer
```


```python
cp_trainer = ChatterBotCorpusTrainer(bot)
cp_trainer.train('chatterbot.corpus.english')
```

    Training ai.yml: [####################] 100%
    Training botprofile.yml: [####################] 100%
    Training computers.yml: [####################] 100%
    Training conversations.yml: [####################] 100%
    Training emotion.yml: [####################] 100%
    Training food.yml: [####################] 100%
    Training gossip.yml: [####################] 100%
    Training greetings.yml: [####################] 100%
    Training health.yml: [####################] 100%
    Training history.yml: [####################] 100%
    Training humor.yml: [####################] 100%
    Training literature.yml: [####################] 100%
    Training money.yml: [####################] 100%
    Training movies.yml: [####################] 100%
    Training politics.yml: [####################] 100%
    Training psychology.yml: [####################] 100%
    Training science.yml: [####################] 100%
    Training sports.yml: [####################] 100%
    Training trivia.yml: [####################] 100%
    

## 5.Start Chatting!
The basic training and building procedures are now done. Try it for yourself!


```python
print(bot.get_response('hi'))
```

    How are you doing?
    

## 6.Post-Modeling Adjustment
Some additional parameters can be changed for specific requirements, please see [here](https://chatterbot.readthedocs.io/en/stable/logic/index.html).

__Thank You Very Much!__
