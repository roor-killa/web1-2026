# web1-2026
Cours Web 1 2026
import random

class File:
    def __init__(self):
        self.tab = []

    def file_vide(self):
        return self.tab == []

    def enfiler(self, v):
        self.tab.append(v)

    def defiler(self):
        if not self.file_vide():
            self.tab.pop(0)

    def tete(self):
        if not self.file_vide():
            return self.tab[0]
        else:
            return None

    def affiche_file(self):
        print("-------")
        for i in range(len(self.tab)):
            print(self.tab[len(self.tab)-i-1], ' ', end='')
        print()
