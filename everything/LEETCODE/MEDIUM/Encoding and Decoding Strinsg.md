```
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """

        # use of a delimiter <- a character inserted to seperate strings (character must not be a possible character)
        return "π".join(strs)

        

    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        return s.split('π')
        


# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))
```

does not work all the time because not all computers are able to use Unicode (both roughly the same speed)

```
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """

        encoded = ''
        for s in strs:
            encoded += str(len(s)) + "/:" + s # <- create a new string where the digit is the length of string and delmiter is signal of splitting, every delimiter signals to the next delimiter
        return encoded
        

    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """

        decoded = []
        i = 0
        while i < len(s):
            delim = s.find('/:', i)
            length = int(s[i:delim])
            string = s[delim+2 : delim+2+length]
            decoded.append(string)
            i = delim + 2 + length
        return decoded
        
        


# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))
```