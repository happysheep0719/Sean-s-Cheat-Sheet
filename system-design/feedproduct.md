# Design a feed product

Requirements:

- each user could have 1-1000 friends. We need they can get stories from your friends in real time.
- Scalability
    - milions fo query per second
    - a lot of data to store
- Ranking? Ranking in real time?

## Push/Pull model

### Push model

Each user maintain a list of friends' stories that are eligible to be displayed to himself/herself.

Pros:

- real time update
- Scalability
    - can shard by user
- easy to implement and understand

Cons:

- duplicate storage for each story
- One user's request is handled by one machine


### Pull model

each user maintains a list of stories of his/her own.