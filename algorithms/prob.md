<extoc></extoc>

# Probility, Sampling, Randomization, etc

# Shuffling algorithm

**Random Shuffle** - All the permutations have the same probability.

```java
Random random = new Random();
```

Data Structure:

Shuffled || To be shuffled


# Sampling

**How do we sample one element from a stream of unknown/unlimited size?**

- use one varible to record the sample and another varible to count the stream
- Replace the sample with the new element with prob. of `1 / counter`

```java
Element sample = null;
int counter = 0

Element newElement = stream.getNext();
while (newElement != null){
    counter++;
    if (random(counter) == 0){
        sample = newElement;
    }
    newElement = stream.getNext();
}
```

**Follow-up. How do we sample K element from a stream of unknown/unlimited size?**

- Reservoir sampling
- Use a counter and Size-k element to store the samples
- Replace one of the samples with the new element with prob. of `k / counter`
- Replace the i-th sample with the new element with prob. of `1 / k`

**Follow-up. return a random index of the largest numbers**

- Use a counter to record the number of largest and an element to record the largest
- If the largest change, reset the counter to 1
- If the new element is equal to the largest
    - replace the random index with the new index with prob. of `1 / counter`

## Design a random generator with other random generator

**P1. Design Random5() with Random7()**

index|0|1|2|3|4|5|6
---|---|---|---|---|---|---|---
-|0|1|2|3|4|5|6

- If the generated number is in [0, 4], output it.

**P2. Design Random7() with Random5()**

index|0|1|2|3|4
---|---|---|---|---|---
0|0|1|2|3|4
1|5|6|7|8|9
2|10|11|12|13|14
3|15|16|17|18|19
4|20|21|22|23|24

- Pick a number from [0, 20]

**P3. Design Random1000000() with Random2()**

- Random125() = Random5() * 25 + Random5() * 5 + Random5()
- Random2() -> Random2^k()
    - 2^k >= 1000000