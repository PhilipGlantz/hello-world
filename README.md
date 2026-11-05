import numpy as np


A1 = np.array([[-1.0651, 1.0552], [0.0261, 0.9703], [2.0148, 3.0503], [1.9689, -0.9971]])
b = np.array([2.0187, 3.0239, 13.9598, 5.9321])
c = np.array([-0.9946, -3.0319, 0,0,0,0])
B = [2,3,4,5] 
N = [0,1]
A2 = np.array((np.eye(4)))

it = 0 

while True:
    
    x_B = np.linalg.solve(A2, b)
    z = c[B] @ x_B
    y = np.linalg.solve(A2.T, c[B])
    r_N = c[N] - A1.T @ y

    print("Detta är xB", x_B)
    print("Detta är z", z)
    print("Detta är y", y)
    print("Detta är r_N", r_N)

    if np.all(r_N >= -1e-10):
        break
    
    if it == 0:
        kindex = 0
    else:
        kindex = np.argmin(r_N)
    
    k = N[kindex]

    d = np.linalg.solve(A2, A1[:, kindex])
    
    tmax = []
    index = []
    for i in range(4):
        if d[i] > 0:
            tmax.append(x_B[i] / d[i])
            index.append(i)

    lindex = index[np.argmin(tmax)]
    l = B[lindex]


    temp_col = A2[:, lindex].copy()
    A2[:, lindex] = A1[:, kindex]
    A1[:, kindex] = temp_col

    B[lindex], N[kindex] = k, l

    it += 1 


