git status    → verfica lo stato dei files
git log   	-> vedere la lsiat di commit
git remote -v    → vedere il repositorio remoto
git branch -v   → vedere tutti rami



git add .      → aggiungi tutti file nello stage
git commit -m "modifiche miglioramenti"    →   dai nome alle modifiche
git push origin master



git config --global --edit
[alias]
fatto = "!f() { git add . && git commit -m \"$1\" && git push origin master; }; f"


git fatto "NOME DELLA  COMMIIT"