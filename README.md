# Mexico Restaurant Intelligence Dashboard | Power BI

A full end-to-end business analytics project analyzing real-world restaurant ratings data from Mexico (2012), covering consumer demographics, restaurant attributes, and rating behavior across multiple cities and states.

---

## Project Overview

This project explores a Zomato-style restaurant ratings dataset to uncover actionable insights across four analytical dimensions — Local, Dining, Hospitality, and Behavioral. The workflow covers data importing, cleaning in Power Query, relational data modeling, DAX measure creation, and multi-page dashboard design in Power BI.

---

## Dataset Description

The dataset consists of 5 relational tables:

### Consumers
| Column | Description |
|---|---|
| Consumer_ID | Unique identifier for each consumer |
| City / State / Country | Consumer location |
| Latitude / Longitude | Geographic coordinates |
| Smoker | Whether the consumer smokes |
| Drink_Level | Abstemious, casual, or social drinker |
| Transportation_Method | Foot, public transport, or car |
| Marital_Status | Single or married |
| Children | Dependent / independent children |
| Age | Consumer's age |
| Occupation | Student, employed, or unemployed |
| Budget | Low, medium, or high |

### Consumer Preferences
| Column | Description |
|---|---|
| Consumer_ID | Unique identifier |
| Preferred_Cuisine | Types of cuisine the consumer prefers |

### Ratings
| Column | Description |
|---|---|
| Consumer_ID | Unique identifier |
| Restaurant_ID | Unique identifier |
| Overall_Rating | 0 = Unsatisfactory, 1 = Satisfactory, 2 = Highly Satisfactory |
| Food_Rating | Same scale as Overall_Rating |
| Service_Rating | Same scale as Overall_Rating |

### Restaurants
| Column | Description |
|---|---|
| Restaurant_ID | Unique identifier |
| Name | Restaurant name |
| City / State / Country / Zip | Location details |
| Latitude / Longitude | Geographic coordinates |
| Alcohol_Service | None, wine & beer, or full bar |
| Smoking_Allowed | Yes, no, bar section, or smoking area |
| Price | Low, medium, or high |
| Franchise | Whether the restaurant is a franchise |
| Area | Open or closed area |
| Parking | None, yes, public, or valet |

### Restaurant Cuisines
| Column | Description |
|---|---|
| Restaurant_ID | Unique identifier |
| Cuisine | Types of food the restaurant serves |

---

## Data Cleaning & Import

1. Get Data → More → All → Folder → Connect → select dataset folder path
2. Click Transform Data → Duplicate the file for each table
3. Expand each Binary file to load individual datasets
4. Cleaned and transformed all tables using Power Query (null handling, data type fixes, column renaming)

---

## Data Modeling

Built a star-schema style relational model in Power BI connecting all 5 tables via `Consumer_ID` and `Restaurant_ID` keys.

---

## DAX Calculated Columns

**Age Group**
```
AgeGroup =
SWITCH(
    TRUE(),
    consumers[Age] <= 18, "Children and Adolescents",
    consumers[Age] <= 30, "Young Adults",
    consumers[Age] <= 45, "Adults",
    consumers[Age] <= 60, "Middle-aged Adults",
    "Seniors"
)
```

**Service Rating Category**
```
Service_Rating_Category = SWITCH(
    TRUE(),
    ratings[Service_Rating] = 0, "Unsatisfactory",
    ratings[Service_Rating] = 1, "Satisfactory",
    "Highly Satisfactory"
)
```

**Overall Rating Category**
```
Overall_Rating_Category = SWITCH(
    TRUE(),
    ratings[Overall_Rating] = 0, "Unsatisfactory",
    ratings[Overall_Rating] = 1, "Satisfactory",
    "Highly Satisfactory"
)
```

**Food Rating Category**
```
Food_Rating_Category = SWITCH(
    TRUE(),
    ratings[Food_Rating] = 0, "Unsatisfactory",
    ratings[Food_Rating] = 1, "Satisfactory",
    "Highly Satisfactory"
)
```

---

## Dashboard Pages & Key Insights

### 📍 Local Insights
- Majority of consumers are from San Luis Potosí, followed by Cuernavaca, Morelos
- Young adults (under 30) dominate all three states
- Most consumers are non-smokers; Jiutepec has a 100% non-smoking population
- Most restaurants lack parking; valet parking exists only in San Luis Potosí and Cuernavaca

### 🍽️ Dining Insights
- San Luis Potosí has 84 restaurants vs. 23 each in Morelos and Tamaulipas
- Mexican cuisine is the most preferred, followed by American cuisine
- Non-franchise restaurants dominate and are evenly distributed across all rating categories

### 🏨 Hospitality Insights
- 66.92% of restaurants serve no alcohol; 26.15% offer wine & beer; 6.93% offer a full bar
- 61% of consumers use public transport; 27% use cars; 11% walk
- ~73% of restaurants maintain smoke-free policies

### 👤 Behavior Insights
- Students make up 93% of consumers in San Luis Potosí and 94% in Tamaulipas
- 67 students have a medium budget; only 4 have a high budget
- Among single consumers, all non-smokers show a declining trend from abstemious to social drinkers

### ⭐ Review Insights
- **Top Restaurant Overall:** Tortas Locas Hipocampo (most highly satisfied consumers)
- **Top 5 by Overall Rating:** Tortas Locas Hipocampo, Puesto de Tacos (30 highly satisfied), La Cantina Restaurante (28), Cafeteria y Restaurante El Pacífico (24), Restaurant la Chalita (20)
- Food and service ratings closely mirror overall satisfaction trends

---

## Tools & Technologies

| Tool | Usage |
|---|---|
| Power BI Desktop | Dashboard design, data modeling, DAX |
| Power Query | Data cleaning and transformation |
| DAX | Calculated columns and measures |

---

## Project Structure

```
📁 Dataset/
   ├── consumers.csv
   ├── consumer_preferences.csv
   ├── ratings.csv
   ├── restaurants.csv
   └── restaurant_cuisines.csv
📄 README.md
📄 Restaurant Ratings Analysis.pbix
```
