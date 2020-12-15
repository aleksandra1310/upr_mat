#!/usr/bin/env python
# coding: utf-8

# # Уравнение Навье-Стокса

# In[10]:


import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import matplotlib.animation as animation
from matplotlib.ticker import LinearLocator, FormatStrFormatter
from matplotlib import cm


# In[53]:


class Lab7(object):
    def __init__(self, u, h, n, m):
        self._init_matrix = np.zeros((n, m), dtype="float")
        self._u = u
        self._h = h
        self._n = n
        self._m = m
        self._prev_value = -1.0
        self._tolerance = 10e-6
        self._fig = plt.figure()
    
    def _calculate_value(self, i, j):
        value = self._init_matrix[i+1, j] + self._init_matrix[i-1, j]
        value += self._init_matrix[i, j+1] + self._init_matrix[i, j-1]
        value += self._u * (self._h**2)
        return value / 4.0
    
    def plot_matrix(self):
        self._fig.clear(True)
        plt.gcf().canvas.get_renderer()
        self._fig.set_dpi(150)
        self.ax = self._fig.gca(projection='3d')
        self.ax.set_zlim(0, 0.3)
        self.ax.zaxis.set_major_locator(LinearLocator(11))
        self.ax.zaxis.set_major_formatter(FormatStrFormatter('%.1f'))
        self.ax.view_init(25, 25)

        X = np.arange(0, self._n, 1)
        Y = np.arange(0, self._m, 1)
        X, Y = np.meshgrid(X, Y)
        Z = self._init_matrix.copy()
        norm = plt.Normalize(Z.min(), Z.max())
        colors = cm.viridis(norm(Z))
        rcount, ccount, _ = colors.shape
        
        surf = self.ax.plot_surface(
            X, 
            Y,
            Z,
            rcount=rcount,
            ccount=ccount,
            facecolors=colors,
            shade=False
        )
        surf.set_facecolor((0,0,0,0))
        plt.show()
    
    def print_results(self):
        data = pd.DataFrame(self._init_matrix)
        display(data)
    
    def main(self):
        while abs(self._prev_value-self._init_matrix[1,1]) > self._tolerance:
            self._prev_value = self._init_matrix[1, 1]
            for i in range(1, self._n-1):
                for j in range(1, self._m-1):
                    self._init_matrix[i, j] = self._calculate_value(i, j)
        self.print_results()
        self.plot_matrix()


# In[55]:


u = 2.0
h = 0.1
n = 11
m = 11
lab7 = Lab7(u, h, n, m)
lab7.main()


# In[56]:


u = 4.0
h = 0.1
n = 11
m = 11
lab7 = Lab7(u, h, n, m)
lab7.main()

