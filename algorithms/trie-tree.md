<extoc></extoc>

# Trie Tree

It is a search tree.

- insert, delete, or search for some kind of "**keys**"
- store **ordered** data


What is the **requirement** of this dictionary?

- n - # of words
- m - average length of the string/word
- k - # of words with the same prefix

- search (word)
- delete
- add
- find all words with given prefix, e.g., auto-completion in google search
    - in HashMap O(nm)


[!trie tree](https://www.google.com/imgres?imgurl=https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Trie_example.svg/1200px-Trie_example.svg.png&imgrefurl=https://en.wikipedia.org/wiki/Trie&h=1125&w=1200&tbnid=34jkA_88J_LiRM:&q=trie+tree&tbnh=186&tbnw=198&usg=AI4_-kRRf0_pqX5ZYkQejhVbqfUf6fzQXg&vet=1&docid=RbU6Xb8ttbB0dM&itg=1&sa=X&ved=2ahUKEwjyh4qoudfdAhXmIzQIHTUGApAQ_B0wGnoECAMQCQ)

## Implementation

```
class TrieNode {
    Map<Character, TrieNode> children;
    // another way: TrieNode[] children; // size 26 array
    Integer value;
    boolean isWord;
}
```