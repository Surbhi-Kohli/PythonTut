message='hello World'
you can create strings with single or double quotes
#separate var name with '_' like my_message
print(message)


multiline string
message_big= """ Boby's world was a 
good cartoom in 1998"""

len - to find the no. of characters in a string
print(len(message)) #11
print(message[0]) #h
print(message[11])#IndexError: index out of range

#Slicing
print(message[0:5]) #hello (excludes the last)
print(message[:5]) #hello
print(message[6:]) #World

print(message.lower()) # hello world
print(message.upper()) #HELLO WORLD
print(messagge.count('hello)) # 1
print(message.count('l'))# 3
print(message.find('World')) 6(index of start of World)
print(message.find('Universe')) # -1

new_message = message.replace('World','Universe')
print(new_message) # hello Universe

greeting = 'Hello'
name = 'Michael'
message=greeting+', '+name
print(message) #Hello, Michael

message = '{}, {} . Welcome!'.format(greeting,name)
print(message)

With python 3.6+ we can use fstrings
Fstrings:

message = f'{greeting},{name.upper}.Welcome !'
print(message)
print(dir(name)) # dir gives attributes and methods available on this
print(help(str))
print(help(str.lower))
