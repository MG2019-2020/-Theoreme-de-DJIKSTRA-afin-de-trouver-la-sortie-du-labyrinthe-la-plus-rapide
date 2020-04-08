import random

class graphe:
  def __init__(self):
    self.sommet = set()
    self.longu = defaultdict(list)
    self.distances = {}

  def ajout_noeud(self, value):
    self.sommet.add(value)

  def ajout_longu(self, from_noeud, to_noeud, distance):
    self.longu[from_noeud].append(to_noeud)
    self.longu[to_noeud].append(from_noeud)
    self.distances[(from_noeud, to_noeud)] = distance


def dijsktra(graphe, initial):
  vu = {initial: 0}
  path = {}

  sommet = set(graphe.sommet)

  while sommet: 
    noeud_min = None
    for noeud in sommet:
      if noeud in vu:
        if noeud_min is None:
          noeud_min = noeud
        elif vu[noeud] < vu[noeud_min]:
          noeud_min = noeud

    if noeud_min is None:
      break

    sommet.remove(noeud_min)
    current_weight = vu[noeud_min]

    for lon in graphe.longu[noeud_min]:
      weight = current_weight + graphe.distance[(noeud_min, lon)]
      if lon not in vu or weight < vu[lon]:
        vu[lon] = weight
        path[lon] = noeud_min

  return vu, path
