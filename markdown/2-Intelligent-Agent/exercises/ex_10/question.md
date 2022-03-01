

Consider a simple thermostat that turns on a furnace when the
temperature is at least 3 degrees below the setting, and turns off a
furnace when the temperature is at least 3 degrees above the setting. Is
a thermostat an instance of a simple reflex agent, a model-based reflex
agent, or a goal-based agent?


#!/usr/bin/env python3
# -*- coding: utf-8 -*-
#----------------------------------------------------------------------------
# Created By  : Kevin Amin García Gallardo
# Created Date: 28/Feb/2022 23:50:00
# version ='1.0'

from matplotlib.pyplot import imshow, show, plot, pause, clf
from random import randint


"""
0 -> clean   //   1 -> wall   //   2 -> dirt
"""
matrix = [
    [1, 1, 1, 1, 1, 1],
    [1, 0, 0, 0, 0, 1],
    [1, 0, 0, 0, 0, 1], 
    [1, 0, 0, 0, 0, 1], 
    [1, 0, 0, 0, 0, 1],
    [1, 1, 1, 1, 1, 1]
]

"""
Actions Matrix -> represents the action for each position
Actions = up (0), down (1), left (2), right (3), clean(4), end (5)
"""
actionsMatrix = [
    [9, 9, 9, 9, 9, 9],
    [9, 1, 3, 1, 5, 9],
    [9, 1, 0, 1, 0, 9], 
    [9, 1, 0, 1, 0, 9], 
    [9, 3, 0, 3, 0, 9],
    [9, 9, 9, 9, 9, 9]
]


"""
The robot always starts at matrix[1][1]
"""
currLine = 1
currCol = 1

def renderMatrix(matrix):
    imshow(matrix, 'pink')
    show(block=False)
    plot(currCol, currLine, '*r', 'LineWidth', 5)
    pause(0.1)
    clf()
    

def environment(m):
    for mI in range(1, 5):
        for aI in range(1, 5):
            number = randint(0, 3)
            m[mI][aI] = 2 if number == 1 else 0

    renderMatrix(matrix)


def findNextAction(x, y):
  return actionsMatrix[x][y]



"""
decides which action will be done
Actions = up (0), down (1), left (2), right (3), clean(4)
"""
def AgentRobot(x, y):
    if (matrix[x][y] == 2):
        return 4
    return findNextAction(x, y)


def main():
    environment(matrix)
    global currLine
    global currCol
    while True:
        action = AgentRobot(currLine, currCol)
        if (action == 0):
            print("up")
            currLine = currLine - 1
            renderMatrix(matrix)
        elif (action == 1):
            print("down")
            currLine = currLine + 1
            renderMatrix(matrix)
        elif (action == 2):
            print("left")
            currCol = currCol - 1
            renderMatrix(matrix)
        elif (action == 3):
            print("right")
            currCol = currCol + 1
            renderMatrix(matrix)
        elif (action == 4):
            print("clean")
            matrix[currLine][currCol] = 0
            renderMatrix(matrix)
        else:
            print("end")
            break
    for i in range(1, len(matrix) - 1):
        for j in range(i, len(matrix[i]) - 1):
            print(matrix[i][j])
  


if __name__ == "__main__":
    main()
