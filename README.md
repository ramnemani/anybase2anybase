# anybase2anybase
Given below are three Python functions to convert a given number from one number base to another base

def base10_to_anybase(nbr, to_base):
    assert type(nbr) is int, "The first argument should be Integer"
    assert type(to_base) is int, "The second argument should be Integer"

    ## We lied. This function can handle only base 2 - base 62
    if to_base < 2 or to_base > 62 :
        raise Exception('This function can handle only base 2 - base 62')  
        
    ## handle negative numbers in future
    if nbr < 0 :
        raise Exception('This function does not yet handle negative values') 
    elif nbr == 0:
        return str(nbr)

    cs = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    
    qtnt = nbr
    list_Of_remainders = []
    
    ## A list of remainders is cerated by dividing qtnt by to_base repeatedly until the qtnt becomes 0.
    ## The variable 'qtnt' is assigned the nbr passed into the function
    
    while qtnt > 0:
        qtnt, rmndr = qtnt//to_base, qtnt%to_base
        list_Of_remainders.append(str(cs[rmndr]))
        
    ## The list_Of_remainders list is reversed and converted into a string that is the to_base representation of
    ## the number passed into the function.
    
    list_Of_remainders.reverse()
    s = ''.join(i for i in list_Of_remainders)
    
    return s

def anybase_tobase10(nbrstr, from_base):
    assert type(nbrstr) is str, "The first argument should be string"
    assert type(from_base) is int, "The second argument should be Integer"

    ## We lied. This function can handle only base 2 - base 62
    if from_base < 2 or from_base > 62 :
        raise Exception('This function can handle only base 2 - base 62')
    
    ## handle negative numbers in future
    if nbrstr.isalnum() == False:
        raise Exception('The number string must be alphanumeric only')
    
    cs = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    
    # nbrstr is converted into a list of individual digits or characters
    
    list_Of_digits = list(nbrstr) 

    # Below line converts each digit in the 'list_Of_digits' list to it's Base 10 equivalent.
    # enumerate function is used to get each digit and it's position in the list
    # reversed list is used, so that the right most digit in the list gets associated
    # with position 0. 
    
    lc = [ cs.index(digit) * from_base ** position \
          for position,digit in enumerate(reversed(list_Of_digits))] 
    
    ## The variable 'lc' is a list of integers that contain Base 10 equivalent 
    ## of each digit from the 'list_Of_digits' list. We get the Base 10 number of nbrstr by
    ## adding up all the integers in 'lc' list
    
    return sum(lc)

def anybase_to_anybase(nbrstr, from_base, to_base):
    assert type(nbrstr) is str, "The first argument should be string"
    assert type(from_base) is int, "The second argument should be Integer"
    assert type(to_base) is int, "The third argument should be Integer"

    ## Step 1 : Convert the nbrstr from from_base to a Base 10 number
    base10_nbr = anybase_tobase10(nbrstr, from_base)
    
    ## Step 2 : Convert Base 10 number to  to_base
    s = base10_to_anybase(base10_nbr, to_base)

    return s
 
## Example usage
## Below example converts from base10 to base62
##
s = base10_to_anybase(99877, 62)  
print(s)

##
## Below example converts from base6 to base10
##
n = anybase_tobase10('99', 6)
print(n)

##
## Below example converts from base16 to base8
##
s = anybase_to_anybase('1e', 16, 8)
print(s)

##
## Below example converts from base8 to base16
##
s = anybase_to_anybase('36', 8, 16)
print(s)

