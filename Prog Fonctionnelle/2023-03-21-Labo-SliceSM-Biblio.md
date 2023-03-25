# ReductionAdd
(add.int.Pi.device.reductionAddIntI_device ????) :
```cpp
KAddIntProtocoleI(....)
    ... // Comme le generic
    ReductionAdd::reduce(tabSM, ptrSumGM);
```

# `01_cudatools.generic.Reduction.cu.h

```cpp
#pragma once

#include "Lock.cu.h"
#include "Thread2D.cu.h"

/*----------------------------------------------------------------------*\
 |*			prt fonction / reduction			*|
 \*---------------------------------------------------------------------*/

#define BinaryOperator(name) T (*name)(T, T)
#define AtomicOp(name) void (*name)(T*, T)

/*----------------------------------------------------------------------*\
 |*			Implementation 					*|
 \*---------------------------------------------------------------------*/

class Reduction
{
public:
	template <typename T>
	static __device__ void reduce(BinaryOperator(OP) ,AtomicOp(ATOMIC_OP), T* tabSM, T* ptrResultGM)
	//static __device__ void reduce(T (*OP)(T, T) ,void (*ATOMIC_OP)(T*, T), T* tabSM, T* ptrResultGM) // idem ci-dessus mais sans define
    {
	    // Meme principe que ReductionAdd

	    reductionIntraBlock(OP, tabSM);
	    //__synchTrheads() pas utile de le mettre ici, car on a deja mis un syncthreads dans le intra, en avoir 2 r�duirait les perfomances
	    // Il ne faut pas que le InterBlock soit execut� qu'apr�s le intra donc bien s'assurer avoir le syncthread avant l'interblock
	    reductionInterBlock(ATOMIC_OP, tabSM, ptrResultGM)

	    //__syncThreads() pas utile ici
    }

private:

	/*--------------------------------------*\
	|*	reductionIntraBlock		*|
	 \*-------------------------------------*/

	/**
	 * used dans une boucle in reductionIntraBlock
	 */
	template <typename T>
	static __device__ void ecrasement(BinaryOperator(OP),T* tabSM, int middle)
    {
	    // TODO ReductionGeneric
	    // Meme principe que ReductionAdd
	    // OP est la variable representant l'operateur binaire

	    const int TID_LOCAL = Thread2D::tidLocalBlock();

	    if(TID_LOCAL < middle)
		{
            tabSM[TID_LOCAL] = OP(tabSM[TID_LOCAL + middle]);
		}
    }

	/**
	 * Sur place, le resultat est dans tabSM[0]
	 */
	template <typename T>
	static __device__ void reductionIntraBlock(BinaryOperator(OP),T* tabSM)
	    {
	    // Meme principe que ReductionAdd
	    // OP est la variable representant l'operateur binaire

	    int m = Thread2D::nbThreadBlock() >> 1;

	    //Si on mets un IF ici pour filtrer qui fait ...
	    while(m > 0)
		{
            ecrasement(OP, tabSM, m);
            m = m >> 1;
            __syncthreads(); // ... Certain thread du block n'attendrait pas le sync, et cette barri�re n'est lev�e que quand le m�me nombre de thread qu'ayant appel� la m�thode est atteint
            // Du coup on a mis le "IF" filtrant dans l'�crasement
            // il est conseill� de mettre syncthreads dans les m�thodes appelantes plut�t que les "feuilles"
		}
    }

	/*--------------------------------------*\
	|*	reductionInterblock		*|
	 \*-------------------------------------*/

	template <typename T>
	static __device__ void reductionInterBlock(AtomicOp(ATOMIC_OP), T* tabSM, T* ptrResultGM)
	    {
	    // Meme principe que ReductionAdd
	    // ATOMIC_OP est la variable representant l'operateur binaire atomic
	    const int TID_LOCAL = Thread2D::tidLocalBlock(); // tidLocal == tidLocalBlock == tidBlock (pour correspondre en fonction du support)

	    if(TID_LOCAL == 0)
		{
            ATOMIC_OP(ptrsss, tabSM[0] )
            // pas besoin de __syncthreads(); car on est � la fin du code ici
            // Si on le mettrait, on ralenti les performances
		}
    }

    };
```

# `02_use_cuda.generic.int.PI.device.reductionIntI_device.cu`

```cpp
__global__ void KIntProtocoleI(int* ptrSumGM)
    {
    extern __shared__ int tabSM[]; // réceptionner notre tabSM du driver NVidia (pas de dimensions

    reductionIntraThread(tabSM);
    __syncthreads(); // on le mets ici car c'est un peu plus logique, on est le chef d'orchestre donc c'est nous qui dirigions
    Reduction::reduce(add, addAtomicV1, tabSM, ptrSumGM);
    }
```

```
__device__ void addAtomicV1(int* ptrX , int y)
    {
    atomicAdd(ptrX, y) // atomicAdd de la bibliothèque NVidia (il n'y a pas pour les longs par exemple --> voir addAtomicV2)
    }
```