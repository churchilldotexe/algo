# BIG O
   As your input grows, how fast does computation or memory grow? 

   Important complexity concept to Remember:
   - grows is with respect to input.
   - drop the constant
   - expect the worst case 

### trick to tell what complexity a logic is 
   - look for loops
   
```ts
   function sum_char_codes(n:string):number{
      let sum = 0
      for(let i=0;i<n.length;i++){ 
         sum += n.charCodeAt(i)
      }

      return sum
   }
```
in the example above it is a O(n) because the iteration(looping) output of n depends on the count of n parameter.
As "n" grows the output grows(linear = O(n))


### Another Big O trick
if the input halves at each steps, its likely O(logN) or O(NlogN)
- halving means = log 
- multiplying means = squared
