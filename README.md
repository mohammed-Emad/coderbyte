# coderbyte
Lambda!

# GraphChallenge
```python3
class stack():
     def __init__(self,strArr):
          strArr    = list(strArr)
          N   = int(strArr[0])
          self.start, self.end = (strArr[1], strArr[N])
          nodes, self.pointes = (strArr[N+1:], strArr[1:N+1])
          
          self.islink = lambda a,b: True if '{}-{}'.format(a,b) in nodes else False
          self._all = dict(map(lambda a:(a,list(filter(lambda b:self.islink(a,b)or self.islink(b,a), self.pointes))), self.pointes))
          self.qu   = [[self.start]] 
          self.done = [] #explored
          self.sw   = [] #switch to new neighbours
          self.res  = False #result
          self.GO = list(range(N))
          
     def check(self):
         if self.qu and self.GO:
            self.GO.append(0) #loop
            self.path = self.qu.pop(0)
            self.nn = self.path[-1]
            if self.nn not in self.done:
               self.sw = self._all[self.nn]
               self.done.append(self.nn)
               return True               
     def work(self,neg):
            self.np=list((*self.path,neg))
            self.qu.append(self.np)
            if neg == self.end:
               self.res = self.np
               self.GO = []

def GraphChallenge(strArr):
    STC = stack(strArr) 
    u = list(map(lambda _:list(map(lambda neg:STC.work(neg),STC.sw)) if STC.check() else -1,STC.GO))
    return ''.join(list(map(lambda o:o+'-' ,STC.res)))[:-1] if STC.res else -1 


if __name__ == "__main__":
  #print(GraphChallenge(input()))
  nodes= [["4", "A", "B", "C", "D", "A-B", "B-D", "B-C", "C-D" ],
       ["7", "A", "B", "C", "D", "E", "F", "G", "A-B", "A-E", "B-C", "C-D", "D-F", "E-D", "F-G"],
       ["5", "A", "B", "C", "D", "F", "A-B", "A-C", "B-C", "C-D", "D-F"],
       ["4", "X", "Y", "Z", "W", "X-Y", "Y-Z", "X-W" ],
       ["4", "W", "Y", "Z", "W", "X-Y", "Y-Z", "X-W" ],
       [ "7", "C", "B", "A", "D", "E", "G", "F", "A-B", "B-E", "E-G", "C-D", "D-B", "D-E", "E-F" ],
       ["9", "Z", "B", "C", "D", "R", "A", "Y", "Q", "E", "A-Z", "A-R", "Z-Y", "Z-C", "C-B", "Y-Q", "Q-D", "D-E", "R-E" ],
       ["5", "N1", "N2", "N3", "N4", "N5", "N1-N3", "N3-N4", "N4-N5", "N5-N2", "N2-N1"]]
  for strArr in nodes:
      print(GraphChallenge(strArr))
```

```python3 GraphChallenge.py```

**Output**
```
      A-B-D
      A-E-D-F-G
      A-C-D-F
      X-W
      -1
      C-D-E-F
      Z-A-R-E
      N1-N2-N5

```
