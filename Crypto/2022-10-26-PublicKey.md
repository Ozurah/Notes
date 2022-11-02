> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `4. Public Key Cryptography - diffie-Hellmann`</span>

- Cryptographie asymétrique
  - pas de problème de partage de clé
    - La public est partagée à tous
    - la privée est gardée secrète
  - Signer un message avec la clé privée
  - Vérifier la signature avec la clé publique
  - **Confidentialité** <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// Le plus important</span> 
- Cryptographie symétrique
  - 1 seule clé de cryptage
  - Partage de la clé entre les membres

# Fonction de Caramichael

![](Screen/2022-10-26-10-54-22.png)
== **Ordre de k**, mentionné le HW de la semaine 5



# Diffie-Hellmann

![](Screen/2022-10-26-11-12-27.png)

| key     | Alice                                                                                          | Bob                                                                                            |
| ------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| private | a                                                                                              | b                                                                                              |
| public  | $A = g^a \% p$                                                                                 | $B = g^b \% p$                                                                                 |
| linked  | $S = B^a \% p = (g^b)^a \%p$ <span style="color: green;font-size:1.5em">$= g^{ab} \% p$</span> | $S = A^b \% p = (g^a)^b \%p$ <span style="color: green;font-size:1.5em">$= g^{ab} \% p$</span> |

Avec la clé publique, il n'est pas possible de trouvé la privée (exposant), à cause de la multitude de possibilités d'obtenir le même résultat.

Quand les clés publiques sont liées, partagés, les clés deviennent les mêmes

## Cryptage/Décryptage

> <span style="font-size: 1.5em">📍</span> <span style="color: orange; font-size: 1.3em;">numéro de slides `43-50` (explication des étapes)</span>



<!-- #region TODO BLOCK --> 
<div style="margin: 20px auto; padding: 10px; background-color: #ffd48a; border-left: 5px solid #8a5700;color: black; font-size: 2em">
<span> 📝 </span>TODO<br>
<span style="font-size: 0.75em">
intégrer les notes de Sarah pour cette partie au lieu d'une simple image de ses notes.

<span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// Cependant, elle est super bien !! :D</span> 
</span></div>

<!-- #endregion TODO BLOCK -->

![](Screen/2022-10-26-11-23-43.png)


$C_A * A^{p-1-b} = M_A * g^{ab} * (g^a)^{p-1-b} = M_A * g^{ab} * g^{-ab} * g^{a*(p-1)} \% p = M_A * 1 * (g^{p-1})^a = M_A$	