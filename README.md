import unittest

from main import molekyl, num, Group, letter, Atom, LETTER, sträng, Syntaxfel


class TestStringMethods(unittest.TestCase):

    def test_H2(self): 
        ordkö = molekyl("H2")
        Group(ordkö)
        self.assertTrue(ordkö.isEmpty())

    def test_P21(self):
        ordkö = molekyl("P21")
        Group(ordkö)
        self.assertTrue(ordkö.isEmpty())

    def test_Ag3(self): 
        ordkö = molekyl("Ag3")
        Group(ordkö) 
        self.assertTrue(ordkö.isEmpty())
    
    
    def test_cr12(self): 
        ordkö = molekyl("cr12")
        with self.assertRaises(Syntaxfel):
            Group(ordkö)

if __name__ == "__main__":
    unittest.main()
