Add your answers to the Algorithms exercises here.

## Exercise I

```py
a)  a = 0
    while (a < n * n * n):  # looping from 0 -> n^3
      a = a + n * n # O(1)
```

- Answer: 1 \* n^3 => O(n^3)

```py
b)  sum = 0
    for i in range(n): # looping 0 -> n
      i += 1 # O(1)
      for j in range(i + 1, n): # looping 1 -> n
        j += 1 # O(1)
        for k in range(j + 1, n): # looping 2 -> n
          k += 1 # O(1)
          for l in range(k + 1, 10 + k): # looping 3 -> 10 + 3
            l += 1 # O(1)
            sum += 1 # O(1)
```

- Answer: (1 _ n) _ (1 _ (n - 1)) _ (1 _ (n - 2)) _ (2 \* 10) => O(n^3)

```py
c)  def bunnyEars(bunnies):
      if bunnies == 0:
        return 0

      return 2 + bunnyEars(bunnies-1)
    # has same effect as:
    for i in range(0, bunnies): # looping 0 -> bunnies (n)
        ans += 2 # O(1)
    return ans
```

- Answer: 1 \* bunnies = O(bunnies) == O(n)

## Exercise II

1. Setup: array represents floors of building, value is F below _f_, T _f_ and above, indicating wether or not the egg breaks when dropped from that floor: `floors = [F, F, F, T, T, T, T]` -> _f_ = 3 (or 4 if we call floor 1 = index 0). Define a function that accepts an array of floors and values indicating start and stop corresponding to index values of floors.

```py
floors = [F, F, F, T, T, T, T]
def drop_egg(floors, start, stop):
# initial call to our function would look like:
drop_egg(floors, 0, len(floors))
```

2. "Throw" the egg off of the middle floor (divide the array, check value at that index: `broke = floors[stop + start // 2]`)

```py
def drop_egg(floors, start, stop):
    middle = start - stop // 2
    broke = floors[middle]
```

3. If the egg broke, check one floor down. If it breaks, move down to middle of first half of floors. If not, check one floor down
   a) if it breaks move down to the middle of the first half of floors.
   b) if not, return _f_ = middle

```py
    if broke:
        check = floors[middle - 1]
        if check:
        # one down also broke
            drop_egg(floors, start, middle // 2)
        else:
            return middle
```

4. If the egg didn't break, move to middle of upper half of floors

```py
    else:
        drop_egg(floors, middle, stop)
```

-> Runtime Complexity: since we're dividing the floors in half for each recursive call we have essentially a binary search = O(log(n)). The additional check of one floor lower is O(1) and so becomes insignificant for large n.
