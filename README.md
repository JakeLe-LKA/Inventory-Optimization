# Inventory-Optimization

## Executive Summary

The report proposes an optimized inventory policy to maximize profit and ensure product availability. The strategy follows the periodic control inventory management method:  
- Each time the inventory is lower than the level **s** (reorder point), place an order to bring the inventory up to level **S** (order-up-to level).  
- This saves checking costs and simplifies management.

**Optimal strategy:**
- Reorder point (**s**): 165 units
- Order-up-to level (**S**): 575 units
- Expected annual profit: ~EUR 161,000  
- Low financial risk  
- Recommend quarterly review for continuous improvement.

This policy will help **SAIGON BEERS CO.** increase profit while minimizing risk and maintaining product availability.

---

## Description of Business

- **Company Name:** SAIGON BEERS CO  
- **Business Type:** Beverage industry (beer production and sales)  
- **Products/Services:** Premium to mass-market beer products  
- **Organization Size:** Medium-to-large, operating in Vietnam and planning regional expansion  
- **Market Type:** Monopolistic competition  
- **Main Competitors:** Heineken Vietnam, SABECO, local craft brands  

---

## Description of the Problem

### Business Issue

SAIGON BEERS CO needs to efficiently manage beer inventory to:
- Maximize profit  
- Avoid stockouts  
- Minimize holding costs  

Key decision: Choose optimal (s, S) inventory policy

- **s**: Reorder point (triggering order)
- **S**: Order-up-to level

### Stakeholder Expectations

#### Chief Operating Officer (COO)
- Ensure product availability
- Minimize reordering disruptions
- Be responsive to demand spikes (holidays, festivals)

#### Chief Financial Officer (CFO)
- Minimize holding & ordering costs
- Reduce tied-up capital
- Maximize profit while controlling risks
  
---
### Feasible Set of Decisions

- **Decision variables:** s (reorder point), S (order-up-to level)

**Constraints:**
- Warehouse Capacity: `S ≤ 1000`
- Minimum Safety Stock: `s ≥ 100`
- Beer Shelf Life: `S ≤ 600` (practical)
- Reasonable Order Size: `S - s ≈ 300–500`

---

### Objective Function

**Goal:** Maximize profit = revenue – inventory cost – ordering cost – stockout cost

```math
∑_{j=1}^{m} [ c·min(Dj, Xj) - h·Yj - Kj - k·(S - Yj) - l·max(0, Dj - Xj) ]
```
Where:
- **Dj**: demand at day *j* (Poisson distributed)
- **Xj**: inventory level at day *j*
- **Yj**: leftover inventory at end of day *j* (`max(0, Xj - Dj)`)
- **K**: fixed cost per order (€)
- **k**: variable cost per bottle ordered (€)
- **c**: profit per bottle sold (€)
- **h**: holding cost per bottle per day (€)
- **l**: penalty cost per bottle lost due to stockout (€)

### Consequences of Decisions
- Profit: Optimized (s, S) improves profitability
- Risk:  
Too low s/S → stockouts, lost sales  
Too high S → high holding costs, risk of spoilage

---

## Results and Analysis

The numerical results indicate that the optimal inventory policy is to set the reorder point **s** at **165 units** and the order-up-to level **S** at **575 units**. Under this strategy, the **expected annual profit is approximately €161,000**.

The process of looking for the above optimal solution can be shown using the tables and figures below:

**Table 1: Optimal s, S for the highest expected profit in the 1st simulation**

| Best (s, S) | Mean profit (€) | Profit std | Stock out bottles | Stock out std | Fill rate (%) |
|-------------|------------------|------------|--------------------|----------------|----------------|
| (150, 550)  | 160 310          | 2 068      | 1 580              | 421            | 97.6%          |

**Figure 1: Expected profit by different s, S point in the 1st simulation**

![Simulation Heatmap](Graphs%20and%20Pictures/491003846_1631281967552845_2130734520271673625_n.png)

Table 1 and Figure 1 shows the maximum expected return of the model in 100 simulations with each different point s, S located in the yellow cells near (150, 550). From there, we narrowed the search space, using smaller steps, and increased the number of simulations to 1000 to find a more stable optimal solution.

**Table 2: Optimal s, S for the highest expected profit in the 2nd simulation**

| Best (s, S) | Mean profit (€) | Profit std | Stock out bottles | Stock out std | Fill rate (%) |
|-------------|------------------|------------|--------------------|----------------|----------------|
| (165, 575)  | 161 531        | 1726    | 970           | 356         | 98.5%         |

**Figure 2: Expected profit by different s, S point in the 2nd simulation**

![Simulation Heatmap](Graphs%20and%20Pictures/491025963_1853225465458904_5621856421242682805_n.png)

Figure 2 indicates almost the same solution, which has the densest yellow cluster sitting around (165, 575).

From a business perspective, the result appears achievable and realistic. The storage requirements stay within the company's warehouse capacity, and the replenishment quantity (around 410 units) is manageable for the warehouse operations. Furthermore, the result aligns with typical expectations for businesses selling fast-moving consumer goods like beer: having a sufficient safety stock is crucial to avoid lost sales, while excessive stock should be avoided due to spoilage risks. The optimization results also appear consistent with intuition. Since beer is a perishable and highly demanded product, it makes sense that the company should avoid stockouts but also not store too much. The recommended inventory levels strike a good compromise. There are no surprising outcomes — the model's suggestion matches what managers would reasonably expect when balancing risk and profit.

---

## Sensitivity Analyses

This part will answer an important question:  
*"Is the current optimal result sustainable when the business environment changes?"*

In the context of an inventory management system (s, S), many input parameters can fluctuate differently due to unstable economic conditions, from interest rates to operating costs. The following analysis will focus on the main parameters that affect the optimal solution (s, S) and assess the sensitivity of the model to each factor.

**Table 3: Simulation model’s parameters affecting the Expected Profit**

| Parameter | Impact on Inventory Strategy (s, S) |
| :--- | :--- |
| Unit profit (c) | Increase in c → Business holds more inventory to reduce risk of lost sales. |
| Holding cost (h) | Increase in h → Decrease in S to reduce inventory levels, favoring faster turnover. |
| Fixed ordering cost (K) | Increase in K → Increase in s to reduce order frequency, consolidating orders to save costs. |
| Probability of delivery success (p) | Increase in p → Decrease in s, allowing more frequent orders due to lower stockout risk. |
| Average demand (average_demand) | Increase in average demand → Increase in S to meet higher customer demand. |
| Stock-out penalty (l) | Increase in l → Increase in S to reduce stockout risk and avoid high penalties. |
| Variable order cost (k) | Increase in k → Similar effect to K (increase in s), but to a smaller extent. |
| Initial inventory (init_S) | Higher init_S → Decrease in early replenishment needs (delays first order), temporarily reducing s. |

By changing each parameter while keeping other factors constant (*ceteris paribus*), we determine the amount of change required to change the optimal solution. Charts and data tables will illustrate the impact of each parameter on total profit and inventory configuration, supporting flexible decision-making in volatile market conditions [Chong and Zak, 2013].

---

### Key sensitive parameters

#### Fixed ordering cost (K)

We investigate the effect of the fixed ordering cost parameter (K) on the optimal inventory strategy (s, S) and the expected profit.

- Base K level: **150**
- K values considered: **50 to 250** (increment of 25 units)

Each K level is simulated to find the corresponding optimal pair (s, S) and calculate the average profit (profit_mean).

**Table 4: Optimal (s, S) and Expected Profit by different value of Fixed Ordering Cost (K)**

| K | s | S | Expected profit |
| :--- | :--- | :--- | :--- |
| 50 | 175 | 565 | 173 616 |
| 75 | 175 | 565 | 170 522 |
| 100 | 170 | 565 | 167 490 |
| 125 | 160 | 570 | 164 491 |
| 150 | 140 | 570 | 161 468 |
| 175 | 170 | 570 | 158 498 |
| 200 | 155 | 570 | 155 489 |
| 225 | 160 | 570 | 152 560 |
| 250 | 155 | 570 | 149 515 |

The results show that the optimal inventory strategy has a relatively high level of stability against changes in ordering costs. Specifically, the reorder threshold (S) remains almost constant around 570, while the s level tends to adjust slightly from 175 to around 155–160 as K increases. This shows that the inventory policy proposed by the model is quite flexible and sustainable when K changes in a wide range.

From the results table, it can be seen that simply increasing K from 150 to 175 or decreasing it to 125 leads to a change in the optimal value of (s, S).

**Figure 3: Relationship between Expected Profit and Fixed Ordering Cost (K)**

![Relationship between K and expected profit](Graphs%20and%20Pictures/iScreen%20Shoter%20-%20Google%20Chrome%20-%20250429071011.png)

In addition, the expected profit (profit_mean) tends to decrease almost linearly as K increases. This is consistent with the theoretical expectation because higher ordering costs will reduce overall efficiency. However, this change does not cause major disruptions in the inventory strategy, showing that the designed system is well adapted to cost fluctuations in practice.

#### Storage cost (h)

We investigate the impact of the storage cost parameter (h) on the optimal inventory strategy (pair (s, S)) and the expected profit of the system. The value of h is adjusted from 0.05 to 0.5 in increments of 0.05 to simulate different capital cost scenarios in the context of high market interest rates.

**Table 5: Optimal (s, S) and Expected Profit by different value of Storage Cost (h)**

| h | s | S | Expected profit |
| :--- | :--- | :--- | :--- |
| 0.05 | 175 | 600 | 177 535 |
| 0.1 | 160 | 595 | 173 229 |
| 0.15 | 155 | 580 | 169 175 |
| 0.2 | 175 | 575 | 165 276 |
| 0.25 | 165 | 570 | 161 514 |
| 0.3 | 170 | 570 | 157 775 |
| 0.35 | 150 | 560 | 154 118 |
| 0.4 | 165 | 560 | 150 484 |
| 0.45 | 155 | 560 | 146 793 |
| 0.5 | 145 | 560 | 143 244 |

The results from the table show a very clear negative relationship between storage cost and optimal profit. Specifically, as h increases from 0.05 to 0.5, the expected profit (profit_mean) decreases almost linearly from about 177,535 units to 143,244 units. This is in line with the theory because higher storage costs will reduce profit margins due to increased holding costs as emphasized by Silver et al. (1998), an increase in holding cost typically leads to a decrease in inventory levels to minimize carrying costs.

Regarding the inventory strategy, we observe that the maximum order level (S) tends to decrease slightly from 600 to 560, while the reorder threshold (s) decreases significantly from 175 to 145 as h increases. This trend reflects a reasonable behavior of the model: when the cost of inventory is higher, the system tends to hold less inventory to avoid incurring additional capital costs, while being more flexible in the decision to reorder  [Zipkin, 2000].


**Figure 4: Relationship between Expected Profit and Storage Cost (h)**

![Relationship between h and expected profit](Graphs%20and%20Pictures/491368581_577750774747548_6165918172029333487_n%20(1).png)

The linear plot between h and the optimal profit clearly visualizes the impact of inventory costs on system performance. The trend line shows the high stability of the model in response to fluctuations in this parameter, and provides a solid basis for decisions to adjust inventory policy in a volatile economic context.

#### Profit per unit (c)

Finally, we look into the effect of the profit per unit parameter (c) on the optimal inventory strategy (s, S) and expected profit (profit_mean). The base c level in the model is considered from 3.0 to 4.0 with a step of about 0.15 units. At each level of c, the model will find the corresponding optimal pair (s, S) and calculate the average profit achieved.

**Table 6: Optimal (s, S) and Expected Profit by different value of Unit per profit (c)**

| c | s | S | Expected profit |
| :--- | :--- | :--- | :--- |
| 3.0 | 165 | 565 | 129 190 |
| 3.15 | 165 | 565 | 138 855 |
| 3.325 | 165 | 565 | 150 227 |
| 3.5 | 170 | 575 | 161 437 |
| 3.675 | 145 | 565 | 172 789 |
| 3.85 | 165 | 570 | 184 152 |
| 4.0 | 170 | 565 | 193 844 |

The results from the data table show that the optimal inventory strategy (s, S) has some slight adjustments when the profit per unit changes. Specifically, the reorder threshold level (S) fluctuates around 565–575, while the s level changes from 145 to 170 depending on the value of c. However, this fluctuation is not large, indicating that the inventory policy is quite stable in the face of moderate changes in unit cost.

In terms of expected profit, the graph shows that profit tends to increase almost linearly as the unit cost of the product increases from 3.0 to 4.0. 

**Figure 5: Relationship between Expected Profit and Profit per unit (c)**

![Relationship between c and expected profit](Graphs%20and%20Pictures/relationship_c.png)

From the data table, it can be seen that different levels of c (e.g. from 3.0 to 3.5) still maintain the same inventory strategy (s ≈ 165–170 and S ≈ 565–575). However, as c continues to increase (from 3.675 onwards), there is a more pronounced change in the level of s (down to 145) to optimize inventory costs in the context of higher product costs.

We also build a simple linear regression model with the expected profit as the target variable and the above three parameters as the explanatory variables to see exactly the relationship between them.

**Table 7: Coefficient of the regression model between Expected Profit and the parameters**

![Coefficient](Graphs%20and%20Pictures/coef.png)

The regression results show that all of these parameters are statistically significant and how sensitive the expected profit is to changes in each of the key parameters: storage cost (h), unit cost (c), and fixed ordering cost (K).

- Storage Cost (h) has a strong negative effect on expected profit, with a coefficient of -77,754.6. This means that for every one-unit increase in storage cost, expected profit decreases by approximately 77,755 units, confirming the significant financial burden of higher inventory holding costs.
- Profit per unit (c) has a strong positive impact, with a coefficient of +64,681.6, implying that as c increases (likely correlated with higher selling price or adjusted demand), expected profit increases substantially.
- Fixed Ordering Cost (K) also negatively affects profit, but to a much smaller extent compared to h, with a coefficient of -120.46. This suggests that each additional unit in K reduces expected profit by about 120 units.

Our key takeaways are that the model shows high robustness to changes in fixed ordering cost (K), with only slight adjustments in (s, S) even when K varies significantly. Expected profit decreases almost linearly with K, but the inventory policy remains sustainable without major disruption.

Second, storage cost (h) has a strong negative impact on both optimal profit and inventory levels. As h increases, the system naturally adapts by lowering both reorder points (s) and maximum stock levels (S), promoting a leaner inventory approach to mitigate rising capital costs.

Third, although changes in profit per unit (c) cause only moderate shifts in the inventory strategy, the expected profit shows an almost linear increasing trend, suggesting specific model assumptions where selling price or demand could be linked to production cost.

Overall, the sensitivity analysis confirms that the current optimal solution is generally sustainable under moderate changes in key parameters. However, in environments with high capital or ordering cost volatility, proactive adjustment of inventory policies will be crucial to maintaining profitability and operational efficiency.

---

## Overall recommendation

The conducted optimization analysis identified a robust optimum at s = 165, S = 575. Averaged over 1000 simulations, this policy delivers a mean annual profit of €161 531, a profit coefficient of variation of 1.1 %, and a fill rate of 98.5 %. This setting offers the best balance between minimizing the risk of stockouts (which would result in lost sales) and avoiding excessive holding costs (which would reduce profit margins).

The results align well with business intuition: ordering too late (low s) increases the risk of running out of stock, while setting an overly high inventory threshold (high S) raises storage costs significantly. Thus, the selected optimal (s, S) parameters reflect a practical and executable policy for SAIGON BEERS CO under current demand conditions.

In addition to the main optimal recommendation, two alternative solutions are proposed to accommodate potential shifts in business priorities or market conditions:
- The first alternative sets s = 165 and S = 560, slightly reducing the order-up-to level. This option would prioritize lowering inventory holding costs, which may be preferable if warehouse space becomes limited or if cash flow constraints intensify. The expected profit under this setting would decrease only marginally compared to the optimal solution.
- The second alternative proposes s = 150 and S = 580, slightly increasing the order-up-to level and while reducing the reorder point. This strategy enhances product availability, reducing the risk of stockouts, and may be advisable if the company expects surges in demand (e.g., seasonal effects or promotional campaigns).
  
From a technical standpoint, these results provide actionable and flexible inventory policies that can be dynamically adjusted based on evolving business needs. Moreover, implementing simulation analysis like this regularly can significantly improve SAIGON BEERS CO’s operational resilience and profitability by ensuring that inventory decisions remain optimized over time, even as demand patterns or cost structures change.
