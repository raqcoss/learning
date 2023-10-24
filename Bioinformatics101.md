# Biology Meets Programming: Bioinformatics for Beginners
University of California San Diego
Coursera
**Taught by:** Pavel Pevzner, Professor
Department of Computer Science and Engineering 
**Taught by:** Phillip Compeau, Visiting Researcher
Department of Computer Science & Engineering
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

