# Tableau Calculated Fields Reference

Copy-pasteable Tableau calculation code blocks designed for the **EV Performance Insights Dashboard**, conforming strictly to the Key Performance Indicators in PRD Section 8.

---

### 1. Sales in Millions (Measure)
Simplifies executive visual axes and KPI labels.

```tableau
// Sales in Millions
[Annual Sales (Units)] / 1000000
```

---

### 2. Manufacturer Market Share (LOD Expression)
Dynamically computes each manufacturer's percentage share of the market regardless of dimensions displayed on the shelf.

```tableau
// Manufacturer Market Share (%)
{INCLUDE [Manufacturer]: SUM([Annual Sales (Units)])} 
/ 
{EXCLUDE [Manufacturer]: SUM([Annual Sales (Units)])}
```
*Format: Percentage with 2 decimal places.*

---

### 3. Annual Market Share Progression (Fixed Year LOD)
Calculates OEM market share for a specific calendar year.

```tableau
// Annual Market Share (Fixed by Year)
SUM([Annual Sales (Units)]) 
/ 
ATTR({FIXED [Model Year] : SUM([Annual Sales (Units)])})
```
*Format: Percentage with 2 decimal places.*

---

### 4. Year-over-Year (YoY) Sales Growth (Table Calculation)
Computes the percentage sales growth between sequential model years.

```tableau
// YoY Sales Growth %
(ZN(SUM([Annual Sales (Units)])) - LOOKUP(ZN(SUM([Annual Sales (Units)])), -1)) 
/ 
ABS(LOOKUP(ZN(SUM([Annual Sales (Units)])), -1))
```
*Compute using: `[Model Year]`*

---

### 5. Value Index: Range per Price (Measure)
Measures vehicle value proposition: kilometers of range per $1,000 USD of MSRP.

```tableau
// Value Index (km / $1,000 Price)
([Driving Range (km)] / [Price ($)]) * 1000
```
*Format: Number with 2 decimal places.*

---

### 6. Sales-Weighted Fleet Driving Range (Measure)
Accurately weights fleet driving range by unit sales volume.

```tableau
// Sales-Weighted Avg Driving Range (km)
SUM([Driving Range (km)] * [Annual Sales (Units)]) / SUM([Annual Sales (Units)])
```

---

### 7. Sales-Weighted Fleet Battery Capacity (Measure)
```tableau
// Sales-Weighted Avg Battery Capacity (kWh)
SUM([Battery Capacity (kWh)] * [Annual Sales (Units)]) / SUM([Annual Sales (Units)])
```

---

### 8. Sales-Weighted Customer Rating (Measure)
```tableau
// Sales-Weighted Customer Satisfaction Rating
SUM([Customer Rating] * [Annual Sales (Units)]) / SUM([Annual Sales (Units)])
```

---

### 9. Customer Satisfaction Tier (Dimension)
Segments models into standardized rating bands.

```tableau
// Customer Satisfaction Tier
IF [Customer Rating] >= 4.7 THEN "Tier 1: Exceptional (4.70 - 5.00)"
ELSEIF [Customer Rating] >= 4.4 THEN "Tier 2: High Satisfaction (4.40 - 4.69)"
ELSEIF [Customer Rating] >= 4.0 THEN "Tier 3: Moderate (4.00 - 4.39)"
ELSE "Tier 4: Needs Improvement (< 4.00)"
END
```

---

### 10. DC Fast Charging Tier (Dimension)
Segments charging performance for infrastructure planning.

```tableau
// Fast Charging Tier
IF [Max Charging Speed (kW)] >= 250 THEN "Ultra-Fast (>= 250 kW)"
ELSEIF [Max Charging Speed (kW)] >= 150 THEN "High-Speed (150 - 249 kW)"
ELSE "Standard (< 150 kW)"
END
```

---

### 11. Vehicle Price Segment (Dimension)
Classifies vehicles by price bracket.

```tableau
// Price Segment
IF [Price ($)] < 25000 THEN "Budget / Entry (< $25k)"
ELSEIF [Price ($)] < 45000 THEN "Mass Market ($25k - $45k)"
ELSEIF [Price ($)] < 75000 THEN "Premium ($45k - $75k)"
ELSE "Luxury (> $75k)"
END
```

