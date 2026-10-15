# Multi-Agent Agricultural Optimization System for Morocco

An explainable **multi-agent decision-support system** for agricultural crop allocation and optimization using real Moroccan agricultural datasets.

The system combines:

- Multi-Agent Systems
- Fuzzy Logic
- Agricultural Data Analysis
- Crop Suitability Scoring
- Scenario Ranking
- Resource Optimization
- Interactive Visualization

The objective is to recommend suitable crop allocations while considering factors such as soil quality, water availability, climate conditions, crop compatibility and resource balance.

---

## Project Overview

Agricultural planning involves several interacting factors:

- Soil conditions
- Water availability
- Climate
- Crop characteristics
- Fertilizer efficiency
- Farm strategy
- Available agricultural surface

Instead of treating these factors as a single prediction problem, this project models them using specialized autonomous agents.

Each agent evaluates one part of the agricultural environment.

Their outputs are then combined through fuzzy reasoning and an optimization layer to rank different crop-allocation scenarios.

The final system provides an explainable recommendation rather than a black-box prediction.

---

## Data

The project uses real Moroccan agricultural datasets stored locally as Excel files.

### Production Vegetale 2010–2022

Used for information such as:

- Crop production
- Cultivated surface
- Crop categories
- Agricultural sectors
- Historical crop yield references

### Indicateurs Sectoriels – Agriculture et Pêche 2010–2020

Used for:

- Precipitation indicators
- Cultivated area indicators
- Agricultural sector context
- Resource-related indicators

The system cleans and restructures the datasets before they are used by the different agents.

---

## Real vs Derived Variables

A key design principle of the project is to distinguish official data from variables generated for the simulation.

### Variables obtained from the source datasets

Examples include:

```text
crop
agricultural sector
production
cultivated surface
precipitation
year
cultivated area
```

### Derived decision variables

The system calculates additional normalized indicators such as:

```text
soil_quality_index_derived
water_availability_index_derived
climate_favorability_index_derived
fertilizer_efficiency_index_derived
resource_balance_index_derived
decision_surface_ha_derived
yield_reference_t_ha_derived
```

These indicators are used only as explainable decision-support variables and are not presented as directly observed agricultural measurements.

---

## Multi-Agent Architecture

The system is divided into specialized agents.

### DataAgent

Responsible for:

- Loading agricultural datasets
- Cleaning data
- Restructuring available columns
- Combining usable agricultural information
- Preparing data for the other agents

### SoilAgent

Evaluates soil suitability and produces a normalized soil score.

### WaterAgent

Evaluates water availability and penalizes crops with high water requirements when resources are limited.

### ClimateAgent

Evaluates climate favorability and crop compatibility with environmental conditions.

### CropAgent

Handles crop-specific characteristics and compatibility.

### FertilizerAgent

Estimates the contribution of fertilizer conditions to crop suitability.

### FarmTypeAgent

Determines an appropriate agricultural strategy such as:

```text
rainfed
irrigated
intensive
mixed
```

### FuzzyLogicAgent

Combines the different environmental scores using interpretable fuzzy rules.

### YieldAgent

Estimates expected crop yield and total expected production.

### OptimizationAgent

Generates and evaluates multiple land-allocation scenarios.

### DecisionAgent

Transforms optimization results into an understandable final recommendation.

### VisualizationAgent

Displays the simulation process and recommendation through an interactive Pygame interface.

### CoordinatorAgent

Orchestrates the complete multi-agent workflow.

---

## System Workflow

```text
Official Agricultural Data
          │
          ▼
      DataAgent
          │
          ▼
 ┌─────────────────────┐
 │ Specialized Agents  │
 ├─────────────────────┤
 │ SoilAgent           │
 │ WaterAgent          │
 │ ClimateAgent        │
 │ CropAgent           │
 │ FertilizerAgent     │
 │ FarmTypeAgent       │
 └─────────────────────┘
          │
          ▼
    FuzzyLogicAgent
          │
          ▼
       YieldAgent
          │
          ▼
   OptimizationAgent
          │
          ▼
      DecisionAgent
          │
          ▼
 Recommended Crop Allocation
```

---

## Fuzzy Logic

Agricultural conditions are rarely completely good or completely bad.

For this reason, the project uses fuzzy reasoning rather than only rigid thresholds.

Variables can belong to categories such as:

```text
Low
Medium
High
```

for characteristics including:

```text
soil quality
water availability
climate favorability
crop compatibility
fertilizer efficiency
```

Example reasoning:

```text
IF water availability is LOW
AND crop water demand is HIGH
THEN crop suitability decreases significantly
```

Another example:

```text
IF soil quality is HIGH
AND climate favorability is HIGH
THEN crop suitability increases
```

This makes the decision process easier to interpret.

---

## Yield Estimation

Expected crop yield is calculated from a historical yield reference combined with moderated environmental factors.

Conceptually:

```text
Expected Yield
      =
Historical Yield Reference
      ×
Environmental Adjustment
```

The adjustment considers factors such as:

- Soil suitability
- Water availability
- Climate
- Fertilizer conditions
- Farm strategy
- Crop compatibility
- Fuzzy suitability

Expected production can then be estimated using:

```text
Expected Production
=
Allocated Surface × Expected Yield
```

---

## Crop Allocation Optimization

The optimizer generates several possible land-allocation scenarios.

Examples include:

```text
100% Crop A

50% Crop A
50% Crop B

70% Crop A
30% Crop B

60% Crop A
40% Crop B
```

When enough crops are available, the system can also evaluate selected three-crop combinations.

Each scenario is scored using several criteria including:

- Expected production
- Expected yield
- Fuzzy suitability
- Resource balance
- Diversification
- Water stress

The scenarios are then ranked from best to worst.

---

## Decision Output

The system selects the highest-ranked scenario and generates an interpretable recommendation.

The recommendation can include:

```text
Recommended crops

Land allocation

Expected yield

Expected production

Fuzzy suitability score

Resource balance

Optimization score
```

This makes it possible to understand both **what the system recommends** and **why it recommends it**.

---

## Interactive Visualization

The project includes a desktop visualization developed with **Pygame**.

The interface displays:

- Multi-agent workflow
- Current simulation stage
- Fuzzy reasoning stage
- Optimization stage
- Recommended crop
- Recommended allocation
- Expected yield
- Expected production
- Resource balance
- Ranked scenarios

This allows the complete decision process to be followed visually.

---

## Generated Results

The simulation automatically generates several output files:

```text
results/
├── merged_agriculture_dataset.csv
├── scenario_results.csv
├── best_allocation_report.txt
├── simulation_summary.json
└── agents_simulation.png
```

These files make it possible to inspect both the processed data and the final optimization results.

---

## Technologies

- Python
- Pandas
- NumPy
- Fuzzy Logic
- Multi-Agent Systems
- Data Analysis
- Scenario Optimization
- Pygame
- Excel Data Processing

---

## Project Structure

```text
.
├── agents/
│   ├── coordinator_agent.py
│   ├── data_agent.py
│   ├── soil_agent.py
│   ├── water_agent.py
│   ├── climate_agent.py
│   ├── crop_agent.py
│   ├── fertilizer_agent.py
│   ├── farm_type_agent.py
│   ├── fuzzy_logic_agent.py
│   ├── yield_agent.py
│   ├── optimization_agent.py
│   ├── decision_agent.py
│   └── visualization_agent.py
│
├── data/
├── results/
├── main.py
├── requirements.txt
└── README.md
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/wassimm22331/Multi-Agent-Agricultural-Optimization-Morocco.git
cd Multi-Agent-Agricultural-Optimization-Morocco
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Project

Place the required Moroccan agricultural Excel files inside:

```text
data/
```

Then run:

```bash
python main.py
```

The system will:

1. Load and preprocess the agricultural data
2. Execute the multi-agent analysis
3. Apply fuzzy reasoning
4. Estimate crop yields
5. Generate crop-allocation scenarios
6. Rank the scenarios
7. Select the best recommendation
8. Launch the visualization
9. Save the results

---

## Limitations

This project is an academic decision-support simulation.

The official datasets contain aggregate agricultural information rather than detailed parcel-level measurements.

Some environmental indicators therefore need to be derived for simulation purposes.

The fuzzy rules are intentionally interpretable and relatively simple.

The optimization component evaluates generated scenarios rather than solving a full continuous agricultural optimization problem.

The results should therefore be considered experimental decision-support outputs rather than real agronomic recommendations.

---

## Future Improvements

Possible extensions include:

- Integration of regional weather APIs
- More detailed soil datasets
- Geographic information
- Larger crop databases
- Historical price information
- Economic profitability optimization
- Machine learning yield prediction
- Reinforcement learning for dynamic crop allocation
- More advanced multi-objective optimization
- Interactive web dashboard
- Regional recommendation maps

---

## What This Project Demonstrates

This project demonstrates practical experience with:

- Multi-Agent System design
- Data preprocessing
- Decision-support systems
- Fuzzy logic
- Mathematical scoring
- Ranking algorithms
- Scenario optimization
- Explainable AI concepts
- Agricultural data analysis
- Modular Python architecture
- Interactive visualization

---

## Author

**Wassim Trachli**

Master's Student in Artificial Intelligence and Connected Objects  
Université Ibn Tofaïl, Morocco

[GitHub](https://github.com/wassimm22331)  
[LinkedIn](https://www.linkedin.com/in/wassim-trachli-12b302318/)
