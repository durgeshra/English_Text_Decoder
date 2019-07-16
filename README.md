README for CS251 - Q4 (Substitution Cipher)

The code is divided into two parts : Frequency analysis and Dictionary lookup

How to use: In ghci, call `decipher "string to decode"` to print the decoded output.
In order to disable dictionary lookup, comment out L52, and uncomment L53 (in current version).

1) Frequency Analysis :

* mapping : clubs the frequency data by the sequence of letters in English from most frequent to less frequent. This is achieved by counting frequency of each letter in the supplied string (using `mainCount`) and then sorting the same in descending order of frequency (using `sortByFreq, qsort, gteq, lt`).
What we are basically doing in `mainCount` is using a blank array `[]` and adding the data of each letter of supplied string using `addInfo`.
* replace : using the array of tuples obtained from `mapping`, replaces each character in the string by the (possibly) correct letter (using `subdecipher, replace`).

2) Dictionary Lookup:

* dictData : 3 sample dictionaries are supplied (5k words, 10k words and the words as decoded from cipher.txt using an online tool). Any one can be used during testing (the last one is NOT to be used in the final version).
* closest : when `decipher` is called, it calls `closest` to return the word that is present in dictionary, that minimizes the cost function as described below. It searches through the entire dictionary, and uses the word with minimum cost in the dict (#letters has to be the same, 100000 ensures that the cost is big enough to act as upperbound). `distance_let` serves as the for loop over the dictionary that calls `letDist` and minimizes the cost. `letDist` computes the cost ketter by letter using the cost function `freqDataNum`. It is the frequency data provided at `http://pi.math.cornell.edu/~mec/2003-2004/cryptography/subs/frequencies.html`, multiplied by 100, the intuition being that letters having similar frequencies should be penalized less than the ones far away but adjacent to each other.