# python-alg


    def solve(row):
       if row == 8:
           return True
        
    for col in range(8):
        if col not in cols and row-col not in diag1 and row+col not in diag2:
            board[row] = col
            cols.add(col)
            diag1.add(row-col)
            diag2.add(row+col)

            if solve(row + 1):
                return True

            cols.remove(col)
            diag1.remove(row-col)
            diag2.remove(row+col)

    return False
    board = [-1] * 8
    cols, diag1, diag2 = set(), set(), set()
    solve(0)
    for r in range(8):
    print(" ".join("Q" if board[r] == c else "." for c in range(8)))


#water-jug

    from collections import deque
    def water_jug(X, Y, target):
    q = deque([(0, 0)])
    visited = set()

    while q:
        x, y = q.popleft()

        if (x, y) in visited:
            continue
        visited.add((x, y))
        print("X =", x, ", Y =", y)

        if x == target or y == target:
            print("Target reached!")
            return

        q.extend([
            (X, y), (x, Y), (0, y), (x, 0),
            (max(0, x-(Y-y)), min(Y, x+y)),
            (min(X, x+y), max(0, y-(X-x)))
        ])
water_jug(4, 3, 2)

tic tac toe

board = [" "] * 9

def show():
    for i in range(0, 9, 3):
        print(board[i], "|", board[i+1], "|", board[i+2])
        if i < 6:
            print("---------")

def win():
    lines = [(0,1,2),(3,4,5),(6,7,8),
             (0,3,6),(1,4,7),(2,5,8),
             (0,4,8),(2,4,6)]
    return any(board[a] == board[b] == board[c] != " "
               for a,b,c in lines)

player = "X"

for _ in range(9):
    show()
    pos = int(input(f"Player {player}, enter position (1-9): ")) - 1

    if pos not in range(9) or board[pos] != " ":
        print("Invalid position!")
        continue

    board[pos] = player

    if win():
        show()
        print(player, "wins!")
        break

    player = "O" if player == "X" else "X"
else:
    show()
    print("Draw!")

a *


graph = {
    'A': {'B': 2, 'C': 4},
    'B': {'D': 5, 'E': 2},
    'C': {'F': 3},
    'D': {}, 'E': {'F': 2}, 'F': {}
}

h = {'A': 6, 'B': 4, 'C': 4, 'D': 3, 'E': 2, 'F': 0}

open_list = [(h['A'], 0, 'A', ['A'])]
visited = set()

while open_list:
    open_list.sort()
    f, cost, node, path = open_list.pop(0)

    if node == 'F':
        print("Best Path:", " -> ".join(path))
        print("Total Cost:", cost)
        break

    if node in visited:
        continue
    visited.add(node)

    for next_node, weight in graph[node].items():
        if next_node not in visited:
            g = cost + weight
            open_list.append((g + h[next_node], g,
                              next_node, path + [next_node]))



