package : java.util.concurrent.Semaphore

rappel : les sémaphores agissent avec un compteur qui est incrémenté ou décrémenté par les threads. Si le compteur est à 0, les threads qui veulent accéder à la ressource sont bloqués. Si le compteur est à 1, les threads qui veulent accéder à la ressource sont débloqués.

`acquire` : réservé la ressource (après l'appel de la méthode)

