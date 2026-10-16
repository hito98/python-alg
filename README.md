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
