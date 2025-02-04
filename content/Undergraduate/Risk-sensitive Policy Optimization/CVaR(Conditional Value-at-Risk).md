Risk measure that quantifies the potential loss in value of an investment portfolio beyond a certain confidence level

portfolio - collection of a financial assets(stocks, bonds, cash equivalents,...) typically managed with a goal of achieving financial objectives(maximizing return, minimizing risk,...). 
### Calculation
Given risk level $q \in (0,1]$, CVaR of a random cost $C$ is defined as
$$\text{CVaR}_q[C]:=\int_0^q \text{VaR}_u[C]du$$
where $\text{VaR}_q[C]:=\text{inf}\{ \eta \in\mathbb{R}|P(C\leq\eta)\geq1-q \}$ , worst $q$-quantile of the cost distribution
