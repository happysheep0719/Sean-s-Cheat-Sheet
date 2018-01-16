# Python

## Basics

```
def main():
    x = [1, 2, 3, 4]
    for i in range(len(x)):
        print("The %dth number of List x is %d".format(i, x[i]))

if __name__ == "__main__":
    main()
```

## delivering function parameters
## for loop
range is removed in python3
xrange is replaced with range
## devide
1/2=0.5 in python3
1//2 = 0 in python3
## list operation
python2: zip()
python3: list(zip())
## Data Structure
a = set([2,3,4]).union([1,2,3])
b = {}.get(1, None)
q = collections.deque()
course = q.popleft()
q.append(i)
[elegantly initialize dict](https://www.linuxzen.com/python-you-ya-de-cao-zuo-zi-dian.html)
a={}.fromkeys([1,2,3],0)
print(a)

1 in {1:2} is faster than 1 in {1:2}.keys()
## File Input and Output

```
file = open("input.txt")
x = file.readline()
print(x)
```

## String Format
Python2 vs Python3
https://pyformat.info/

## Map key to multiple values
http://python3-cookbook.readthedocs.io/zh_CN/latest/c01/p06_map_keys_to_multiple_values_in_dict.html


