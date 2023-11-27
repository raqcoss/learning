# Biology Meets Programming: Bioinformatics for Beginners

*University of California San Diego*

Coursera

<br>

**Taught by:** Pavel Pevzner, Professor.

Department of Computer Science and Engineering 
<br>

**Taught by:** Phillip Compeau, Visiting Researcher.

Department of Computer Science & Engineering

## k-mer count

```
def PatternCount(Pattern, Genome):
    count = 0
    for i in range(len(Genome)-len(Pattern)+1):
        if Genome[i:i+len(Pattern)] == Pattern:
            count += 1
    return count 
```
## Most frequent k-mer
```
# Input:  A string Text and an integer k
# Output: A list containing all most frequent k-mers in Text
def FrequentWords(Text, k):
    words = []
    freq = FrequencyMap(Text, k)
    m = max(freq.values())
    for key in freq:
        if freq[key] == m:
            words.append(key)
    return words
# Copy your FrequencyMap() function here.
def FrequencyMap(Text, k):
    freq = {}
    n = len(Text)
    for i in range(n-k+1):
        Pattern = Text[i:i+k]
        freq[Pattern] = 0
    # add another for loop here to range over each k-mer Pattern of text and increase freq[Pattern] by 1 each time
    for i in range(n-k+1):
        Pattern = Text[i:i+k]
        freq[Pattern] += 1
    return freq
# Now, we will set Text equal to the oriC of Vibrio cholerae and Pattern equal to "TGATCA"
Text = "ATCAATGATCAACGTAAGCTTCTAAGCATGATCAAGGTGCTCACACAGTTTATCCACAACCTGAGTGGATGACATCAAGATAGGTCGTTGTATCTCCTTCCTCTCGTACTCTCATGACCACGGAAAGATGATCAAGAGAGGATGATTTCTTGGCCATATCGCAATGAATACTTGTGACTTGTGCTTCCAATTGACATCTTCAGCGCCATATTGCGCTGGCCAAGGTGACGGAGCGGGATTACGAAAGCATGATCATGGCTGTTGTTCTGTTTATCTTGTTTTGACTGAGACTTGTTAGGATAGACGGTTTTTCATCACTGACTAGCCAAAGCCTTACTCTGCCTGACATCGACCGTAAATTGATAATGAATTTACATGCTTCCGCGACGATTTACCTCTTGATCATCGATCCGATTGAAGATCTTCAATTGTTAATTCTCTTGCCTCGACTCATAGCCATGATGAGCTCTTGATCATGTTTCCTTAACCCTCTATTTTTTACGGAAGAATGATCAAGCTGCTGCTCTTGATCATCGTTTC"
k = 10

# Finally, let's print the result of calling FrequentWords on Text and Pattern.
print(FrequentWords(Text, k))
```
## Reverse complement
```
# Input:  A DNA string Pattern
# Output: The reverse complement of Pattern
def ReverseComplement(Pattern):   
    return Reverse(Complement(Pattern))

# Copy your Reverse() function here.
def Reverse(Pattern):
    old = ""
    new = ""
    for char in Pattern:
        new = char + old
        old = new
    return new


# Copy your Complement() function here.
def Complement(Pattern):
    old = ""
    new = ""
    for char in Pattern:
        if char == "A":
            new_char = "T"
        elif char == "T":
            new_char = "A"
        elif char == "C":
            new_char = "G"
        elif char == "G":
            new_char = "C"
        else: new_char = "N"
        new = old + new_char
        old = new
    return new
```
## Mapping a Pattern

```
def PatternMatching(Pattern, Genome):
    # your code here
    k = len(Pattern)
    positions = PatternMap(Genome, k)[Pattern]
    return positions

def PatternMap(Text, k):
    locations = {}
    n = len(Text)
    for i in range(n-k+1):
        Pattern = Text[i:i+k]
        locations[Pattern] = []
    # add another for loop here to range over each k-mer Pattern of text and increase freq[Pattern] by 1 each time
    for i in range(n-k+1):
        Pattern = Text[i:i+k]
        locations[Pattern].append(i)
    return locations
```
## DNA Replication
<a href="https://www.youtube.com/watch?v=7Hk9jct2ozY">DNA animation Video</a>

## Nucleotide frequencies within a window

```
def SymbolArray(Genome, symbol):
    array = {}
    n = len(Genome)
    ExtendedGenome = Genome + Genome[0:n//2]
    for i in range(n):
        array[i] = PatternCount(symbol, ExtendedGenome[i:i+(n//2)])
    return array

def FasterSymbolArray(Genome, symbol):
    array = {}
    n = len(Genome)
    ExtendedGenome = Genome + Genome[0:n//2]

    # look at the first half of Genome to compute first array value
    array[0] = PatternCount(symbol, Genome[0:n//2])

    for i in range(1, n):
        # start by setting the current array value equal to the previous array value
        array[i] = array[i-1]

        # the current array value can differ from the previous array value by at most 1
        if ExtendedGenome[i-1] == symbol:
            array[i] = array[i]-1
        if ExtendedGenome[i+(n//2)-1] == symbol:
            array[i] = array[i]+1
    return array
```
## SkewArray
Skew arrays show the increments on G-C content and the inflection points where ori and terminus are located.

```
def SkewArray(Genome):
    skew = []
    skew.append(0)
    for i in range(0,len(Genome)):
        if Genome[i] == "G":
            skew.append(skew[-1] + 1)
        elif Genome[i] == "C":
            skew.append(skew[-1] - 1)
        else:
            skew.append(skew[-1])

    return skew

def MinimumSkew(Genome):
    positions = [] # output variable
    skew = SkewArray(Genome)
    for i in range (0,len(Genome)):
        if skew[i] == min(skew):
            positions.append(i)  
    return positions
```

## Hamming Distance
The total number of mismatches between strings p and q is called the **Hamming** distance between these strings

```
def HammingDistance(p, q):
    hamming = 0
    if len(p) == len(q):
        for i in range(0,len(p)):
            if p[i] != q[i]:
                hamming += 1
    else: raise "input stings are not the same lenght"
        
    return hamming

def ApproximatePatternMatching(Text, Pattern, d):
    positions = [] # initializing list of positions
    k = len(Pattern)
    Text = Text + "N"*d
    n = len(Text)
    for i in range(n-k+1):
        mismatches = HammingDistance(Text[i:i+k], Pattern)
        if mismatches <= d:
            positions.append(i)
    return positions

def ApproximatePatternCount(Pattern, Text, d):
    count = 0 # initialize count variable
    k = len(Pattern)
    Text = Text + "N"*d
    n = len(Text)
    for i in range(n-k+1):
        mismatches = HammingDistance(Text[i:i+k], Pattern)
        if mismatches <= d:
            count += 1
    return count

```
