class HashNode:

   def __init__(self, key = "", data = None):
      self.key = key
      self.data = data


class Hashtable:

   def __init__(self, size):
      self.size = size
      self.tabell = [None] * size

   def store(self, key, data):
      value = self.hashfunction(key)

      for i in range(self.size):
         nod = self.tabell[value]

         if nod == None:
            self.tabell[value] = HashNode(key, data)
            return
         if nod.key == key:
            nod.data = data
            return

         value = (value + 1) % self.size

   def search(self, key):
      value = self.hashfunction(key)

      for i in range(self.size):
         nod = self.tabell[value]

         while nod is not None:
            nod = self.tabell[value]
            if nod.key == key:
               return nod.data
            
            value = (value + 1) % self.size

         raise KeyError(key)

   def hashfunction(self, key):
      resultat = 0
      for c in key:
          resultat = (resultat*32 + ord(c)) % self.size
      return resultat
    
