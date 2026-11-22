## Hamming numbers implementation
- Surname,Name: Kariavkina, Elizaveta
- Student ID: 12450960



## Hamming numbers 
- The output from my code are hamming numbers, thougth duplicates appear(not forbidden by task)
- I find the reason in my merge function, because it does not check if the same number has appeared in cpyin before
-As for the reason why they append:
-Numbers, which are a result muliplication of 2 or more numbers, can be written in changing the places of their multipliers
-For Example: 10 = 2 * 5 = 5 * 2
-As for my algorithm it first puts 1, 2,3, 5, then 2*2, 3*2, 5*2 .... 2*5, 3*5, 5*5


## Custom blocking queue
-I used linked list and synchronise to restrict access tho this list
