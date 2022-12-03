# -- coding: utf-8 --
"""
Created on Wed Nov  3 15:33:48 2021

@author: SulisSandiwarno
"""

#from sklearn import tree
from sklearn.naive_bayes import MultinomialNB
#datasets
#Harga Tanah            #Jarak Pusat kota        #angkutan
x = [
    [0,                 0,                  1,],
    [1,                 0,                  1,],
    [2,                 0,                  1,],
    [2,                 2,                  1,],
    [2,                 1,                  1,],
    [1,                 2,                  0,],
    [0,                 2,                  0,],
    [0,                 1,                  1,],
    [2,                 2,                  0,],
    [1,                 1,                  0,]
]
#Target (C4)
y = [1, 1, 1, 0, 0, 0, 0, 1, 0, 1]
clf = MultinomialNB()
clf = clf.fit(x, y)


def prog() :
    hargaTanah = int(input("Harga Tanah? (0  murah, 1 sedang, 2 mahal) : "))
    Jarak = int(input("Jarak Pusat Kota? (0 Dekat, 1 Sedang, 2 jauh) : "))
    angkutan = int(input("Ada Angkutan? (0 Ada, 1 Tidak) : "))

    if clf.predict([[hargaTanah, Jarak, angkutan]]):
        print("\nDipilih untuk Perumahan")
    else:
        print("\nTidak Dipilih untuk Perumahan")

prog()
