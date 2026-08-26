import csv


class Drama:

    def __init__(self, drama_name, rating, actors, viewship_rate, genre, director, writer, year, no_of_episodes, network):
        self.drama_name = drama_name
        self.rating = rating
        self.actors = actors
        self.viewship_rate = viewship_rate
        self.genre = genre
        self.director = director
        self.writer = writer
        self.year = year
        self.no_of_episodes = no_of_episodes
        self.network = network

    def __str__(self):

        return f"Drama name: {self.drama_name}, Rating: {self.rating}, Actor: {self.actors}, Viewship rate: {self.viewship_rate}, Genre: {self.genre}, Director:{self.director}, Writer: {self.writer}, Year: {self.year}, No.episodes: {self.no_of_episodes}, Network {self.network} "

    def __lt__(self, other):
        return self.rating < other.rating
    
    def after_2020(self):
        """Checks if the Dramas year is above 2020"""
        if self.year > 2020:
            print(f"The drama is written after 2020. The year is {self.year}")
        else:
            print(
                f"The drama is written during 2020 or before. The year is {self.year}")

    def product_rating_viewship(self):
        """Calculates produkt by multiplying rating with viewship rate"""
        return self.rating*self.viewship_rate


def read_file(filename):
    """Opens csvfile and prints each line"""
    with open(filename, "r") as file:
        csvfile = csv.reader(file, delimiter=',')
        for line in csvfile:
            print(line)


def object_file_list(filename):
    """Creates an empty list, reads in csv file and returns list with drama objects"""
    drama_object_list = []
    with open(filename, "r") as file:
        csvfile = csv.reader(file, delimiter=",")
        next(csvfile)
        for line in csvfile:
            line[1] = float(line[1])
            line[3] = float(line[3])
            line[7] = int(line[7])
            line[8] = int(line[8])
            drama = Drama(line[0], line[1], line[2], line[3],
                        line[4], line[5], line[6], line[7], line[8], line[9])
            drama_object_list.append(drama)
    return drama_object_list


def search_year(drama_object_list):
    """Crates and empty list, and matches the contents with user input and returns list with matching objects"""
    drama_list = []
    choice = int(input("What year do you wanna search?"))
    for drama in drama_object_list:
        if drama.year == choice:
            drama_list.append(drama)
    return drama_list

drama_object_1 = Drama("Legend of the Blue Sea",8.1,"Jun Ji-hyun, Lee Min-ho",17.6,"Fantasy,Romance,Comedy","Jin Hyuk, Park Seon-Ho","Park Ji-eun",2016,21,"SBS")
drama_object_2 = Drama("My roommate is a gumiho",8.7,"Jang Ki-yong, Lee Hye-ri, Kang Han-na",5.5,"Romance, Comedy, Fantasy","Nam Sung-woo, Park Joon Hwa","Baek Sun-woo, Choi Bo-rim",2021,16,"TvN")

def main():


    choice_print = input("Print list?")
    if choice_print == "Yes":
        read_file(filename="kdrama.csv")
    else:
        print("Not printing the list")
    print("-----------------------")
    print("Test of the 5 methods")
    print("-----------------------")
    print(drama_object_1)
    print("***********************")
    print(drama_object_2)
    drama_object_1.after_2020()
    calc_product_rating = drama_object_2.product_rating_viewship()
    print(calc_product_rating)
    print(f"{drama_object_1 < drama_object_2}")

    drama_objects = object_file_list(filename="kdrama.csv")
    found_drama = search_year(drama_objects)
    for drama in found_drama:
        print(drama)
main()
