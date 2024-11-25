
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

# **Black Scholes Merton Model addition: dividend yield**

The assumptions of the model are quite restricted, but the importance of the framework is not in discussion. However, we can clearly adapt it by adding some basic things, starting with the dividend yield $q$. </br>
Therefore, the formula for *d1* and *d2* are as follows:

<div align="center">

$$
\begin{aligned}
\Large{d_1} & = \frac{\ln\left(\frac{S_0}{K}\right) + \left(r - q + \frac{\sigma^2}{2}\right)T}{\sigma\sqrt{T}} \\
\Large{d_2} & = \frac{\ln\left(\frac{S_0}{K}\right) + \left(r - q -\frac{\sigma^2}{2}\right)T}{\sigma\sqrt{T}}
\end{aligned}
$$

</div>



Since the information downloaded is not in real time, the results are not fully reliable. However, it would be possible to get more accurate option prices, if we were able to obtain the needed values from a faster data provider.

# Adding Option Greeks
The Option Greeks are a set of risk measures that indicate how sensitive an option's price is to various factors, such as changes in the price of the underlying asset, time decay, volatility, and interest rates. Therefore, they can help understanding the position that the company could have if it had a new option to the portfolio.

## Delta
Delta measures the sensitivity of the option's price to change with respect to changes in the price of the underlying asset. It represents the change in the option's price for a $1 move in the price of the underlying asset:
- For a put option, its value ranges from -1 to 0: for example, a Delta of -0.5 means that if the underlying asset's price increases by $1, the option price will decrease by $0.5.
- For a call option, its value ranges from 0 to 1: for example, a Delta of 0.5 means that if the underlying asset's price increases by $1, the option's price will increase by $0.50.

Delta can be used to hedge the portfolio position by ensuring that the overall portfolio has a net delta close to zero, making it less sensitive to small changes in the underlying asset's price.

<div align="center">

$$
\begin{aligned}
\Large{\Delta} & = \frac{\partial V}{\partial S} \\
\Large{\Delta_{\text{call}}} & = \Phi(d_1) \\
\Large{\Delta_{\text{put}}} & = -\Phi(-d_1)
\end{aligned}
$$

</div>


## Theta
Theta measures the sensitivity of the option's price to the passage of time, also known as time decay. It represents the amount by which the option's price decreases as time to expiration decreases by one day. Near expiration Theta tends to increase (in absolute value) as the option approaches expiration, especially for at-the-money options, since a slight increase or decrease could mean a bigger win or loss. </br>
It can also happen that Theta is negative, indicating that the option's value decreases over time, which is common for both call and put options.

<div align="center"">  

$$
\begin{aligned}
\Large{\Theta} & = -\frac{\partial V}{\partial \tau} \\
\Large{\Theta_{\text{call}}} & = -\frac{S\phi(d_1)\sigma}{2\tau} - rK\exp{(-rT)}\Phi(d_2) \\
\Large{\Theta_{\text{put}}} & = -\frac{S\phi(d_1)\sigma}{2\tau} + rK\exp{(-rT)}\Phi(-d_2)
\end{aligned}
$$

</div>

## Gamma
Gamma measures the rate of change of delta with respect to changes in the underlying asset's price. It indicates how much the delta will change if the underlying asset's price changes by $1.
- High Gamma: Indicates that delta is highly sensitive to changes in the underlying asset's price, which is typical for at-the-money options.
- Low Gamma: Indicates that delta is less sensitive to changes in the underlying asset's price, typical for deep in-the-money or out-of-the-money options.

Gamma is monitored to understand how delta might change with large price movements, helping to manage the risk of the delta-hedged portfolios.

<div align="center">
  
$$
\begin{aligned}
\Large{\Gamma} & = \frac{\partial \Delta}{\partial S} = \frac{\partial^2 V}{\partial S^2} \\
\Large{\Gamma} & = \frac{\phi(d_1)}{S\sigma\sqrt{\tau}}
\end{aligned}
$$

</div>

## Vega
Vega measures the sensitivity of the option's price to changes in the implied volatility of the underlying asset. It represents the change in the option's price for a 1% change in implied volatility.
- High Vega: Indicates that the option's price is highly sensitive to changes in volatility, common for longer-dated options or options that are at-the-money.
- Low Vega: Indicates that the option's price is less sensitive to changes in volatility.

<div align=center>  

$$
\begin{aligned}
\Large{\upsilon} & = \frac{\partial V}{\partial \sigma} \\
\Large{\upsilon} & = S\phi(d_1)\sqrt{\tau}
\end{aligned}
$$

</div>

## Rho
Rho measures the sensitivity of the option's price to changes in the risk-free interest rate. It represents the change in the option's price for a 1% change in the risk-free interest rate.
- Call Option: A positive rho means that the option's price increases as interest rates rise.
- Put Option: A negative rho means that the option's price decreases as interest rates rise.

<div align=center>  

$$
\begin{aligned}
\Large{\rho} & = \frac{\partial V}{\partial r} \\
\Large{\rho_{\text{call}}} & = K\tau\exp{(-rT)}\Phi(d_2) \\
\Large{\rho_{\text{put}}} & = -K\tau\exp{(-rT)}\Phi(-d_2)
\end{aligned}
$$

</div>


# **References**

## **Textbook**

- **[Options, Futures, and Other Derivatives, 11th Edition](https://elibrary.pearson.de/book/99.150005/9781292410623)**


<br/>
<br/>
<br/>
<b>Disclaimer: </b><br>
The code written in this file is for educational and informational purposes only. It is not intended as financial advice, and I make no guarantee of its accuracy, completeness, or suitability for any specific purpose. Any use of this code is at your own risk. I am not liable for any damages or losses arising from its use. Always perform your own testing and consult a financial professional before making any trading or investment decisions.
