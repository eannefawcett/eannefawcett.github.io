---
layout: post
title:  "Finding All Factors for Any Number"
date:   2020-07-18 13:51:02
categories: technical, algorithms, python
paginator: Finding All Factors for Any Number
---

Today, I'd like to share a function I wrote in python with you that returns all factors for any number passed into the function. I found this tool to be useful when working through the problems posted at https://projecteuler.net/. I can foresee this also being useful in the development of other algorithms.






```def factors(number):
  '''Finds the all possible factors of the number, and returns a list of potential factors.'''

  divisible_by = range(1, number)

  potential_factors = []

  for i in divisible_by:

    if number%i == 0:

      potential_factors.append(i)

  return potential_factors
```






This function utilizes modulo division, represented by the "%" in python, to find the factors of the user's chosen number. In modulo division, the value returned is the remainder. In this case, if the remainder is zero, then the dividend and the devisor can be considered factors. With the number set to be the dividend and the range of values possible from 1 to the number set to be the divisor, any quotient with a remainder of zero will pass the if statement in the factors function above. With this pass, the divisor will be stored as a factor.

To avoid multiples of the same number appearing in the potential_factors list, only the divisor is stored. The quotient, which is also a factor for the number, will be evaluated separately. For instance, for the number 35, the divisor 5 will pass the if statement, since 35%5 = 0, so the divisor 5 will be stored in the potential_factors list. We know that 5 * 7 = 35, so 7 is the matching factor to 5. When the function arrives at 7 in the divisible_by list, the divisor 7 will pass the if statement, since 35%7 = 0, and it will be added to the potential_factors list. Recording the quotient value for each divisor is outside of the scope of what this function requires to operate effectively.

Although we might use the quotient and divisor when solving factor problems algebraically on paper, not all terms are necessary when doing the same work computationally. This is in part due to iteration. Remembering that all of the numbers from 1 to the selected number will be evaluated independently removes the ability to use the shortcut of matching divisors and quotients to find factors.

The thought process for generating the above function looked something like:

1. List out all of the possible numbers that could be multiplied together to get the chosen number.
2. See if pairs of possible numbers will match the chosen number.
3. How do I do know that the pair of potential numbers will match together to produce the chosen number in the first place?
4. If I divide the chosen number by one of the possible numbers; then, if I get a decimal, it didn't work. Move on to the next number. If it does work, then save it for later use.



This produced the pseudocode:

1. Develop a range of possible factors using the chosen number.
2. Determine if a decimal is present when diving the chosen number by the range of possible factors.
3. If a decimal is present, do nothing, and continue. If a decimal is not present, store the value.



To conclude, prior knowledge of math can be used to develop functions, in this case, a function to produce all factors for a given number. Sometimes, where we start in the problem solving process looks different than the end result. It's okay to start thinking in terms of one thing, multiplication in this case, and to swap to another way of thinking, in this case division, when a question can't be answered by the original terms of thinking.
