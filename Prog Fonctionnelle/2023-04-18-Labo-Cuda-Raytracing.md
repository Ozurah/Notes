3 versions :
- `GM` : Global Memory
  - host ==> kgm
  - device ==> kgm
- `SM` : Shared memory
  - host ==> ksm
  - device ==> ksm
- `CM` : Constant memory
  - host ==> kcm
  - device ==> kcm

Mémoires sur le device : `ptrGM`, `ptrSM`, `ptrCM`
--> Envoyées à la méthode "work" qui est identique pour les 3 versions
`work(float* ptrDev)`


La share memory sera utilisée comme un **cache**

![](Export/schema-TP6%20-%20CudaRaytracing.drawio.svg)

# Rappel pour l'ordre d'implem
1. Avoir un rendu "gris"
2. Implémenté la logique (work)
3. Faire les versions (GM, SM, CM)