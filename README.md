# anybase2anybase
The python file anybase2anybase.py has three Python functions to convert a given number from one number base to another base.

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

