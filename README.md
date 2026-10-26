# Syntaxkontroll

from linkedQFile import LinkedQ


class Syntaxfel(Exception):
    pass

def Group(ordkö):
    Atom(ordkö)
    if not ordkö.isEmpty():
        if ordkö.peek().isdigit():
            num(ordkö)

def Atom(ordkö):
    LETTER(ordkö)

    if not ordkö.isEmpty():
        if ordkö.peek().islower():
            letter(ordkö)

def LETTER(ordkö):
    ordet = ordkö.peek()

    if not ordet.isupper():
        raise Syntaxfel("Saknad stor bokstav vid radslutet")

    ordkö.dequeue()

def letter(ordkö):
    ordet = ordkö.dequeue()

    if not ordet.islower():
        raise Syntaxfel("Saknad liten bokstav vid radslutet")
    
def num(ordkö):
    ordet = ordkö.dequeue()


    if ordet == "0":
        raise Syntaxfel("För litet tal vid radslutet")
    if ordet == "1":
            if ordkö.isEmpty():
                raise Syntaxfel("För litet tal vid radslutet")
    
    while not ordkö.isEmpty() and ordkö.peek().isdigit():
        ordkö.dequeue()
    
def molekyl(mening):
    ordkö = LinkedQ()
    for tecken in mening:
        ordkö.enqueue(tecken)
    return ordkö

def sträng(ordkö): 
    rest = ""

    while not ordkö.isEmpty():
        rest += ordkö.dequeue()

    return rest

def main(): 

    while True:
        mening = input()
        ordkö = molekyl(mening)
        if mening == "#":
            break
        try: 
            Group(ordkö)
            print("Formeln är syntaktiskt korrekt")

        except Syntaxfel as fel:
            rest = sträng(ordkö)

            if rest:
                print(str(fel) + " " + rest)
            else: 
                print(fel)

if __name__ == "__main__":
    main()
