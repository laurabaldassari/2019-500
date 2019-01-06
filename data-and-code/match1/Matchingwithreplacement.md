# On Matching with Replacement, using Matching

1. Suppose you run a 1:1 propensity match **with replacement**. You should want to know:
    - how many treated subjects are in your matched sample, and 
    - how many control subjects are in your matched sample
    
If you run a match using `match_with_replacement <- Match(Y, Tr, X, M=1, ties = FALSE)` then these answers come from `n_distinct(match_with_replacement$index.treated)` and `n_distinct(match_with_replacement$index.control)`, respectively. This method works for 1:2 matches, too.

2. When matching with replacement using the Match function from the Matching package, you should always indicate `ties = FALSE`.
    - So, `match2 <- Match(Tr=Tr, X=X, M = 1, ties=FALSE)` is OK, but `match2 <- Match(Tr=Tr, X=X, M = 1)` is not. 
    - You'll know it worked properly if you run `n_distinct(match2$index.treated)` and `n_distinct(match2$index.control)` and the control group size is no larger than the treated group size. 

Regardless of whether you're doing with or without replacement, run `Match` using `ties = FALSE`.
