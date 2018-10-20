---
layout: post
title: Bash case statements are pretty powerful
---

I've been brushing up on my *Bash* skills. I worked on a problem to calculate the Scrabble score of a set of letters.
In Scrabble, each letter has different values. For example, "A" has a value of one and "Z" has a value of 10.

In Python, you might do something like this.

    letters_to_score = {
        ("A", "E", "I", "O", "U", "L", "N", "R", "S", "T") : 1,
        ("D", "G") : 2,
        ("B", "C", "M", "P") : 3,
        ("F", "H", "V", "W", "Y") : 4,
        ("K", ) : 5,
        ("J", "X") : 8,
        ("Q", "Z") : 10
    }

    def score(word):
        sum = 0
        for letter in list(word.upper()):
            for letters, value in letters_to_score.items():
                if letter in letters:
                    sum += value
        return sum
        
        
When I tried to create a Bash version of the program, I was unsure of what to do. I could create a dictionary, but
it seems that there's not really an equivalent of tuples. So, you'd have to have an entry for each individual letter. In 
Bash, I opted to use [case](https://www.tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_03.html) statements instead.

    letters=${1^^}
    sum=0
    for letter in $(grep -o . <<< $letters); do
        case $letter in
            [AEIOULNRST]) ((sum++));;
            [DG])         ((sum+=2));;
            [BCMP])       ((sum+=3));;
            [FHVWY])      ((sum+=4));;
            [K])          ((sum+=5));;
            [JX])         ((sum+=8));;
            [QZ])         ((sum+=10));;
            *)            exit 1;;
        esac
    done
    echo $sum
    
The case statements allow for fairly powerful [pattern](http://wiki.bash-hackers.org/syntax/pattern) matching. Python doesn't
really have a direct equivalent to this. [PEP 275](https://www.python.org/dev/peps/pep-0275/) proposed adding a similar
feature to Python. However, it was rejected with reasoning that there are already equivalent features in Python.
