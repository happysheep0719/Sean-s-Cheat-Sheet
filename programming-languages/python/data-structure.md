# Basic Operation

## List
python2: zip()
python3: list(zip())

## Set
a = set([2,3,4]).union([1,2,3])

## Dict
b = {}.get(1, None)
[elegantly initialize dict](https://www.linuxzen.com/python-you-ya-de-cao-zuo-zi-dian.html)
a={}.fromkeys([1,2,3],0)

### enumerate
1 in {1:2} is faster than 1 in {1:2}.keys()

### Map key to multiple values
http://python3-cookbook.readthedocs.io/zh_CN/latest/c01/p06_map_keys_to_multiple_values_in_dict.html



## Deque
q = collections.deque()
course = q.popleft()
q.append(i)






