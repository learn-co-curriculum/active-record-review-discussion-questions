# ActiveRecord Review Discussion

## ActiveRecord

Before we learned about ActiveRecord, we were able to call on a class method such as `Pet.all` which would return a collection of all the pet instances. That method would look like this:

```ruby
  class Pet
    # ...

    def self.all
      ALL
    end

    # ...
  end
```

When our class inherits from `ActiveRecord::Base`, we get the `all` method (and many more methods) for free.

Discuss with your table the steps involved in ActiveRecord's implementation of the class method `all`.  Read the SQL logger output. How is SQL used? What's the return value of this method?

## Domain Modeling

With your table discuss how you would model out the relationships between three models: `Voter`, `Vote`, and `Candidate`.  On which table do the foreign keys belong?

## AR Query Methods

Take a look at the following `Voter` class:

```ruby
class Voter < ActiveRecord::Base
  has_many :votes
  has_many :candidates, through: :votes
end
```

By providing the macros `has_many :votes` and `has_many :candidates, through: :votes`, ActiveRecord gives the `Voter` class the instance methods `Voter#votes` and `Voter#candidates`. These methods will fire some SQL, grab some rows from the database, and return the appropriate Ruby instances.

Your task is to run the following commands and read the SQL logger outputs. If you feel very comfortable or passionate about SQL, you can even try and guess what SQL commands will run under the hood when these methods are triggered:

```ruby
voter = Voter.create

candidate = Candidate.create

voter.votes

voter.candidates

vote = Vote.create(voter_id: voter.id, candidate_id: candidate.id)

vote = voter.votes.create(candidate: candidate) # alternative approach to above

vote.voter


```
