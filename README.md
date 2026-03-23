# Introduction
Description of the project

# Pseudocode
Put pseudocode in this box:

```
orig = original string
query = query string

n = len(orig)
orig_indices = `[0....n]`

suffixes_unsorted = `[orig[i:] for i in orig_indices]` (if we wanted full rotations then it's `orig[i:]+orig[:i]`)

suffix_array = orig_indices sorted by suffixes_unsorted as the index (will be in lexicographic)

bwt = built letter-wise: for i in suffix_array, the next letter is `orig[i-1]`

----

make count dictionary C where `C[c]` gives the first row in S1 where c (a character) appears (all suffixes (rows) whose value in S1 < c will come before `C[c]`)

One way to build C would be:

1. create counts = {c:n} where c is the character and n is the number of times it appears in bwt (or S1 or orig, it's equivalent)

2. create C from smallest to largest lexicographic character:
    1. total = 0
    2. for c in sorted(counts): `C[c] = total, total += counts[c]`

----

define what I will call a function Occ(c,i).

- when i=0, Occ(c,i) = 0

- when i>0, Occ(c,i) = how many times c has appeared in `bwt[0...i]`, <u>i included</u>.

----

Search pseudocode:

prior operations:

- suffix_array was computed first
- the bwt was created using the suffix_array
- Occ and C were created using bwt
- bwt never used again

assuming: 
- Occ(c,i) returns how many times c has occured in bwt[0...i] for i > 0
	(it can be a dict computed once instead of a function if we explicitly assign for i =< 0, i just think of it as a function)
- C[c] returns how many times c appears in the string

steps:
1. start with every suffix in our window

lower = 0 
upper = n - 1

2. repeatedly update for longer and longer suffixes

for c in reversed(query):
	earliest_c = C[c]
	
	if lower =< 0 : 
			lower = earliest_c
		else : 
			lower = earliest_c + Occ(c,lower-1)
	
	upper = earliest_c + Occ(c,upper) - 1
	
	if lower > upper: no match found

3. return positions in orig
   
   return suffix_array[lower:upper+1]
```

# Successes
Description of the team's learning points

# Struggles
Description of the stumbling blocks the team experienced

# Personal Reflections
## Group Leader
Group leader's reflection on the project

## Other member
Other members' reflections on the project

# Generative AI Appendix
As per the syllabus
