# Lit Review: 2010, Tagaki - Energy storage of PV using batteries of battery-switch stations

@GenuineLukas 

### Summary

The paper by Takagi explores the concept of utilizing battery switch stations(BSS) for electric vehicles as an innovative solution for managing surplus electricity from photovoltaic(PV) systems. In response to Japan’s ambitious target of reaching 54 million kW in PV capacity by 2030, the authors discuss the challenges of integrating large-scale PV into the power grid, such as voltage rise and surplus electricity. They propose that instead of building costly new storage facilities, existing battery stations for EVs could serve a dual purpose by storing excess electricity. The economic analysis presented suggests that using BSS for surplus power is more cost-effective compared to traditional pumped storage, potentially saving up to 695.7 billion yen annually if the batteries are leased under that amount.

### Statistical and Mathematical Analysis

Here’s a breakdown of the key mathematical and statistical analyses featured in the study.

1. **Optimal Generation Mix Model(OPIGEN):**
    - Objective: Minimize the total cost of the energy system, which includes construction, fuel, and operational costs of power plants.
    - Methodology: Uses linear programming to determine the most cost-effective mix of power generation sources.
    - Variables: Includes variables for the capacity and output of various types of power plants(e.g., nuclear, IGCC, LNG-MACC, and pumped storage).
    
    Since the total cost includes the construction cost, fuel cost, and operational cost of power plants, setting the total cost as an objective function of linear programming enables us to get the most economical construction and operation patterns of the power plants.
    
2. **Charge and Discharge Control Analysis**
    - Control Signal x: This represents a variable that controls the charging and discharging of power based on grid needs.
    - Equations:
        - $\int^{24}_{0}x(t)dt = X$ - Ensures the total control signal over 24 hours equals the preset value X, which is necessary for daily battery switching.
        - $Q_{demand}=P_{MAX} \cdot X$ - Relates the daily charge demand to the maximum charging power and the control signal.
        
        Charge/Discharge Rules: Include setting maximum charging power $P_{MAX}$ and managing the state of charge $SOC(t)$ to ensure batteries meet daily operational needs without exceeding capacity.
        
3. **Economic Evaluation**:
    - **Annual Cost Comparison**: Compares the total annual cost of energy generation using pumped storage versus BSS.
    - **Cost Benefit Analysis**: Calculates potential savings and economic value per kilowatt-hour of battery use, incorporating leasing costs and operational efficiencies.
    - **Formula**: Economic Value per kWh= $\frac{Total Cost Difference}{Battery Capacity}$
        
        Economic Value per kWh=Total Cost DifferenceBattery Capacity
        
    - This formula helps determine the leasing price that would make using BSS economically advantageous over pumped storage.

### Review

Takagi et al, build upon the concept of vehicle-to-grid systems, which involve using electric vehicle(EV) batteries to store and return electricity to the grid. Previous studies have highlighted the potential of V2G in enhancing grid stability and aiding in the integration of renewables (Kempton & Tomic, 2005; Lund & Kempton, 2008). However, the innovation in Takagi et al.'s study lies in the use of BSS, which are typically used solely for speeding up the EV charging process, as a means to also mitigate the effects of PV surplus.

Their methodology involves a comparative economic analysis between two scenarios: one using pumped storage and another using BSS. The study leverages the Optimal Generation Mix Model (OPTIGEN), a linear programming model that aims to minimize energy system costs by optimizing the mix of different power sources, including nuclear, coal, and renewables. The results indicate a clear cost benefit in favor of using BSS over pumped storage, primarily due to lower operational costs and the dual-use capability of BSS.

### **Original Business Model:**

- **Primary Function**: The original business model for BSS primarily focuses on facilitating rapid battery swapping for electric vehicles. This enables EV owners to replace their depleted batteries with fully charged ones in a short time, rather than waiting for their batteries to recharge. The primary revenue stream in this model comes from servicing EV owners who pay for battery swaps.
- **Infrastructure Utilization**: The infrastructure is solely used for automotive purposes, ensuring that EVs have minimal downtime due to battery charging.
- **Operational Scope**: The operations are centered around the transportation sector, specifically catering to the needs of EV users.

### **New Business Model Proposed:**

- **Dual Functionality**: The new business model expands the functionality of BSS to also act as a storage solutions for surplus electricity from PV systems. This is in response to the integration challenges of renewable energy sources like solar power, which can produce excess energy during peak production times that the grid cannot immediately use.
- **Economic Efficiency**: By utilizing BSS as both a service for EV owners and a grid energy storage system, the stations can generate additional revenue from utilities needing to store surplus energy. This dual use optimizes the utilization of the BSS infrastructure.
- **Broadened Market Impact**: While the original model impacts primarily the transportation sector, the new model also engages the energy sector, providing services to utility companies. This engagement helps stabilize the grid and makes renewable energy sources more viable and efficient.
- **Financial Model**: The new model proposes a leasing mechanism where utilities would pay to use the battery capacity of BSS for energy storage. This creates a new revenue stream independent of the transportation services provided to EV owners.

In summary, the new business model not only extends the revenue base of BSS but also contributes to a more robust and sustainable energy landscape by integrating renewable energy solutions with existing transportation infrastructure. This approach leverages existing assets in a novel way, demonstrating an innovative convergence of the transportation and power sectors.

### **Shortcomings and Challenges**

1. **Infrastructure and Investment**: Although BSS can use existing infrastructure, significant upgrades or modifications might be necessary to handle the dual functionality of serving both transport and grid storage needs. This requires upfront investment which might deter quick adoption.
2. **Battery Lifespan and Efficiency**: Frequent charging and discharging of batteries can degrade their capacity over time. The increased cycles from dual usage could accelerate wear and tear, potentially increasing operational costs and reducing the economic attractiveness.
3. **Technology Specificity**: The model's success is highly dependent on the specific technology used for BSS and the types of batteries. Technological advancements in battery technology, such as solid-state batteries, could alter the dynamics of feasibility and cost.
4. **Regulatory and Market Risks**: Regulatory changes, market volatility in energy prices, and shifts in government policy towards renewables and EVs could impact the long-term viability of this model.
5. **Complex Coordination**: The operational complexity of synchronizing the energy needs of the grid with the charging requirements of EVs without causing inconvenience to EV users could pose logistical challenges.
6. **Public Acceptance**: Depending on how the model impacts the speed and convenience of battery swaps for consumers, public acceptance might vary. Any perception of reduced service quality for EV users could hinder adoption.

In summary, while the proposed business model offers innovative use of BSS for energy storage and has clear potential benefits, its widespread adoption will depend on overcoming technological, economic, and regulatory challenges. Careful consideration of the impact on battery life, infrastructure needs, and regulatory environments will be crucial in determining its feasibility and prevalence in the energy and transportation sectors.