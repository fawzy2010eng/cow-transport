###########################
# 6.0002 Problem Set 1a: Space Cows 
# Name:
# Collaborators:
# Time:

# from ps1_partition import get_partitions
import time


# ================================
# Part A: Transporting Space Cows
# ================================

# Problem 1
def load_cows(filename):
    """
    Read the contents of the given file.  Assumes the file contents contain
    data in the form of comma-separated cow name, weight pairs, and return a
    dictionary containing cow names as keys and corresponding weights as values.

    Parameters:
    filename - the name of the data file as a string

    Returns:
    a dictionary of cow name (string), weight (int) pairs
    """
    # TODO: Your code here
    f = open(filename, "r")
    for line in filename:
        line = line.replace("\n", "")
    dict={}
    for x in f:
        dict[x.partition(",")[0]]=x.partition(",")[2]
    for key in dict:
        dict[key]=dict[key].replace("\n","")
    return dict
    pass

# print(load_cows("ps1_cow_data.txt"))

# Problem 2
def greedy_cow_transport(cows, limit=10):
    """
    Uses a greedy heuristic to determine an allocation of cows that attempts to
    minimize the number of spaceship trips needed to transport all the cows. The
    returned allocation of cows may or may not be optimal.
    The greedy heuristic should follow the following method:

    1. As long as the current trip can fit another cow, add the largest cow that will fit
        to the trip
    2. Once the trip is full, begin a new trip to transport the remaining cows

    Does not mutate the given dictionary of cows.

    Parameters:
    cows - a dictionary of name (string), weight (int) pairs
    limit - weight limit of the spaceship (an int)

    Returns:
    A list of lists, with each inner list containing the names of cows
    transported on a particular trip and the overall list containing all the
    trips
    """
    # TODO: Your code here
    ListOfLists=[[]]
    x=(sorted(cows, key=cows.__getitem__,reverse=True))
    print(x)
    def sum(list):
        sum=0
        for i in range(len(list)):
            sum=sum+int(cows[list[i]])
        return sum
    def checklist(list, z):
        for i in range(len(list)):
            if list[i] == z:
                return False
            else:
                return True
    while checklist(x,""):
        for i in range(len(x)):
            if sum(ListOfLists[len(ListOfLists) - 1]) < limit and sum(ListOfLists[len(ListOfLists) - 1]) + int(cows[x[i]]) <= limit:
                ListOfLists[len(ListOfLists) - 1].append(x[i])
                x[i]=""
                print(ListOfLists)
            if sum(ListOfLists[len(ListOfLists) - 1]) + int(cows[x[len(x)-1]]) >= limit:
                print(x[len(x)-1])
                ListOfLists.append([])
    return ListOfLists

pass


def partitions(set_):
    if not set_:
        yield []
        return
    for i in range(2 ** len(set_) // 2):
        parts = [set(), set()]
        for item in set_:
            parts[i & 1].add(item)
            i >>= 1
        for b in partitions(parts[1]):
            yield [parts[0]] + b


biglist = []


def get_partitions(set_):
    for partition in partitions(set_):
        biglist.append(([list(elt) for elt in partition]))
    return (biglist)
# Problem 3
def brute_force_cow_transport(cows, limit=10):
    """
    Finds the allocation of cows that minimizes the number of spaceship trips
    via brute force.  The brute force algorithm should follow the following method:

    1. Enumerate all possible ways that the cows can be divided into separate trips 
        Use the given get_partitions function in ps1_partition.py to help you!
    2. Select the allocation that minimizes the number of trips without making any trip
        that does not obey the weight limitation

    Does not mutate the given dictionary of cows.

    Parameters:
    cows - a dictionary of name (string), weight (int) pairs
    limit - weight limit of the spaceship (an int)

    Returns:
    A list of lists, with each inner list containing the names of cows
    transported on a particular trip and the overall list containing all the
    trips
    """
    # TODO: Your code here
    #return all the possibilities
    biglist=(get_partitions(cows))


    # return the sum of 1d list
    def sum(list):
        sum = 0
        for i in range(len(list)):
            sum = sum + int(cows[list[i]])
        return sum


    # return the sum of the 2d list
    def SUMOFBIGLIST(list):
        sum = 0
        for i in range(len(list)):
            for j in range(len(list[i])):
                sum = sum + int(cows[list[i][j]])
        return sum


    # get the total weight of all cows
    def TheTotalWeight(dict):
        sum = 0
        for X in dict:
            sum = sum + int(dict[X])
        return sum


    # replace the over wight trip with 0 weight trip
    for i in range(len(biglist)):
        for j in range(len(biglist[i])):
            if sum(biglist[i][j]) > limit:
                biglist[i][j] = []

    smalllist = []
    lengthlist = []


    # only accept the list that has no empty trip
    for i in range(len(biglist)):
        if SUMOFBIGLIST(biglist[i]) == TheTotalWeight(cows):
            smalllist.append(biglist[i])
            lengthlist.append(len(biglist[i]))

    return smalllist[lengthlist.index(min(lengthlist))],len(smalllist[lengthlist.index(min(lengthlist))])
    pass

# Problem 4
def compare_cow_transport_algorithms():
    """
    Using the data from ps1_cow_data.txt and the specified weight limit, run your
    greedy_cow_transport and brute_force_cow_transport functions here. Use the
    default weight limits of 10 for both greedy_cow_transport and
    brute_force_cow_transport.

    Print out the number of trips returned by each method, and how long each
    method takes to run in seconds.

    Returns:
    Does not return anything.
    """
    # TODO: Your code here
    before = time.time()
    (brute_force_cow_transport(load_cows("ps1_cow_data.txt")))
    after = time.time()
    print(after - before)
    pass
