        ^     Matches the beginning of a line  
        $     Matches the end of the line  
        .     Matches any character    
        \s    Matches whitespace  
        \S    Matches any non-whitespace character  
        \*    Repeats a character zero or more times  
        *?    Repeats a character zero or more times(non-greedy)  
        \+    Repeats a character one or more times  
        +?    Repeats a character one or more times(non-greedy)  
        [aeiou] Matches a single character in the listed set  
        [^XYZ]  Matches a single character not in the listed set  
        [a-z0-9] The set of characters can include a range  
        (       Indicates where string extraction is to start  
        )       Indicates where string extraction is to end  


#### find } catch { \n  log.error...  \n  throw ...
    ^(.*} catch.*)(?:(?:\r\n|[\r\n])[^\r\n]+)(log.error.*)(?:(?:\r\n|[\r\n])[^\r\n]+)(throw)
    
    
#### Matching across different lines
    [\s\S]* or [\w\W]* or [\d\D]*
    If we have regular expression like below: 
        HostPeer.doSelect[\s\S]*(host.save\()+?
    It will try to find 
![regular expression (cross multi lines)](https://github.com/adrrrrrrrian/notes/blob/master/bigdata/regular%20expression%20(cross%20multi%20lines).PNG)
