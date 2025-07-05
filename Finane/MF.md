**Amount = Principal * Time * Return**
The transaction details are below –

- Amount – Rs.100,000/-
- Tenure – 5 years
- Interest (%) – 10

Principal = Rs.100,000/-
Interest = 10%
Yearly interest amount = 10% * 100,000
= Rs.10,000/-
Here is how the math looks –

|**Year**|**Principal Outstanding**|**Interest payable**|
|---|---|---|
|01|Rs.100,000/-|Rs.10,000/-|
|02|Rs.100,000/-|Rs.10,000/-|
|03|Rs.100,000/-|Rs.10,000/-|
|04|Rs.100,000/-|Rs.10,000/-|
|05|Rs.100,000/-|Rs.10,000/-|
|**Total Interest received**|   |**Rs.50,000/-**|
Amount = Rs.100,000 * 5 * 10%
= **Rs.50,000/-**

Banks don’t pay simple interest, they pay compound interest. What do you think is the difference between simple interest and compound interest?

 If someone agrees to pay you compound interest, then it essentially means that the person or the entity is agreeing to pay you interest on the interest already earned.

 The transaction details are as follows –

- Amount – Rs.100,000/-
- Tenure – 5 years
- Interest (%) – 10
- Interest type – Compound Interest (compounded annually)

**Year 1**

At the end of 1st year, you are entitled to receive a 10% interest on the principal outstanding and previous interest (if any)

assume you are closing this at the end of the 1st years, then you would receive the principal amount plus the interest applicable on the principal amount.

Amount = Principal + (Principal * Interest),  this can be simplified to
= Principal * (1+ interest)

Here, (1+interest) is the ‘interest’ part and the principal is obviously the principal. Applying this –

= 100,000 *(1+10%)
= 110,000

Now assume, you want to close this in the 2nd year instead of the first, here is how much you’d get back –

Remember, you are supposed to get paid interest on the interest earned in the first year, hence –

Principal *(1+ Interest) * (1+Interest)

principal *(1+ intrest) *  is the amount receivable at the end of the 1st year 
remaining is 2nd year 

Principal *(1+ Interest)^(2)
= 100,000*(1+10%)^(2)
= 121,000

In the 3rd year, you’d get interest on the 1st two year’s interest as well. The math –

Principal *(1+ interest) *(1+interest) *(1+interest)
Principal *(1+ Interest)^(3)
= 100,000*(1+10%)^(3)
= 133,100

We can generalize this –
**P*(1+R)^(n)**, where –
- P = Principal
- R = Interest rate
- N = Tenure

 if you were to have this open for the entire 5 years, you’d receive –
= 100,000*(1+10%)^(5) = 161051/-

You will use the **absolute** method to measure the return if your investment horizon is less than a year.

if your investment horizon is more than a year, you will use CAGR or the **compounded annual growth rate**, to measure returns.

You will make 10% of 100,000 which is Rs.10,000/-, in other words, your investment has grown by 10% on a year on year basis. This is the absolute return. This is straightforward because the time under consideration is 1 year or 365 days.

Now, what if the same investment was held for 3 years instead of 1 year, and what if instead of a simple return of 10%, the return was compounded annually at 10%? How much money would you make at the end of 3 years?

To calculate this, we simply have to apply the growth rate formula –

**Amount = Principal*(1+return)^(time)**

Which as you realize is the same formula used while calculating the compound interest. Applying this formula –

100,000*(1+10%)^(3)

= **Rs.133,100/-**

Referring to the previous section, if you were to charge compound interest, then this is the same amount of interest you receive from your friend in the 3rd year.

Continuing on the same lines, here is another question –

If you invest Rs.100,000/- and receive Rs.133,100/- after 3 years, then what is the growth rate of your investment?

To answer this question, we just need to reorganize this formula –

**Amount = Principal*(1+return)^(time)**

and solve for ‘return’.

By doing so, the formula reworks itself to –

**Return** = **[(Amount/Principal)^(1/time)] – 1**

Return here is the growth rate or the CAGR.

Applying this to the problem –

CAGR = [(133100/100000)^(1/3)]-1

= **10%**



![[Pasted image 20250705104949.png]]

- Simple interest is the interest that gets paid only on the outstanding principal
- Compound interest is paid on both interest and the principal outstanding
- Interest and return are like two sides of the same coin
- Absolute return is a measure of the growth in return when your investment is for less than a year
- Compounded annual growth rate (CAGR) is the measure of your return when your investment duration is more than a year
- Compounding works best when you give your investments enough time to grow


##  **Present value of money**

Consider that you purchased a piece of land for Rs.15,000,000/- today and held it for 15 years. After 15 years, you sell the land at Rs.75,000,000/-. On the face of it, this looks great, after all, you’ve made a five times return on this.

But here is an important question you need to ask yourself.  How valuable is Rs.75,000,000/- that you will receive 15 years from now, in today’s terms?

What if in 15 years from today, Rs.75,000,000/- is less valuable than Rs.15,000,000/-?

- What is my risk-free opportunity cost today?
- Given the risk-free opportunity cost, what is the amount that needs to be invested today, such that it grows to Rs.75,000,000/- in 15 years.


**Opportunity cost = Risk free rate + Risk premium**
This is what you could’ve earned _elsewhere_, safely.

- Risk-Free Rate (Govt Bond): **7.5%**
    
- Add Risk Premium (e.g., 1.5%):  
    ➡️ Total: **9% Opportunity Cost**

**Present value = Future value / (1+ discount rate ) ^ (time)**

Where:
- Future Value (FV) = ₹75,000,000
- r = discount rate = 9% = 0.09
- n = number of years = 15    

= 75,000,000 / (1+9%)^(15)
= 20,590,353



The future value of money is simply the inverse of the present value of money. Going by the real estate example, the future value of money helps us find an answer to a question like this –
- What will be the value of Rs.20,590,353/- in 15 years from now?
To find an answer to this question, we again must find out the opportunity cost. Irrespective of future value or present value problems we are trying to solve, the opportunity cost remains the same.

So, 9% will be the opportunity cost.

**= P*(1+R)^(n),** which is also the future value, therefor –

**Future value =** **P*(1+R)^(n)**

Where,

- P = Amount
- R = opportunity cost
- N = Time period

Applying this,

= 20,590,353 * (1+9%)^(15)

Remember, when we worked out the present value of Rs.75,000,000/- at a 9% discount rate for 15 years, the answer was 20,590,353. Now, we are trying to do the exact opposite i.e compound 20,590,353 at 9% for 15 years. So the answer has to be 75,000,000. When you do this math –

= 20,590,353 * (1+9%)^(15)

= **75,000,000**
