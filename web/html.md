

```flow
st=>start: Start
e=>end: End
op1=>operation: My Operation
sub1=>subroutine: My Subroutine
cond=>condition: Yes or No?
io=>inputoutput: catch something

st->io1->cond
cond(yes)0>io->e
cond(no)->sub1(right)->op1
```

