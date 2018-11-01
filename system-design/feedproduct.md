# Design a feed product

Requirements:

1. each user could have 1-1000 friends. We need they can get stories from your friends in real time.
2. Scalability
    - milions fo query per second
    - a lot of data to store
3. can do ranking in real time

## Push/Pull model

### Push model

Pros:

- real time update
- Scalability
    - can shard by user
- easy to implement and understand

Cons:

- duplicate storage for each story