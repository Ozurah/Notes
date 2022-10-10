Code | Explication
---|---
reg = re.compile(strreg) | compile la regex pour la rendre plus rapide (converti 1 fois et stock dans une variable)
re.search(strreg, string) | compilation + recherche
reg.search(string) | recherche

# String -> Expr. Rég
```py
strReg = "^A"
reg = re.compile(strReg)
reg = re.compile(r''+strReg)
```