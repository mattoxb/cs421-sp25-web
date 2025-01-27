<iframe id="kmsembed-1_oyoactbr" width="640" height="394" src="https://mediaspace.illinois.edu/embed/secure/iframe/entryId/1_oyoactbr/uiConfId/55779922/pbc/113245372/st/0" class="kmsembed" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" referrerPolicy="no-referrer-when-downgrade" sandbox="allow-downloads allow-forms allow-same-origin allow-scripts allow-top-navigation allow-pointer-lock allow-popups allow-modals allow-orientation-lock allow-popups-to-escape-sandbox allow-presentation allow-top-navigation-by-user-activation" frameborder="0" title="Tail Recursion"></iframe>

i
## Errata

Some changes needed in `fun1` and `fun3`:

```haskell
fun1 xx = aux xx 0
    where aux [] a = a
          aux (x:xs) a | even x = aux xs (a-1)  -- add 'a' on left side
                       | odd x  = aux xs (a+1)

fun3  n  = aux n 1 1 
    where aux 1 f1 f2 = f1 -- change to 1 to match original function
          aux n f1 f2 = aux (n-1) f2 (f1 + f2)
```

## Slides
- [[01.2.3-tail-recursion.pdf|Tail Recursion (PDF)]]
- [[01.2.3-tail-recursion-4up.pdf|Tail Recursion (4up, PDF)]]