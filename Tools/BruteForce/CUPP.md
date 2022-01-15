# CUPP
Common User Passwords Profiler
Custom password list generator. Installation: `sudo apt install cupp`
___

### Interactive Mode
```bash
cupp -i
```

Simply insert target person's known info and it will generate a password list!

## Password Policy

Assuiming that the password must meet the following conditions:
1.  8 characters or longer
2.  contains special characters
3.  contains numbers

Use the following commands:
```bash
sed -ri '/^.{,7}$/d' harry.txt            # remove shorter than 8
sed -ri '/[!-/:-@\[-`\{-~]+/!d' harry.txt # remove no special chars
sed -ri '/[0-9]+/!d' harry.txt            # remove no numbers
```

## Mangling

It is still possible to create many permutations of each word in that list. We never know how our target thinks when creating their password, and so our safest option is to add as many alterations and permutations as possible, noting that this will, of course, take much more time to brute force.

Many great tools do word mangling and case permutation quickly and easily, like [rsmangler](https://github.com/digininja/RSMangler) or [The Mentalist](https://github.com/sc0tfree/mentalist.git). These tools have many other options, which can make any small wordlist reach millions of lines long. We should keep these tools in mind because we might need them in other modules and situations.

As a starting point, we will stick to the wordlist we have generated so far and not perform any mangling on it. In case our wordlist does not hit a successful login, we will go back to these tools and perform some mangling to increase our chances of guessing the password.

Tip: The more mangled a wordlist is, the more chances you have to hit a correct password, but it will take longer to brute force. So, always try to be efficient, and properly customize your wordlist using the intelligence you gathered

# Username Generator

```bash
git clone https://github.com/21y4d/usernameGenerator.git
```

```bash
bash usernameGenerator/usernameGenerator.sh Bill Gates
```