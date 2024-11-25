
<h1>Black Scholes Merton Model</h1>

The Black-Scholes-Merton Model is a mathematical framework used to estimate the price of European-style options - contracts that can only be exercised on their expiration date, unlike American options, which allow execution at any time before expiration.

<h1> Assumptions of the Model: </h1>

- No dividends are paid out during the life of the option.
- Market returns follow a random walk.
- There are no transaction costs in buying the option.
- The risk-free rate and volatility of the underlying asset are known and constant.
- The returns on the underlying asset are log-normally distributed.
- The option is European and can only be exercised at expiration.

<br/>
Once we take these assumptions for granted, the model provides the following formulas to compute the options:
<br/> 
<br/> 


<div align="center">

$$
\begin{aligned}
\Large{\textbf{European Call Option Value:}} & \quad S_0 N(d_1) - Ke^{-rT} N(d_2) \\
\Large{\textbf{European Put Option Value:}} & \quad Ke^{-rT} N(-d_2) - S_0 N(-d_1)
\end{aligned}
$$

</div>

The terms *N(d1)* is the cumulative probability that a random draw from a standard normal distribution will be less or equal to d1, and represents the probability that the option will finish in the money, adjusted for the fact that the payoff is based on the current asset price. </br>
Similarly, *N(d2)* is the cumulative probability that a random draw from a standard normal distribution will be less than or equal to d2, and represents the probability that the option will be exercised (the option is in the money at expiration).


<div align="center">

$$
\begin{aligned}
\Large{d_1} & = \frac{\ln\left(\frac{S_0}{K}\right) + \left(r + \frac{\sigma^2}{2}\right)T}{\sigma\sqrt{T}} \\
\Large{d_2} & = \frac{\ln\left(\frac{S_0}{K}\right) + \left(r - \frac{\sigma^2}{2}\right)T}{\sigma\sqrt{T}}
\end{aligned}
$$

</div>


Where:
- ${S_0}=$ Underlying Asset Price
- ${K=}$ Option Strike Price
- ${r=}$ Interest Rate
- $\sigma=$ volatility
- $T=$ Time

Let's try this with an example: The current price of a stock is 42$, its strike price is 40$, the risk-free rate is 10%, the volatility is 20%, and the strike date is in 6
