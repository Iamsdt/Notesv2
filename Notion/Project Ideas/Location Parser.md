---
Owner: Shudipto Trafder
tags:
  - Idea
Last edited time: 2024-03-04T20:18
Created time: 2024-03-04T20:10
---
## Plans:

Create a location parser, where it will take full address and return

- City
- State
- Country

Finally, parse agin into cordinates

  

Supporting Materials:

1. Spacy:

This depends on what exactly you want spaCy to recognise and how your data looks – does you database contain only the places, or also texts with those entities in context? If you want spaCy to recognise those addresses _in context_, you also need training examples of those entities in context. The examples in context should also be similar to the data you later want to use the model on.

Ultimately, you'll have to experiment with different approaches and see what works best for your data. Here are some ideas if you only have the places and addresses, but no context:

- Create **sentence templates** that are similar to the data you're looking to analyse, and randomly fill them in with entries from your database. For example, if your application needs to recognise addresses in email conversations, a template could look like: "Our office is located at [STREET] in [CITY]". If you're building a conversational application, you might want to use templates like "Find me directions to [ADDRESS]" or "Book me a flight to [CITY] via [CITY]." Based on these templates, you can then create [training data](https://spacy.io/usage/training#training-data) for the entity recognizer.
- Use the [`PhraseMatcher`](https://spacy.io/usage/linguistic-features#adding-phrase-patterns) and create match patterns using the countries, cities etc. and run it over a **large corpus of sentences**. Then you can use the sentences containing matches to create training data that's closer to real-world examples.

Given the size of your database, you'll likely end up with a very large training corpus as well. So you should also look into some [tips and strategies](https://spacy.io/usage/training#tips) for batching up your training examples and experimenting with different hyperparameters.

You'll also need to think about which labels you want the entity recognizer to learn – do you simply want to improve one of the built-in entity types like `GPE` and `LOCATION`, or do you want to add your own labels like `STREET`, `STATE` or `CITY`?

Here are some of the relevant sections in the documentation:

- [Setting entity annotations](https://spacy.io/usage/linguistic-features#setting-entities)
- [Phrase matching](https://spacy.io/usage/linguistic-features#adding-phrase-patterns)
- [Training an additional entity type](https://spacy.io/usage/training#example-new-entity-type)
- [Optimization tips and advice](https://spacy.io/usage/training#tips), like best strategies for batch sizes and hyperparameters