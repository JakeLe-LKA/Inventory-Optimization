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

**Table 3**: Simulation model’s parameters affecting the Expected Profit

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

**Table 4**: Optimal (s, S) and Expected Profit by different value of Fixed Ordering Cost (K)

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
