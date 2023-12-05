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

## Motifs
https://bioinformaticsalgorithms.com/faqs/motifs.html


```
def Count(Motifs):
    count = {} # initializing the count dictionary
    k = len(Motifs[0])
    for symbol in "ACGT":
        count[symbol] = []
        for j in range(k):
             count[symbol].append(0)
    t = len(Motifs)
    for i in range(t):
        for j in range(k):
            symbol = Motifs[i][j]
            count[symbol][j] += 1
    # your code here
    return count

# Input:  A list of kmers Motifs
# Output: the profile matrix of Motifs, as a dictionary of lists.
def Profile(Motifs):
    t = len(Motifs)
    k = len(Motifs[0])
    count = Count(Motifs)
    profile = {}
    for symbol in "ACGT":
        profile[symbol] = []
        for j in range(k):
            profile[symbol].append(0)
            profile[symbol][j] = count[symbol][j] / t
    return profile

def Consensus(Motifs):
    k = len(Motifs[0])
    count = Count(Motifs)
    consensus = ""
    for j in range(k):
        m = 0
        frequentSymbol = ""
        for symbol in "ACGT":
            if count[symbol][j] > m:
                m = count[symbol][j]
                frequentSymbol = symbol
        consensus += frequentSymbol   
    return consensus

def Score(Motifs):
    consensus = Consensus(Motifs)
    k = len(Motifs[0])
    t = len(Motifs)
    score = []
    for j in range(k):
        score.append(0)
        for i in range(t):
            if Motifs[i][j] != consensus[j]:
                score[j] += 1
    return sum(score)
```
Conserved functions with ot without pseudocounts
```
def product(myList):
    result = 1
    for i in range(0,len(myList)):
        result = result * myList[i]
    return result

def Pr(Text, Profile):
    k = len(Text)
    keys = []
    for key in Profile.keys():
        keys.extend(key)
    probs = []
    for j in range(k):
        probs.append(0)
        for symbol in keys:
            if Text[j] == symbol:
                probs[j] = Profile[symbol][j]
    probability = product(probs)
    return probability
def ProfileMostProbableKmer(text, k, profile):
    n = len(text)
    most_prob_kmer = text[0:k]
    for i in range(n-k+1):
        probable_kmer = text[i:i+k]
        probability = Pr(probable_kmer, profile)
        if probability > Pr(most_prob_kmer,profile):
            most_prob_kmer = probable_kmer
    return most_prob_kmer
```

```
def GreedyMotifSearch(Dna, k, t):
    BestMotifs = []
    for i in range(0, t):
        BestMotifs.append(Dna[i][0:k])
    n = len(Dna[0])
    for i in range(n-k+1):
        Motifs = []
        Motifs.append(Dna[0][i:i+k])
        for j in range(1, t):
            P = Profile(Motifs[0:j])
            Motifs.append(ProfileMostProbableKmer(Dna[j], k, P))
        if Score(Motifs) < Score(BestMotifs):
            BestMotifs = Motifs
    return BestMotifs 
```
# Motifs with pseudocounts

Applying Laplace’s Rule of Succession
```
def CountWithPseudocounts(Motifs):
    t = len(Motifs)
    k = len(Motifs[0])
    count = {}
    for symbol in "ACGT":
        count[symbol] = []
        for j in range(k):
             count[symbol].append(1)
    t = len(Motifs)
    for i in range(t):
        for j in range(k):
            symbol = Motifs[i][j]
            count[symbol][j] += 1
    # your code here
    return count

def ProfileWithPseudocounts(Motifs):
    t = len(Motifs)
    k = len(Motifs[0])
    count = CountWithPseudocounts(Motifs)
    profile = {}
    for symbol in "ACGT":
        profile[symbol] = []
        for j in range(k):
            profile[symbol].append(0)
            profile[symbol][j] = count[symbol][j] / (t+4) # According to laplace, 4 nucleotide controls are added
    return profile

def Consensus(Motifs): #updated
    k = len(Motifs[0])
    count = CountWithPseudocounts(Motifs)
    consensus = ""
    for j in range(k):
        m = 0
        frequentSymbol = ""
        for symbol in "ACGT":
            if count[symbol][j] > m:
                m = count[symbol][j]
                frequentSymbol = symbol
        consensus += frequentSymbol   
    return consensus

def Score(Motifs): #updated
    consensus = Consensus(Motifs)
    k = len(Motifs[0])
    t = len(Motifs)
    score = []
    for j in range(k):
        score.append(0)
        for i in range(t):
            if Motifs[i][j] != consensus[j]:
                score[j] += 1
    return sum(score)

def GreedyMotifSearchWithPseudocounts(Dna, k, t):
    BestMotifs = [] # output variable
    for i in range(0, t):
        BestMotifs.append(Dna[i][0:k])
    n = len(Dna[0])
    for i in range(n-k+1):
        Motifs = []
        Motifs.append(Dna[0][i:i+k])
        for j in range(1, t):
            P = ProfileWithPseudocounts(Motifs[0:j])
            Motifs.append(ProfileMostProbableKmer(Dna[j], k, P))
        if ScoreWithPseudocounts(Motifs) < ScoreWithPseudocounts(BestMotifs):
            BestMotifs = Motifs
    return BestMotifs


```
## Randomized Motifs Search

```

import random

def Motifs(Profile, Dna):
    t = len(Dna)
    k = len(Profile["A"])
    motifs = []
    for i in range(t):
        motifs.append("")
        motifs[i] = (ProfileMostProbableKmer(Dna[i], k, Profile))
    return motifs

def RandomMotifs(Dna, k, t):
    n = len(Dna[0])
    rand_motifs = []
    for i in range(t):
        rand = random.randint(0, n-k)
        rand_motifs.append(Dna[i][rand:rand+k])
    return rand_motifs

def RandomizedMotifSearch(Dna, k, t):
    t = len(Dna)
    motifs = RandomMotifs(Dna, k, t)
    BestMotifs = motifs
    while True:
        Profile = ProfileWithPseudocounts(motifs)
        motifs = Motifs(Profile, Dna)
        if Score(motifs) < Score(BestMotifs):
            
            BestMotifs = motifs
        else:
            return BestMotifs 

#Format input in the correct form
def FormatDnaMatrix(Dna):
t = len(Dna)
for i in range(t):
        Dna[i] = Dna[i].upper()
        Dna[i].replace(" ", "")
        Dna[i].replace("U", "T")

```
## Gibbs Sampler

```
def Normalize_(Probabilities): #obsolete
    total_probability = sum(Probabilities.values())
    normalized = {key: value / total_probability for key, value in Probabilities.items()}
    return normalized

def Normalize(Probabilities):
    # check if values are list or primitive
    keys = list(Probabilities.keys())
    if isinstance(Probabilities[keys[0]], list):
        k = len(Probabilities[keys[0]])
    else:
        k = None

    if k is not None:
        
        total_probability = [0]*k
        normalized = {}
        for key in keys:
            normalized[key] = [0]*k
        for j in range(k):
            for key in keys:
                total_probability[j] += Probabilities[key][j]
            for key in keys:
                
                normalized[key][j] = Probabilities[key][j] / total_probability[j]
         
    else:
        total_probability = sum(Probabilities.values())
        normalized = {key: value / total_probability for key, value in Probabilities.items()}
        
    return normalized


def WeightedDie_(Probabilities): #obsolete
    nucleotides = []
    for key in Probabilities.keys():
        nucleotides.extend(key) 
    k = len(nucleotides[0])
    kmer = '' # output variable
    for j in range(k):
        rand = random.uniform(0,1)
        thresholds = [0]
        for value in Probabilities.values():
            thresholds.append(value + thresholds[-1])
        n = 0
        for i in Probabilities.keys():
            n += 1 
            if rand >= thresholds[n-1] and rand < thresholds[n]:
                kmer += i
    return kmer

def WeightedDie(Probabilities): # Updated
    kmer = '' # output variable
    Probabilities = Normalize(Probabilities)
    # check if values are list or primitive
    keys = list(Probabilities.keys())
    if isinstance(Probabilities[keys[0]], list):
        k = len(Probabilities[keys[0]])
    else:
        k = None

    if k is not None:
        for j in range(k):
            rand = random.uniform(0,1)
            thresholds = [0]
            for key,value in Probabilities.items():
                thresholds.append(value[j] + thresholds[-1])
            n = 0
            for i in Probabilities.keys():
                n += 1 
                if rand >= thresholds[n-1] and rand < thresholds[n]:
                    kmer += i
    else:
        rand = random.uniform(0,1)
        thresholds = [0]
        for key,value in Probabilities:
            thresholds.append(value + thresholds[-1])
        n = 0
        for i in Probabilities.keys():
            n += 1 
            if rand >= thresholds[n-1] and rand < thresholds[n]:
                kmer += i
    return kmer

def ProfileGeneratedString(Text, profile, k):
    kmer_probability = {}
    generated_string = ""
    n = len(Text)
    for i in range(n-k+1):
        current_kmer = Text[i:i+k]
        kmer_probability[current_kmer] = 0
        prob_value = Pr(current_kmer,profile)
        kmer_probability[current_kmer] += prob_value
    kmer_probability = Normalize(kmer_probability)
    rand = random.uniform(0,1)
    thresholds = [0]
    for kmer,value in kmer_probability.items():
        thresholds.append(value + thresholds[-1])
    q = len(list(kmer_probability.values()))   
    for u in range(q):
        if rand >= thresholds[u] and rand < thresholds[u+1]:
            generated_string = list(kmer_probability.keys())[u]
    return generated_string

```
