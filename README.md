
earl-shapely
============

Earl Grey macros to wrap
[shapely](https://github.com/AriaMinaei/shapely) so that it can
interface with
[Earl Grey](https://earl-grey.io)

The `::`, `record` and `union` macros are defined and are used as
such:

```earlgrey
require:
   earl-shapely ->
      any, nil, array-of

require-macros:
   earl-shapely ->
      ::, record, union

record Person:
   name    :: String
   age     :: Number
   friends :: array-of(Person)

union BinaryTree:
   nil
   record:
      val   :: any
      left  :: BinaryTree
      right :: BinaryTree
```

The `::` operator can also be used to check if something has a certain
type. It is also compatible with Earl Grey's assignment and pattern
matching syntax:


```earlgrey
tree :: BinaryTree = {val = 1, left = {val = 10}}

if tree :: BinaryTree:
   print "It's a tree!"
else:
   print "It isn't!"

what-is-it(match value) =
   s :: String ->
      '"{s}" is a string!'
   n :: Number ->
      '{n} is a number!'
   (t and {=> val}) :: BinaryTree ->
      '{t} is a binary tree! The top level has value {val}'

print what-is-it(tree)
print what-is-it("Blah blah blah")
```
