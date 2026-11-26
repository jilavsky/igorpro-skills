---
description: "The StatsPermute function permutes elements in waveA based on the lexicographic order of waveB and the direction dir."
slug: /commands/statspermute
---

<div className="command-signature">

## <strong>StatsPermute</strong> (<em>waveA</em>, <em>waveB</em>, <em>dir</em>) {#statspermute}

</div>

The StatsPermute function permutes elements in *waveA* based on the lexicographic order of *waveB* and the direction *dir*. It returns 1 if a permutation is possible, and returns 0 otherwise. Use *dir*=1 for the next permutation, and *dir*=-1 for a previous permutation.

### *Details* {#details}
Both *waveA* and *waveB* must be numeric. The lexicographic order of elements in the index wave is set so that permutations start with the index wave *waveB* in ascending order and end in descending order. Elements of *waveA* are permuted in place according to the order of the indices in *waveB* which are clipped (after permutation) to the valid range of entries in *waveA*. *waveB* is also permuted in place in order to allow you to obtain sequential permutations. If *waveA* consists of real numbers, you can permute them using the lexicographic value of the entries directly. To do so, pass $"" for *waveB*. Whenever it returns 0, neither *waveA* and *waveB* are changed.  If waveB is not null, it must be real valued. WaveA may be complex if waveB is not null.

### *Examples* {#examples}

```igor
Function AllPermutations(num)
	Variable num
	
	Variable i,nf=factorial(num)
	Make/O/N=(num) wave0=p+1,waveA,waveB=p
	
	Print wave0
	for(i=0;i<nf;i+=1)
		waveA=wave0
		if(statsPermute(waveA,waveB,1)==0)
			break
		endif
		print waveA
	endfor
end
```

Executing `AllPermutations(3)` prints:
```
  wave0[0]= {1,2,3}
  waveA[0]= {1,3,2}
  waveA[0]= {2,1,3}
  waveA[0]= {2,3,1}
  waveA[0]= {3,1,2}
  waveA[0]= {3,2,1}
```

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md)