# Trainingsumgebung PMP

In diesem Ordner befinden sich

- Jupyter Notebook Endabgabe
- Feinstaubmesswerte Stadt Graz
- Wetterdaten Stadt Graz

Getestet wurde die Umgebung wie beschrieben auf einem Ubuntu Server.

## Installierte Software Pakete

Mit dieser Software installiert und den .xlsx Dateien im selben Ordner wie das Jupyter Notebook lässt sich dieses ausführen.

per apt

```
libhdf5-serial-dev
graphviz
python3-opencv
vim
tmux
htop
ranger
docker-ce
mongodb
nodejs
npm
```

im python venv per pip3

```
numpy==1.18.0
scipy
matplotlib
h5py==2.10.0
pydot-ng
tensorflow-cpu
jupyterlab
pandas
pymongo
xlrd
seaborn
```

## Ursprüngliche Entwicklungsumgebung

Alle Herangehensweisen, die wir gegangen sind um ein Vorhersagemodell zu entwickeln befinden sich auf dem FH-Server, erreichbar unter:

- Server IP: 10.25.2.103
- Jupyter Lab Port: 8888
- Jupyter Lab Passwort: pmf

Läuft das jupyter-lab nicht, kann dieses durch aktivieren des virtual environments (~/MachineLearning/venvs/cpu) und ausführen von `jupyter-lab` gestartet werden.