import sys
import csv
import copy
import pprint

def printGreekRoman(latin, mate):
    greekRoman = []
    
    if( mate == []):
        return []
    
    for i in range(len(latin)):
        temp = []
        for j in range(len(latin)):
            temp.append((latin[i][j],mate[i][j]))
        greekRoman.append(temp)    
            
    return greekRoman

def findSquare(sets, orthog, s):
    if s == len(latin):
        return orthog
    for i in range(len(sets[s])):
        orthog.append(sets[s][i])
        if isOkey(orthog) == False:
            orthog.pop()
            continue
        result = findSquare(sets, copy.deepcopy(orthog), s+1)
        if len(result) == len(latin):
            return result
        orthog.pop()

    return []
        
            
                   
def isOkey(temp):
    if len(temp) == 1:
        return True
    for c in range(len(temp[0])):
        exist = [temp[0][c]]
        for r in range(1, len(temp)):
            if temp[r][c] in exist:
                return False
            else:
                exist.append(temp[r][c])
    return True

                
def findMate(latin, orthogonal):
    mate = copy.deepcopy(latin)
    for i in range(len(orthogonal)):
        temp = orthogonal[i]
        k = temp[0]
        for c in range(len(orthogonal)):
            for r in range(len(orthogonal)):
                if latin[r][c] == temp[c]:
                    mate[r][c] = k
                    break
    return mate
    
def findTransversals(latin, elems, rows, c):
    if c == len(latin):
        return elems
    for r in range(len(latin)):
        if latin[r][c] not in elems and r not in rows:
            elems.append(latin[r][c])
            rows.append(r)
            temp = findTransversals(latin, elems[:], rows[:], c+1)
            if len(temp) == len(latin):
                if temp not in combs:
                    combs.append(temp[:])
            elems.pop()
            rows.pop()
    return elems
                   

def makeSets(combs):
    sets = []
    for i in range(len(latin)):
        sets.append([])
    for i in range(len(combs)):
        sets[combs[i][0]].append(combs[i])
    for i in range(len(sets)):
        if sets[i] == []:
            return []
    return sets



input_filename = sys.argv[1]
latin = []
with open(input_filename, 'r') as f:
    reader = csv.reader(f, delimiter=',', quoting=csv.QUOTE_NONE)
    for row in reader:
        li = [int(x) for x in row]
        if len(li) != 0:
            latin.append(li[:])

# print(latin)
combs = []
findTransversals(latin, [], [], 0)
# print(len(combs))
sets = makeSets(combs)
# print(sets)
if sets == []:
    print(sets)
    sys.exit()

orthogonal = findSquare(sets, [], 0)
# print(orthogonal)

if(orthogonal != []):
    mate = findMate(copy.deepcopy(latin), orthogonal)
    # print(mate)
    pprint.pprint(printGreekRoman(latin, mate))

