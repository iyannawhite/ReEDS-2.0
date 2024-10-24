# Model Documentation
## Overview
ReEDS is a mathematical programming model of the electric power sector. Given a set of input assumptions, ReEDS models the evolution and operation of generation, storage, transmission, and production technologies. 

The model consists of two separate but interrelated modules:
  * Supply module -  this module solves a linear program for the cost-minimizing levels of power sector investment
  * Operation and storage (VRE) module - this module calculates key parameters for assessing the 
  value of VRE generators and storage

The latest, detailed documentation of the ReEDS model can be found in the latest version of the published documentation: [Regional Energy Deployment System (ReEDS) Model Documentation: Version 2020](https://www.nrel.gov/docs/fy21osti/78195.pdf).

Detailed documentation of ReEDS 2.0 input files are available [here](./sources.md)


## Acknowledgments

We gratefully acknowledge the many people whose efforts contributed to
this report. The ReEDS modeling and analysis team at the National
Renewable Energy Laboratory (NREL) was active in developing and testing
the ReEDS model version 2023. We also acknowledge the vast number of
current and past NREL employees on and beyond the ReEDS team who have
participated in data and model development, testing, and analysis. We
are especially grateful to Walter Short who first envisioned and
developed the Wind Deployment System (WinDS) and ReEDS models. We thank
Walter Short, Owen Zinaman, Laura Vimmerstedt, Jeffrey Logan, Cara
Marcy, Gokul Iyer, and Mike Meshek for their comments and improvements
on successive versions of this report. Finally, we are grateful to all
those who helped sponsor ReEDS model development and analysis,
particularly supporters from the U.S. Department of Energy (DOE) but
also others who have funded our work over the years. This report was
funded by the DOE Office of Energy Efficiency and Renewable Energy under
contract number DE-AC36-08GO28308. Any errors or omissions are the sole
responsibility of the authors.


## List of Abbreviations and Acronyms

| Abbreviation/Acronym | | 
| --- | --- |
AC | alternating current
AEO | Annual Energy Outlook
ATB | Annual Technology Baseline
BA | balancing area
BECCS | Bioenergy with Carbon Capture and Storage
CAES | compressed-air energy storage
CAIR | Clean Air Interstate Rule
CC | combined cycle
CCS | carbon capture and sequestration
CES | clean energy standard
CF | capacity factor
CFL | compact fluorescent lamp
CO<sub>2</sub> | carbon dioxide
CO<sub>2</sub>e | carbon dioxide equivalent
CMIP | Coupled Model Intercomparison Project
CPP | Clean Power Plan
CPUC | California Public Utilities Commission
CSAPR | Cross-State Air Pollution Rule
CSP | concentrating solar power
CT | combustion turbine
CV | capacity value
DAC | Direct Air Capture
DC | direct current
DG | distributed generation
DNI | direct normal insolation
DOE | U.S. Department of Energy
DSIRE | Database of State Incentives for Renewables & Efficiency
DUPV | distribution-side utility-scale photovoltaic
EAC | early action credit
EGR | enhanced gas recovery
EGS | enhanced geothermal system
EIA | U.S. Energy Information Administration
ELCC | effective load carrying capability
EMM | Electricity Market Module
EOR | enhanced oil recovery
EPA | U.S. Environmental Protection Agency
ERC | emission rate credit
ERCOT | Electric Reliability Council of Texas
FERC | Federal Energy Regulatory Commission
FOM | fixed operation and maintenance
GCM | general circulation model
GHG | greenhouse gas
GIS | geographic information systems
GW | gigawatt
H2 or H<sub>2</sub> | Hydrogen
HMI | U.S. Bureau of Reclamation Hydropower Modernization Initiative
HSIP | Homeland Security Infrastructure Project
HVDC | high-voltage direct current
IGCC | integrated gasification combined cycle
IOU | investor-owned utility
IPM | U.S. Environmental Protection Agency Integrated Planning Model
IPP | independent power producer
ISO | independent system operator
IRS | Internal Revenue Service
ITC | investment tax credit
JEDI | Jobs and Economic Development Impact model
km<sup>2</sup> | square kilometer
kV | kilovolt
kW | kilowatt
kWh | kilowatt hour
LCOE | levelized cost of energy
LDC | load-duration curve
LED | light-emitting diode
LOLP | loss of load probability
MACRS | Modified Accelerated Cost Recovery System
MATS | Mercury and Air Toxic Standards
MMBtu | million British thermal units
MPI | materials price index
MW | megawatt
MWh | megawatt hour
NaS | sodium-sulfur
NEB | Canadian National Energy Board
NEMS | National Energy Modeling System
NERC | North American Electric Reliability Corporation
NG | natural gas
NHAAP | National Hydropower Asset Assessment Program
NLDC | net load-duration curve
NO<sub>x</sub> | nitrogen oxide
NPD | non-powered dam
NRC | Nuclear Regulatory Commission
NREL | National Renewable Energy Lab
NSD | new stream-reach development
NSRDB | National Solar Radiation Database
O&M | operation and maintenance
OGS | oil-gas steam
PCM | production-cost model
POI | point of interconnection
PRM | planning reserve margin
PRODESEN | Mexican Programa de Desarrollo del Sistema Eléctrico Nacional
PSH | pumped storage hydropower
PTC | production tax credit
PV | photovoltaic
PVB | photovoltaic and battery
RA | resource adequacy
RCP | representative concentration pathway
REC | renewable energy certificate
ReEDS | Regional Energy Deployment System
reV | Renewable Energy Potential tool
RGGI | Regional Greenhouse Gas Initiative
RLDC | residual load-duration curve
RPS | renewable portfolio standard
RROE | rate of return on equity
RTO | regional transmission organization
SAM | System Advisor Model
SENER | Secretaría de Energía for Mexico
SM | solar multiple
SO<sub>2</sub> | sulfur dioxide
T&D | transmission and distribution
TEPPC | Transmission Expansion Planning Policy Committee
tCO<sub>2</sub> | metric ton of carbon dioxide
TW | terawatt
TWh | terawatt hour
UPV | utility-scale photovoltaic
VOM | Variable Operation and Maintenance
VRE | variable renewable energy
WACC | weighted average cost of capital
WECC | Western Electricity Coordination Council
WIND | Wind Integration National Dataset
WinDS | Wind Deployment System


## Introduction

This document describes the structure and key data elements of the
Regional Energy Deployment System model architecture 2.0 (ReEDS 2.0, or
simply ReEDS) version 2023, which is maintained and operated by the
National Renewable Energy Laboratory (NREL).[^ref1] ReEDS 2.0 builds upon
the original ReEDS model architecture (hereafter, Heritage ReEDS),
adding more flexibility and additional capabilities while maintaining
the features that have contributed to the model’s attractiveness as a
decision-support tool. In the past, Heritage ReEDS has been used in
support of both public and private sector clients to analyze the
evolution of the U.S. (and in some cases, North American) power sector
in response to policies and technological change. In this introduction,
we provide a high-level overview of ReEDS 2.0 objectives, capabilities,
and applications. We also briefly describe the history of the Heritage
ReEDS model and discuss major changes introduced by the transition to
ReEDS 2.0. Finally, we provide a short discussion of important caveats
that apply to any ReEDS analysis.

The ReEDS model code and input data can be accessed at
<https://github.com/NREL/ReEDS-2.0>.


### Overview

ReEDS is a mathematical programming model of the electric power sector.
Given a set of input assumptions, ReEDS models the evolution and
operation of generation, storage, transmission, and production[^ref2]
technologies. The results can be used to explore the impacts of a
variety of future technological and policy scenarios on, for example,
economic and environmental outcomes for the entire power sector or for
specific stakeholders. ReEDS employs a modular structure to maximize
user flexibility. Currently, the model consists of two separate but
interrelated modules: a supply module, which solves a linear program for
the cost-minimizing levels of power sector investment; and operation and
a storage (VRE) module,[^ref3] which calculates key parameters for
assessing the value of VRE generators and storage.

Power markets are represented in the model by separating the continent
into model regions, each of which has sources of supply and demand.
Regions are connected by a representation of the transmission network,
which includes existing transmission capacity and endogenous new
capacity. The model represents all existing generating units, planned
future builds, and endogenous new capacity within each region. The model
is intended to solve on the decadal scale, though the time horizon for a
particular model run (and the intervening model solve years) can be
selected by the user. Within each year, a selected representative
timeslices and stress periods are used to characterize seasonal and
diurnal patterns in supply and demand.


### ReEDS History

The ReEDS model heritage traces back to National Renewable Energy
Laboratory’s (NREL’s) seminal electric sector capacity expansion model,
called the Wind Deployment System (WinDS) model. The WinDS model was
developed beginning in 2001 to examine long-term market penetration of
wind in the electric power sector {cite}`shortModelingLongTermMarket2003`. From 2003
to 2008, WinDS was used in a variety of wind-related analyses, including
the production of hydrogen from wind power, the impacts of state-level
policies on wind deployment, the role of plug-in hybrid electric
vehicles in wind markets, the impacts of high wind penetration on U.S
wind manufacturing, the potential for offshore wind, the benefits of
storage to wind power, and the feasibility of producing 20% of U.S.
electricity from wind power by 2030 {cite}`doe20WindEnergy2008`. 
In 2006, a variation of
WinDS was developed to analyze concentrating solar power (CSP) potential
and its response to state and federal incentives. In 2009, WinDS was
recast as ReEDS—a generalized tool for examining the long-term
deployment interactions of multiple technologies in the power sector {cite}`blairRenewableEnergyEfficiency2009`.

Since 2009, ReEDS has been the primary analytical tool in several
studies, including the Hydropower Vision {cite}`u.s.departmentofenergy2016BillionTonReport2016`, Wind Vision {cite}`doeWindVisionNew2015`, SunShot Vision {cite}`doeSunShotVisionStudy2012`, Geothermal Vision {cite}`doeGeoVisionHarnessingHeat2019`, and
Renewable Electricity Futures {cite}`nrelRenewableElectricityFutures2012`. NREL currently uses ReEDS to
publish an annual *Standard Scenarios* report, which provides a U.S.
electric sector outlook under a wide range of possible futures {cite}`cole2020StandardScenarios2020`. ReEDS has also been used to examine impacts of a range of
existing and proposed energy policies {cite:p}`lantzImplicationsPTCExtension2014, maiImpactFederalTax2015, gagnonImpactRetailElectricity2017`. Other recent studies have used ReEDS to
examine the role of natural gas, high renewable scenarios, and other
important issues for the U.S. electricity sector {cite:p}`mignoneCosteffectivenessEconomicIncidence2012, loganNaturalGasScenarios2013, clemmerModelingLowcarbonUS2013, maiEnvisioningRenewableElectricity2014, sullivan2015StandardScenarios2015, coleConsideringRoleSolar2015, coleInteractionsRooftopPV2016, richardsAssessingImpactNuclear2017, coleEnvisioningLowcostSolar2018`. The ReEDS website[^ref4] includes an up-to-date list of publications that use ReEDS.


### Summary of Major Changes

Since the inception of WinDS and ReEDS, NREL has conducted a diverse
suite of analyses. Within each analysis, new capabilities were
developed, thereby improving the sophistication of the model. The
incremental development was often completed by different analysts with
unique intentions and coding preferences. Over time, the model became
increasingly difficult to maintain. Additionally, as the model evolved,
so did the research questions. Therefore, in the fall of 2016, NREL
began to rebuild Heritage ReEDS from the ground up. After three years,
the resulting product was a cleaner, more flexible, and more advanced
tool called ReEDS 2.0. Though ReEDS’ fundamental structure and
functionality have remained constant, ReEDS 2.0 introduces several
changes to the heritage version of the model. The most notable changes
include the following:

- Representative Hours and stress periods

- Hourly ReEDS/Flexible Temporal Resolution

- Decarbonization Scenarios

- Spatial Flexibility?

- Policy Representation (IRA)

- Newer Technology representation

- Transmission (intrazonal, initial capacity, and HVDC macrogrids)

While there are major architectural changes with ReEDS 2.0, many of the
incumbent data and methods supporting ReEDS were updated incrementally.
This documentation describes the data and methods for the 2023 version
of ReEDS. The “Differences from the 2020 Model Version” section of the
appendix summarizes more of the specific changes to made to ReEDS since
the 2020 version.


### Summary of Caveats

Though ReEDS represents many aspects of the U.S. electricity system, it
necessitates simplifications, as all models do. We offer a list of some
important limitations and caveats that result from these
simplifications.

**System-wide optimization:** ReEDS takes a system-wide, least-cost
perspective that does not necessarily reflect the perspectives of
individual decision makers, including specific investors, regional
market participants, or corporate or individual consumers; nor does it
model contractual obligations or noneconomic decisions. In addition,
like other optimization models, ReEDS finds the absolute (deterministic)
least-cost solution that does not fully reflect real distributions or
uncertainties in the parameters; however, the heterogeneity resulting
from the high spatial resolution of ReEDS mitigates this effect to some
degree.

- **Resolution:** Though ReEDS has high spatial, temporal, and process
  resolution for models of its class and scope, it cannot generally
  represent individual units and transmission lines, and it does not
  have the temporal resolution to characterize detailed operating
  behaviors, such as ramp rates and minimum plant runtime. It also does
  not represent all intra-annual time scales, such as weekly or monthly
  trends, as ReEDS intra-annual time slices are designed to characterize
  one day in each season. Many of the time slice shortcomings are
  addressed by using hourly data in VRE modules, but non-VRE generators
  do not get that higher resolution.

- **Foresight and behavior:** Except when running with intertemporal
  optimization, the model has limited foresight, so model
  decision-making does not account for anticipated changes to markets
  and policies. For example, non-intertemporal runs in ReEDS do not
  endogenously model banking and borrowing of credits for carbon,
  renewable, or clean energy policy between solve periods.

- **Project pipeline:** The model incorporates data of planned or
  under-construction projects, but these data likely do not include
  *all* projects in progress.

- **Manufacturing, supply chain, and siting:** The model does not
  explicitly simulate manufacturing, supply chain, or siting and
  permitting processes. Potential bottlenecks or delays in project
  development stages for new generation or transmission are not fully
  reflected in the results. All technologies are assumed to be available
  at their defined capital cost in any quantity up to their technical
  resource potential. Penalties for rapid growth are applied in ReEDS;
  however, these do not fully consider all potential manufacturing or
  deployment limits. Dates associated with cost inputs in the model
  reflect project costs for the commercial operation date but not
  necessarily when equipment is ordered.

- **Financing:** Though the model can use annually varying financing
  parameters to capture near-term market conditions and
  technology-specific financing to account for differences in typical
  investment strategies across technologies, ReEDS cannot fully
  represent differences in project financing terms across markets or
  ownership types and thus does not allow multiple financing options for
  a given technology.

- **Technology learning:** Future technology improvements are considered
  exogenously and thus are not a function of deployment in each
  scenario.

- **Power sector:** ReEDS models only the power sector within its
  defined regional scope (contiguous United States or United States with
  Canada and/or Mexico), and it does not represent the broader U.S. or
  global energy economy. For example, competing uses of resources (e.g.,
  natural gas) across sectors are not dynamically represented in ReEDS,
  and end-use electricity demand is exogenously input into ReEDS.

Notwithstanding these limitations—many of which exist in other similar
tools—the modeling approach considers complex interactions among
numerous policies and technologies while ensuring electric system
reliability requirements are maintained within the resolution and scope
of the model. In doing so, ReEDS can comprehensively estimate the system
cost and value of a wide range of technology options given a set of
assumptions, and we can use the model to generate self-consistent future
deployment portfolios.

A comparison against historical data using ReEDS was completed by Cole
and Vincent {cite:year}`coleHistoricalComparisonCapacity2019` and is useful for providing context for how ReEDS can
perform relative to what actually occurred in historical years.

## Modeling Framework

In this section, we describe the modeling framework underlying ReEDS,
including the modular structure of the model (and how outputs are passed
between modules and convergence is achieved), spatial resolution,
temporal resolution, technology represented, and the model formulations.


### Model Structure

ReEDS combines an optimization module, representing electricity supply,
with a simulation module, which uses a dispatch algorithm and multiple
years of chronological hourly wind, solar, and load data to estimate the
contribution of storage and VRE units to capacity (see [Resource Adequacy](#resource-adequacy)) 
and the level of curtailment for VRE units.

The model can be run sequentially, intertemporally, or using a sliding
window. {numref}`figure-ReEDS-structure` illustrates how the modules
interact when the model is run in sequential solve mode. Within an
iteration, the supply and VRE modules are run in sequence for each model
solve year. For a given model year *t*, the supply module, which has
been provided with a set of inputs dependent on the results from
previous model years, is solved and a subset of the outputs are passed
along to the VRE and storage module. Using these inputs, the module then
calculates the capacity value of VRE and storage, and curtailment rates
for VRE units, which are then applied to the next model year solve
(t+1).[^ref5]

```{figure} ../../images/ReEDS-structure.png
:name: figure-ReEDS-structure

Schematic illustrating the ReEDS structure with a sequential solve
```

When the model is run with sliding window or perfect foresight. 
Each iteration begins with an
execution of the supply module for all model years. The outer cycle (red
arrows) illustrates the order in which the modules are executed:
starting with the supply module followed by the VRE module, after which
the next iteration begins with the supply module. This process is
repeated until convergence. The inner cycles (orange arrows) illustrate
how information is shared by the modules. The types of information
shared by the two modules are the same as for the sequential solve mode.
The major difference is that the supply module passes information for
all model years to the VRE and storage module (and vice versa), and that
an iterative process occurs between the two modules.

Regardless of which foresight mode is chosen, the modular structure
allows each part of the model to be executed independently. However, the
supply and VRE and storage modules are unlikely to be executed without
each other, except for testing purposes. This is because one of the key
strengths of ReEDS resides in its detailed representation of VRE
integration and valuation.


### Model Formulation

The supply module is a linear program that governs the evolution and operation of the
generation and transmission system. This module seeks to minimize power
sector costs as it makes various operational and investment decisions,
subject to a set of constraints on those decisions.

The objective function is a minimization of both capital and operating
costs for the U.S. electric sector, including:

- The net present value of the cost of adding new generation, storage,
  and transmission capacity (including project financing)

- The present value of operating expenses over the evaluation period[^ref6]
  (e.g., expenditures for fuel and operation and maintenance \[O&M\])
  for all installed capacity

- The cost of several categories of ancillary services and storage

- The cost or incentive applied by any policies that directly charge or
  credit generation or capacity

- Penalties for rapid capacity growth as a proxy for manufacturing,
  supply chain, and siting/permitting limitations.

By minimizing these costs and meeting the system constraints (discussed
below), the linear program determines the types of new capacity to
construct in each region during each model year to minimize systemwide
cost. Simultaneously, the linear program determines how generation and
storage capacity should be dispatched to provide the necessary grid
services in each of the selected representative timeslices. The capacity
factor for each dispatchable technology, therefore, is an output of the
model and not an input assumption.

The constraints that govern how ReEDS builds and operates capacity fall
into several main categories:

- **Load Balance Constraints**: Sufficient power must be generated
  within or imported by the transmission system to meet the projected
  load in each of the 134 balancing areas (BAs) in each of the
  representative time-slices. The annual demand and the
  time-slice-specific electricity demand in future years are scaled
  based on load growth inputs.

- **Planning Reserve Constraints**: Each region must have sufficient
  available capacity to meet the forecasted peak demand as well as an
  additional planning reserve margin {cite}`northamericanelectricreliabilitycorporation2021LongTermReliability2021`. Dispatchable technologies
  contribute their full capacity toward planning reserves. For variable
  renewable energy (VRE) technologies, ReEDS uses a load-duration curve
  (LDC) approximation to estimate the effective load-carrying capacity
  of both existing capacity and potential capacity additions to
  determine their contribution to meeting the reserve margin. For
  storage, a chronological simulation using hourly data is used to
  assess its contribution. Planning reserve capacity can also be traded
  between regions if transmission capacity is available.[^ref7]

- **Operating Reserve Constraints:** These constraints ensure enough
  capacity is available to meet unexpected changes in generation and
  load in each reserve-sharing group ([Operational Reliability](#operational-reliability)) and time-slice. ReEDS
  accounts for the following operating reserve requirements: regulation
  reserves, spinning reserves, and flexibility reserves.

- **Generator Operating Constraints:** Technology-specific constraints
  bound the minimum and maximum power production and capacity commitment
  based on physical limitations and assumed average outage rates.

- **Transmission Constraints:** Power transfers among regions are
  constrained by the nominal carrying capacity of transmission corridors
  that connect the regions. Transfers of planning reserves are also
  subject to transmission limits. A detailed description of the
  transmission constraints can be found in [Transmission](#transmission).

- **Resource Constraints:** Many renewable technologies, including wind,
  solar, geothermal, biopower, and hydropower, are spatially
  heterogeneous and constrained by the quantity available at each
  location. Several of the technologies include cost- and
  resource-quality considerations in resource supply curves to account
  for depletion, transmission, and competition effects. The resource
  assessments that seed the supply curves come from various sources;
  these are discussed in [Technology Descriptions](#technology-descriptions), where characteristics of each
  technology are also provided.

- **Emissions Constraints:** ReEDS can limit or cap the emissions from
  fossil-fueled generators for sulfur dioxide (SO<sub>2</sub>), nitrogen
  oxide (NO<sub>x</sub>), and carbon dioxide (CO<sub>2</sub>).
  The emission limit and the emission per megawatt-hour by fuel and
  plant type are inputs to the model. Negative emissions are allowed
  using biomass with carbon capture and storage (BECCS) or direct air
  capture (DAC), and the emission constraint is based on net emissions.
  Emissions can be either capped or taxed, with flexibility for applying
  either. Alternatively, emissions intensities can also be limited to
  certain bounds in ReEDS. The emissions constraints can be applied to
  stack emissions, or can be based on CO<sub>2</sub> equivalent
  emissions, with the later including emissions from upstream methane
  leakage.[^ref8] Methane leakage rates are input by the user.

- **Renewable Portfolio Standards or Clean Electricity Standards:**
  ReEDS can represent renewable portfolio standards (RPSs) and clean
  electricity standards constraints at the national and state levels.
  All renewable generation is considered eligible under a national RPS
  requirement. The renewable generation sources include hydropower,
  wind, CSP, geothermal, PV, and biopower (including the biomass
  fraction of cofiring plants). The eligibility of technologies for
  state RPSs depends on the state’s specific requirements and thus
  varies by state. RPS targets over time are based on an externally
  defined profile. Penalties for noncompliance can be imposed for each
  megawatt-hour shortfall occurring in the country or a given state. In
  the same way, a clean energy standard constraint can be implemented to
  include non-renewable clean energy resources, such as nuclear, fossil
  fuels with carbon capture and sequestration (CCS), or natural gas.


### Spatial Resolution

ReEDS is typically used to study the contiguous United States.[^ref9] 
Within the contiguous United States, ReEDS models capacity
expansion and grid service requirements in 134 model BAs, shown in
{numref}`figure-reeds-regional-structure`. The model BAs are not designed to represent or align perfectly
with real balancing authority areas; they are county aggregates intended
to represent model nodes where electricity supply and demand is
balanced. The model’s synthetic transmission network connects the BAs
and is composed of roughly 300 representative corridors across the three
asynchronous interconnections: the Western Interconnection, the Eastern
Interconnection, and Electric Reliability Council of Texas (ERCOT). The
BAs also respect state boundaries, allowing the model to represent
individual state regulations and incentives. Additional geographical
layers used for defining model characteristics include 3 synchronous
interconnections, 18 model regional transmission operators designed
after existing regional transmission operators, 19 North American
Electric Reliability Corporation (NERC) reliability subregions, 9 census
divisions as defined by the U.S. Census Bureau, and 48 states.[^ref10] The
spatial configuration in the model is flexible, such that the model can
be run at various resolutions (e.g., aggregations of balancing areas),
and data within the model are filtered to only include data for the
regions being modeled in a given scenario.

For more information on the spatial flexibility in the model, see the
“Spatial Resolution Capabilities” section of the appendix.[^ref11]

```{figure} ../../images/reeds-regional-structure.png
:name: figure-reeds-regional-structure

ReEDS regional structure
```

ReEDS includes 134 zones (used for most model decisions), 18
transmission groups (used for grouped-interface flow constraints), 11
planning regions (used by default for representative period selection
and capacity credit calculations), 11 NERC regions (used to define
planning reserve margin constraints), 10 USDA regions (used for
bioenergy supply curves), 9 census divisions (used for fossil gas supply
curves), and 3 synchronous interconnections (used to set the boundaries
for AC transmission expansion).


### Temporal Resolution

- Thematic overview
    - Representative periods
    - 2007-2013; 2012 is default for rep periods while 2007-2013 used for RA
    - Representative period selection
    - Optimized
    - Hierarchical

Many energy system models often solve a full chronological year at
hourly resolution in order to capture the time dependent variability
that pervades increasingly renewable systems. However, high temporal
resolution coupled with high spatial resolution can lead to intractable
optimization problems. For instance, in ReEDS, solving model years in
chronological 4-hour steps is only possible when the model regions are
aggregated and the complexity of the scenario is reduced to eliminate
some constraints. Given the computational challenges, power system
planning models typically forgo full annual temporal resolution and
instead select representative periods to capture variability {cite}`fleischerMinimisingEffectsSpatial2020`. A
common approach as described in the literature {cite:p}`teichgraeberClusteringMethodsFind2019, marcyComparisonTemporalResolution2022, liuHierarchicalClusteringFind2018`
identify these periods uses hierarchical clustering which builds a
hierarchy of clusters based on dissimilarity between sets of
observations in wind capacity factor, solar capacity factor, and demand
time series data. In Reichenberg and Hedenus {cite:year}`Reichenberg2022` the authors demonstrate that hierarchical
clustering is unable to capture regional trends in large systems such as
the United States, motivating an optimization based approach to
determine representative periods in the ReEDS model. The two-step
optimization first weights periods to minimize error in regional
capacity factor and load data over all features (wind capacity factor,
solar capacity factor, and load) and all regions as described by (1).
The error is defined as the difference between the sum of the weighted
regional profiles for wind, solar, and load and the actual regional
profiles over all periods and all regions as described in (2). The
result of this minimization is a selection of representative days
weighted by number of total days in the year.

$$\min \sum_{f,r}^{F,R} E_{1+}(f,r) + E_{1-}(f,r)$$

\(1\)

$$E_{1+}(f,r) + E_{1-}(f,r) = \sum_{p}^{P} W(p)x(p,f,r) - \sum_{p}^{P} x(p,f,r) \quad \forall \ f,r$$

\(2\)

In the second step of the optimization, actual periods are mapped to the
most similar representative period by again minimizing the sum of
absolute error over all periods, features, and regions. The error in
this minimization problem is defined as the difference between the
actual profile for a given actual period, $_{}$,and the representative
profile for the period that actual period is mapped to,
$\left(_{} \right)$. Since each actual period can only be mapped to a
single representative day, the problem is formulated as a mixed integer
linear program as described in (3) and (4).

$$\min [ \sum_{p_a,f,r}^{P,F,R} x(p_a,f,r) - \sum_{p_r}^{P_r} M(p_a,p_r) x(p_r,f,r)]$$

\(3\)

$$\sum_{p_r}^{P_r} M(p_a, p_r) = 1 \quad \forall \ p_a$$

\(4\)

In conjunction, the results of both optimizations lead to a set of
representative periods where the weighting determined in step one
indicates the number of times a representative period will be used over
the course of the year. For example, a representative day weighted by 36
will be used to replace the 36 actual days of the year which are most
similar. Ultimately this optimization-based approach to identify
representative periods helps to reduce the required number of periods
while also capturing regional trends.

- Period resolution: days, 5-day “weeks”, or chronological year

- Timeslice chunks: 4-hour default but can use 1-, 2-, or 3-hour chunks
  for smaller system

- Inter-period linkages

  1.  Diurnal storage cycles within periods

  2.  “Seasonal” storage (currently just H2) level is tracked between
      periods

  3.  Linearized startup costs apply between periods


## Technology Descriptions

This section describes the electricity generating technologies included
in ReEDS. Cost and performance assumptions for these technologies are
not included in this report but are taken directly from the 2023 Annual
Technology Baseline (ATB) {cite}`nrel2023AnnualTechnology2023`.


### Renewable Energy Resources and Technologies

Because renewable energy technologies are a primary focus area of the
ReEDS model, they are characterized in detail. Their characterization
encompasses resource assessments,[^ref12] projected technology
improvements, grid interconnection costs, and operational implications
of integration. Renewable energy technologies modeled include land-based
and offshore wind power, solar PV (both distributed and utility-scale),
CSP with and without thermal storage,[^ref13] hydrothermal geothermal,
near-field enhanced geothermal systems (EGS), deep EGS, run-of-the-river
and traditional hydropower (including upgrades and non-powered dams),
dedicated biomass, cofired biomass, land-fill gas, renewable energy
combustion turbines, and marine hydrokinetic wave technologies. The
input assumptions, data sources, and treatments of these technologies
are discussed in the following sections. Transmission considerations for
renewable energy technologies are discussed in [Interzonal Transmission](#interzonal-transmission).[^ref14]


#### Land-Based Wind

Wind technologies are modeled using representative turbine technologies
by region depending on wind resource quality. Details of the wind
resource data and technology representation can be found in Appendix H
of the Wind Vision study {cite}`doeWindVisionNew2015`. In the current version of ReEDS, we
have relied on the same data sources and approach; however, we extend
the wind resource data to lower-quality wind sites.

The resource assessment for land-based wind uses a resource map of
hourly wind speeds for the United States and offshore areas (for
offshore wind, see [Offshore Wind](#offshore-wind)) and
considers land use exclusions {cite}`lopezLandUseTurbine2021b`. The Reference Access
resource totals more than 7,700 gigawatts (GW), although a Limited
Access and Open Access supply curves are also available.

Individual wind sites are grouped into ten resource classes for ReEDS, 
based on average wind speed ({numref}`land-based-wind-class-def`).[^ref15] The modeling and assessment of individual wind sites
was facilitated using NREL’s Renewable Energy Potential (reV) tool
{cite}`maclaurinRenewableEnergyPotential2021`. The meteorological data for onshore wind are
from the Wind Integration National Dataset (WIND) Toolkit, using
long-term average data for the resource assessment. {numref}`figure-land-based-wind` shows the
land-based wind resource data modeled in ReEDS for all 10 classes, where
the highest average wind speeds belong to class 1 and the lowest to
class 10 {cite}`maiInteractionsWindEnergy2021`. Each class is then further differentiated by
a supply curve for grid interconnection costs in each region. See
[Interzonal Transmission](#interzonal-transmission) for a discussion of interconnection supply curves for
accessing the wind resource.

Distinct wind production profiles are also modeled for each class and
region. In addition, to inform capacity credit and curtailment
calculations, we use hourly production data for each region and class.
Timeslice profiles are based on the 2012 weather year (though this can
be changed by the user), and hourly profiles are from the 2007-2013
weather years.

```{table} Land-Based Wind Class Definitions
:name: land-based-wind-class-def

| Wind Class | Wind Speed Range (m/s) | Potential Wind Plant Capacity (GW) |
|------------|-----------------------:|-----------------------------------:|
|            |                        |                                    |
| 1          |                \> 9.01 |                                106 |
| 2          |            8.77 - 9.01 |                                 91 |
| 3          |            8.57 - 8.77 |                                188 |
| 4          |            8.35 - 8.57 |                                356 |
| 5          |            8.07 - 8.35 |                                684 |
| 6          |            7.62 - 8.07 |                              1,266 |
| 7          |            7.10 - 7.62 |                              1,191 |
| 8          |            6.53 - 7.10 |                              1,159 |
| 9          |            5.90 - 6.53 |                              1,144 |
| 10         |                \< 5.90 |                              1,587 |

```

More information can be found in the NREL Annual Technology Baseline
{cite}`nrel2020AnnualTechnology2020`.

```{figure} ../../images/land-based-wind.png
:name: figure-land-based-wind

Land-based wind resource availability and capacity factor for the three siting scenarios included in ReEDS.
```


#### Offshore Wind

There is substantial diversity in offshore wind generators, in distance
from shore, water depth, and resource quality. ReEDS subdivides offshore
wind potential into fourteen resource classes: seven each for
fixed-bottom and floating turbine designs. Fixed bottom offshore wind
development is limited to resources \< 60 meters \[m\] in depth using
either current-technology monopile foundations (0–30 m); or jacket
(truss-style) foundations (30–60 m). Offshore wind using a floating
anchorage could be developed for greater depths and are assumed the only
feasible technology for development for resource deeper than 60 m.
Within each category, the classes are distinguished by resource quality,
and then supply curves differentiate resource by cost of accessing
transmission in a similar fashion as land-based wind.

Eligible offshore area for wind development includes open water within
the U.S.-exclusive economic zone having a water depth less than 1,000 m,
including the Great Lakes. As with land-based resource, offshore zones
are filtered to remove areas considered unsuitable for development,
including national marine sanctuaries, marine protected areas, wildlife
refuges, shipping and towing lanes, offshore platforms, and ocean
pipelines. The offshore technology selection is made using the Offshore
Wind Cost Model, which selects the most economically feasible technology
for developing a wind resource {cite}`beiterSpatialEconomicCostReductionPathway2016`. More than 4,900
GW of technical offshore wind potential remain after applying the
exclusions.

Current-day cost data are derived from the published data of the global
offshore wind industry as well as estimates from recent development
activity on the Atlantic Coast of the United States {cite:p}`musial2018OffshoreWind2019, nrel2019AnnualTechnology2019`. These data are coupled with engineering assessments and
distance-based cost functions (specific to the offshore export cable and
incremental construction cost associated with moving farther from shore)
to determine expected site-specific costs for technology across a broad
range of water depths and distances from shore {cite}`beiterAssessmentEconomicPotential2017`.
Cost and performance for offshore wind plants are based on assuming a
representative plant size of 600 MW.

Other aspects of our model representations for offshore wind follow the
same methods as those for land-based wind {cite}`lopezLandUseTurbine2021b`. 
{numref}`figure-offshore-wind-resource` shows the offshore wind resource potential
modeled in ReEDS for each of the 14 classes. Classes 1-7 represent fixed-bottom
offshore wind resources with class 1 representing the highest wind speeds. Classes
8-14 represent floating offshore wind resources with class 8 being the
highest wind speeds. The higher speed classes have smaller bin sizes to
capture the highest quality resources with greater resolution.



```{table} Offshore Wind Class Definitions
:name: offshore-wind-class-def

| Wind Class   |     | Wind Speed Range (m/s) | Potential Wind Plant Capacity (GW) |
|--------------|-----|-----------------------:|-----------------------------------:|
| Fixed-Bottom | 1   |                \> 9.98 |                                 24 |
|              | 2   |            9.31 - 9.98 |                                 23 |
|              | 3   |            9.13 - 9.31 |                                 53 |
|              | 4   |            8.85 - 9.13 |                                 97 |
|              | 5   |            7.93 - 8.85 |                                197 |
|              | 6   |            7.07 - 7.93 |                                396 |
|              | 7   |                \< 7.07 |                                445 |
| Floating     | 8   |               \> 10.30 |                                 73 |
|              | 9   |          10.18 - 10.30 |                                 71 |
|              | 10  |          10.01 - 10.18 |                                152 |
|              | 11  |           9.60 - 10.01 |                                293 |
|              | 12  |            8.84 - 9.60 |                                590 |
|              | 13  |            7.43 - 8.84 |                               1189 |
|              | 14  |                \< 7.43 |                               1320 |
```

More information can be found in the NREL Annual Technology Baseline
{cite}`nrel2020AnnualTechnology2020`.

```{figure} ../../images/offshore-wind-resource.png
:name: figure-offshore-wind-resource

Offshore wind resource availability (fixed-bottom and floating) and capacity factor for the contiguous United States
```


#### Solar Photovoltaics

ReEDS differentiates among three solar photovoltaic technologies:
large-scale utility PV (UPV), distribution-side utility-scale PV (DUPV),
and rooftop PV. Investments in UPV and DUPV are evaluated directly in
ReEDS, while rooftop PV deployment and performance are exogenously input
into ReEDS from the dGen model. ReEDS further allows for investment in
hybrid systems comprising coupled UPV and battery technologies (PVB).

UPV in ReEDS represents utility-scale, single-axis-tracking PV systems
with a representative size of 100 megawatts (MW), an array density of 39
MW per square kilometer (km<sup>2</sup>), and an inverter loading ratio
of 1.3. Resource potential is assumed to be located on large parcels
outside urban boundaries, excluding federally protected lands,
inventoried “roadless” areas, U.S. Bureau of Land Management areas of
critical environmental concern, and areas with slope greater than 5%.
Each eligible UPV site is characterized by a raw hourly (8,760)
irradiance profile that is representative of the solar resource within a
10 km<sup>2</sup> contiguous area. Each of these UPV sites are compiled
into supply curves for each of the 134 ReEDS BAs with 9 PV resource
classes, which are further differentiated by cost to connect to the
transmission network (process described in [Interzonal Transmission](#interzonal-transmission)).
The resource classes reflect different
resource qualities based on the annual average global horizontal
irradiance (GHI) reported by the latest National Solar Radiation
Database (NSRDB), assuming a tilt angle equal to the latitude ({numref}`upv-dupv-resource-classes`).
The UPV supply curves input into ReEDS for the conterminous U.S. include
156 terawatts (TW) of potential.

```{table} UPV and DUPV Resource Classes
:name: upv-dupv-resource-classes

|  Class  | GHI (kWh/m^2/day) | Potential UPV Capacity (GW) | Potential DUPV Capacity (GW) |
|---------|-------------------|-----------------------------|------------------------------|
|    1    |          3.0 - 3.5|                          167|                            14|
|    2    |          3.5 - 4.0|                       16,870|                           184|
|    3    |          4.0 - 4.5|                       30,238|                           434|
|    4    |          4.5 - 5.0|                       37,438|                           511|
|    5    |          5.0 - 5.5|                       20,372|                           222|
|    6    |          5.5 - 6.0|                       11,868|                           116|
|    7    |          6.0 - 6.5|                          332|                             4|

```

Investment options along the UPV supply curve can take the form of
either standalone UPV systems or PVB systems. The default PVB technology
represents a loosely DC-coupled system: the PV and battery technologies
share a bi-directional inverter and point of interconnection, and the
battery can charge from either the coupled PV or the grid. The PVB
design characteristics can be user defined for up to three different
configurations, but the default configuration involves an inverter
loading ratio of 2.2 (slightly higher than standalone PV), and a coupled
battery with 4hr duration, whose power-rated capacity is 50% of the
inverter capacity.

The PVB investment option leverages the existing representations of the
independent component technologies, but the cost and performance
characteristics differ from the simple sum of the separate (PV and
battery) parts. For example, the capital costs associated with the fully
integrated PVB hybrid system are reduced based on the cost of a shared
inverter and other balance-of-system components; as a result, the
percentage savings varies by PVB configuration. Improved performance
characteristics are captured through slightly enhanced battery round
trip efficiencies and explicit time series generation profiles; the
latter enables a representation of the PVB system’s ability to divert
otherwise-clipped energy to the coupled battery (during periods where
solar output exceeds the inverter capacity) and avoid curtailment.
Finally, a joint capacity credit results in a greater localized
contribution to resource adequacy, which is comparable overall to the
sum of capacity credits for separate PV and battery systems.

```{figure} ../../images/upv-resource-availability.png 
:name: figure-upv-resource-availabililty

UPV resource availability and DC capacity factor
\[MW<sub>AC</sub><sup>available</sup>/MW<sub>DC</sub><sup>nameplate</sup>\]
for the three siting scenarios included in ReEDS
```

DUPV systems have lower infrastructure requirements than large-scale
rural UPV systems; we assume they connect to existing nearby
distribution substations at about 13 kilovolts (kV), whereas the
representative UPV system connects to a high-voltage bus at 230 kV and
may require a spur line several miles long to reach that connection
point. The cost of the spur line is handled separately in the
accessibility supply curve ([Interzonal transmission](#interzonal-transmission)), but
the additional transformers and power electronics associated with the
larger systems and higher-voltage interconnections add cost and losses
to the UPV systems. On the other hand, the larger UPV systems benefit
from economies of scale. On balance, we assume a per-kW capital cost
penalty of 29%[^ref16] and 5% higher delivered energy (i.e., reduced
losses) for DUPV relative to UPV.

Performance characteristics for UPV and DUPV were developed using NREL’s
reV Tool, using multiyear hourly weather files from the National Solar
Radiation Database[^ref17] at 4-km by 4-km parcels throughout the
contiguous United States from 1998 to 2016. No changes or improvements
in capacity factor over time are assumed for PV technologies. For each
ReEDS BA region, resource quality classifications were made by averaging
across the 1998–2016 period for all available parcels. Hourly generation
profiles were taken from 2007-2013. The generation profiles from 2012
from all the regions in a BA for each resource class were averaged to
provide ReEDS with average capacity factors by time-slice and resource
class.

To mitigate excessive wheeling of distributed PV generation, ReEDS
assumes all power generated by both DUPV and rooftop PV systems is
permitted to be exported to neighboring BAs only when total generation
in the source region exceeds the load for a given time-slice.
UPV-generated electricity, in contrast, can be exported in all
time-slices and regions.

Degradation of the efficiency of solar PV capacity over time is also
modeled at 0.7%/year {cite}`nrel2020AnnualTechnology2020`. This degradation is modeled by reducing the generating capacity of PV by 0.7%/year.

Rooftop PV includes commercial, industrial, and residential systems.
These systems are assumed to have an inverter loading ratio of 1.1. The
Distributed Generation Market Demand model (dGen), a consumer adoption
model for the contiguous U.S. rooftop PV market, is used to develop
future scenarios for rooftop PV capacity, including the capacity
deployed by BA and the pre-curtailment energy production by that
capacity {cite}`sigrinDistributedGenerationMarket2016`. The default dGen trajectories used in
this version of ReEDS are based on the residential and commercial PV
cost projections as described in the 2020 {cite}`nationalrenewableenergylaboratoryAnnualTechnologyBaseline2020`. There are 11
unique rooftop PV trajectories available in ReEDS that are from the 2020
Standard Scenarios report {cite}`cole2020StandardScenarios2020`. These
trajectories were created by running a ReEDS scenario and feeding the
electricity price outputs from ReEDS back into dGen. The trajectories
incorporate existing net metering policy as of spring 2020, and they
include the investment tax credit (ITC) as discussed in [Federal and State Tax Incentives](#federal-and-state-tax-incentives).

Assumptions for each dGen scenario are made consistent with the ReEDS
scenario assumptions as much as is possible. For example, the Tax Credit
Extension scenario also includes an extension of the ITC in dGen, and
the Low PV Cost scenario uses low trajectory from ATB for commercial and
rooftop PV costs.


#### Concentrating Solar Power

Concentrating solar power (CSP) technology options in ReEDS encompass a
subset of possible thermal system configurations, with and without
thermal storage, as shown in {numref}`csp-tech-characteristics`. The various system types access
the same resource potential, which is divided into 3 resource classes
based on direct normal insolation (DNI) ({numref}`csp-solar-resource-classes`). The CSP resource and
technical potential are based on the latest version of NSRDB. Details of
the CSP resource data and technology representation can be found in
Appendix B of Murphy et al. {cite:year}`murphyPotentialRoleConcentrating2019a`. By default, recirculating and dry
cooling systems are allowed for future CSP plants getting built in
ReEDS. CSP cost and performance estimates are a based on an assumed
plant size of 100 MW.

```{table} Characteristics of CSP Technology Options
:name: csp-tech-characteristics

| Storage Duration (hours) | Solar Multiple[^ref18] | Dispatchability | Capacity Credit | Curtailment |
|----|----|----|----|----|
| None | 1.4 | insolation-dependent | Calculated based on hourly insolation | Allowed |
| 6 | 1.0 | dispatchable | Calculated based on storage duration and hourly insolation | Not allowed |
| 8 | 1.3 | dispatchable | Calculated based on storage duration and hourly insolation | Not allowed |
| 10 | 2.4 | dispatchable | Calculated based on storage duration and hourly insolation | Not allowed |
| 14 | 2.7 | dispatchable | Calculated based on storage duration and hourly insolation | Not allowed |

```

The CSP resource classes are defined by power density of DNI,
developable land area having been filtered based on land cover type,
slope, and protected status. CSP resource in each region is therefore
represented as a supply curve of megawatts of solar collector potential,
assuming a power density of 14.9 MW/km.<sup>2</sup> Performance for each
CSP resource class is developed using 2012 hourly resource data
{cite}`senguptaNationalSolarRadiation2018` from representative sites of each region. The
2012 weather files are processed through the CSP modules of the System
Advisor Model (SAM) to develop performance characteristics for each CSP
resource class and representative CSP system considered in ReEDS. CSP
capacity credit calculations are based on hourly profiles from
2007-2013. As with wind and PV technologies, CSP resources are further
distinguished by grid accessibility in each region ([Interzonal Transmission](#interzonal-transmission)).

```{table} Resource Classes for CSP Plants Using a Solar Multiple (SM) of 2.4
:name: csp-solar-resource-classes

|  Resource Class  | DNI (kWh/m^2/day) | Weighted Average Field CF for SM=1 system (%)^a | Available Resource (GW) |
|------------------|-------------------|-------------------------------------------------|-------------------------|
|          Class 1 |           5 - 5.25|                                               17|                    2,641|
|          Class 2 |         5.25 - 5.5|                                               18|                    1,925|
|          Class 3 |         5.5 - 5.75|                                               19|                    1,495|
|          Class 4 |           5.75 - 6|                                               20|                    1,725|
|          Class 5 |           6 - 6.25|                                               21|                    1,850|
|          Class 6 |         6.25 – 6.5|                                               22|                    1,282|
|          Class 7 |         6.5 – 6.75|                                               23|                    1,252|
|          Class 8 |           6.75 – 7|                                               24|                    1,098|
|          Class 9 |           7 – 7.25|                                               26|                    1,381|
|         Class 10 |         7.25 – 7.5|                                               27|                    1,251|
|         Class 11 |         7.5 – 7.75|                                               28|                      677|
|         Class 12 |              >7.75|                                               29|                      114|

```

Resources are then scaled in ReEDS by the ratio of the model-determined
SM and 2.4.

<sup>a</sup> The field capacity factors (CF) shown here are from SAM
(version 2017.09.05, SDK version 181) simulation assuming an SM=1
system. This field capacity factor is meant to represent the upper limit
of corresponding turbine capacity factor for all systems with SM\>1.

The representative CSP system without storage used to define system
performance in ReEDS is a 100-MW trough system with a SM of 1.4. As CSP
systems without storage are non-dispatchable, output capacity factors
are defined directly from SAM results. The average annual capacity
factors for the solar fields of these systems range from 20% (Class 1
resource) to 29% (Class 12 resource).

```{figure} ../../images/csp-resource-availability.png
:name: figure-csp-resource-availability

CSP resource availability and solar field capacity factor for the contiguous United States 
```

The representative system for any new CSP with thermal energy storage is
a tower-based configuration with a molten-salt heat-transfer fluid and a
thermal storage tank between the heliostat array and the steam
turbine.[^ref19] Two CSP with storage configurations are available as shown
in {numref}`csp-tech-characteristics`.

For CSP with storage, plant turbine capacity factors by time-slice are
an output of the model, not an input, as ReEDS can dispatch collected
CSP energy independent of irradiation. Instead, the profile of power
input from the collectors (solar field) of the CSP plants are model
inputs, based on SAM simulations from 2012 weather files.

The capacity credit of CSP with storage is calculated using the same
method as the calculation of the capacity credit of other storage
technologies, except that rather than using net load to show
opportunities to charge, DNI resource is used to show opportunities to
charge the storage. See ["Stress periods” formulation](#stress-periods-formulation) for details.


#### Geothermal

The ReEDS representation of geothermal power was substantial
restructured compared to the prior ReEDS documentation.

The geothermal resource has two distinct subcategories in ReEDS:

- The hydrothermal resource represents potential sites with appropriate
  geological characteristics for the extraction of heat energy. The
  hydrothermal potential included in the base supply curve consists of
  only identified sites, with a separate supply curve representing the
  undiscovered hydrothermal resource.

- EGS sites are geothermal resources that have sufficient temperature
  but lack the natural permeability, in-situ fluids, or both to be
  hydrothermal systems. Developing these sites with water injection
  wells could create engineered geothermal reservoirs appropriate for
  harvesting heat.

EGS is further separated into Near-Field EGS and Deep EGS based upon
proximity to known hydrothermal features. Near-Field EGS represents
additional geothermal resource available near hydrothermal fields
which have been identified. Deep EGS represents available geothermal
resource not tied to existing hydrothermal sites and at depths below
3.5 km.

Geothermal in ReEDS represents a geothermal power production with
representative size up to 100 megawatts electric (MW<sub>e</sub>).
Geothermal resource classes are defined by reservoir temperature
ranges which are closely linked to the cost of a plant normalized by
generation capacity. Energy conversion processes, binary and flash
cycles are linked to reservoir temperature and are specified by
resource class. Plants with reservoir temperatures \< 200 °C (Class
7-10) use a binary cycle, which uses a heat exchanger and secondary
working fluid with a lower boiling point to drive a turbine. All other
reservoir temperatures assume that a turbine is driven directly by
working fluid from the geothermal wells. These assumptions are aligned
with those in ATB 2023.

{numref}`technical-resource-potential` lists the technical resource potential for the different geothermal categories.

```{table} Technical Resource Potential (GW)
:name: technical-resource-potential

| **Resource Class** | Reservoir Temperature **(°C)** | **Hydrothermal** | **Near-Field EGS** | **Deep EGS** |
|:--:|:--:|:--:|:--:|:--:|
|           Class 1  |                         \> 325 |               \- |                0.2 |           \- |
|           Class 2  |                      300 – 325 |              1.8 |                0.2 |           \- |
|           Class 3  |                      275 – 300 |              9.3 |                0.1 |          1.2 |  
|           Class 4  |                      250 – 275 |              0.7 |                0.1 |          8.2 |  
|           Class 5  |                      225 – 250 |              1.1 |                0.1 |           74 |  
|           Class 6  |                      200 – 225 |              2.4 |                0.2 |          320 | 
|           Class 7  |                      175 – 200 |              0.2 |                0.3 |          709 | 
|           Class 8  |                      150 – 175 |              2.6 |                0.3 |          995 | 
|           Class 9  |                      125 – 150 |              1.1 |               0.03 |         1270 | 
|           Class 10 |                         \< 125 |              4.7 |                 \- |           \- | 
|              Total |                                |             23.9 |                1.4 |        3,375 |
```

The default geothermal resource assumptions allow for hydrothermal
sites. Hydrothermal resources have a defined fraction which are
considered identified resources based upon the U.S. Geological Survey’s
2008 geothermal resource assessment. The undiscovered portion of the
hydrothermal resource is limited by a discovery rate defined as part of
the GeoVision Study {cite}`doeGeoVisionHarnessingHeat2019`. The geothermal supply curves are based
on the analysis described by Augustine et al. {cite:year}`augustineGeoVisionAnalysisSupporting2019` and are shown in
{numref}`figure-csp-resource-availability`. The hydrothermal and near-field EGS resource potential is
derived from the U.S. Geological Survey’s 2008 geothermal resource
assessment {cite}`williamsReviewMethodsApplied2008a`, while the deep EGS
resource potential is based on an update of the EGS potential from the
Massachusetts Institute of Technology {cite}`testerFutureGeothermalEnergy2006`. As 
with other technologies, geothermal cost and performance projections are from
the ATB {cite}`nrel2023AnnualTechnology2023`. Alternate resource supply curves can be
incorporated from reV analysis but are currently not part of the default
resource representation. Spurline transmission costs are available when
using reV based supply curves.


#### Hydropower

The existing hydropower fleet representation is informed by historical
performance data. From the nominal hydropower capacity in each BA,
seasonal capacity adjustments are used for Western Electricity
Coordinating Council (WECC) regions based on data from the Transmission
Expansion Planning Policy Committee (TEPPC) 2024 Common Case
{cite:p}`wecc2013InterconnectionwidePlan2013a, weccTEPPCStudyReport2015`. Seasonal capacity adjustments allow more realistic seasonal
variations in maximum capacity due to changes in water availability and
operating constraints. These data are not available for non-WECC
regions. Future energy availability for the existing fleet is defined
seasonally using plant-specific hydropower capacity factors averaged for
2010–2019 as reported by Oak Ridge National Laboratory HydroSource data
(<https://hydrosource.ornl.gov/datasets>). Capacity factors for historical
years are calibrated from the same data source so that modeled
generation matches historical generation. PSH, both existing and new, is
discussed in [Storage Technologies](#storage-technologies). Generally, the
seasonal energy allocation for hydropower must remain in the predefined
season, but ReEDS has the option of allowing a fraction of available
energy to be shifted across seasons, up to 100% of the total.

Three categories of new hydropower resource potential are represented in
the model:

1.  Upgrade and expansion potential for existing hydropower

2.  Potential for powering non-powered dams (NPD)

3.  New stream-reach development potential (NSD).

The supply curves for each are discussed in detail in the Hydropower
Vision report {cite}`doeHydropowerVisionNew2016`, particularly Chapter 3 and Appendix B.

ReEDS does not currently distinguish between different types of
hydropower upgrades, so upgrade potential is nominally represented
generically as a potential for capacity growth that is assumed to have
the same energy production potential per capacity (i.e., capacity
factor) as the corresponding existing hydropower capacity in the region.
An optional representation of hydropower upgrades decouples capacity and
energy upgrades so that the model can choose either type of upgrade
independently. The quantity of available upgrades is derived from a
combination of limited resource assessments and case studies by the U.S.
Bureau of Reclamation Hydropower Modernization Initiative (HMI), U.S.
Army Corps of Engineers (Corps), and NHAAP Hydropower Advancement
Project {cite:p}`montgomeryHydropowerModernizationInitiative2009, bureauofreclamationHydropowerResourceAssessment2011`.
Upgrade availability at federal facilities not included in the
HMI is assumed to be the HMI average of 8% of the rated capacity, and
upgrade availability at non-federal facilities is assumed to be the
NHAAP average of 10% of the rated capacity. Rather than making all
upgrade potential available immediately, upgrade potential is made
available over time at the earlier of either (1) the Federal Energy
Regulatory Commission (FERC) license expiration (if applicable) or (2)
the turbine age reaching 50 years. This feature better reflects
institutional barriers and industry practices surrounding hydropower
facility upgrades. The total upgrade potential from this methodology is
6.9 GW (27 TWh/yr).

```{figure} ../../images/hydro-vision-upgrade-resource-potential.png
:name: figure-hydro-vision-upgrade-resource-potential

Modeled hydropower upgrade resource potential {cite}`doeHydropowerVisionNew2016`
```

NPD resource is derived from the 2012 NHAAP NPD resource assessment
{cite}`kaoNewStreamreachDevelopment2014, hadjeriouaAssessmentEnergyPotential2013`, where the
modeled resource of 5.0 GW (27 TWh/yr) reflects an updated site sizing
methodology, data corrections, and an exclusion of sites under 500 kW to
allow better model resolution for more economic sites.

```{figure} ../../images/hydro-vision-npd-resource-potential.png
:name: figure-hydro-vision-npd-resource-potential

Modeled non-powered dam resource potential {cite}`doeHydropowerVisionNew2016`
```

NSD resource is based on the 2014 NHAAP NSD resource assessment {cite}`kaoNewStreamreachDevelopment2014`, where the modeled resource of 30.7 GW (176 TWh/yr) reflects
the same sizing methodology as NPD and a sub-1 MW site exclusion, again
to improve model resolution for lower-cost resource. The NSD resource
assumes “low head” sites inundating no more than the 100-year flood
plain and excludes sites within areas statutorily barred from
development—national parks, wild and scenic rivers, and wilderness
areas.

```{figure} ../../images/hydro-vision-nsd-resource-potential.png
:name: figure-hydro-vision-nsd-resource-potential

Modeled new stream-reach development resource potential {cite}`doeHydropowerVisionNew2016`
```

The combined hydropower capacity coupled with the costs from the ATB {cite}`nrel2023AnnualTechnology2023` results in the supply curve shown in {numref}`figure-hydro-vision-nsd-resource-potential`.

```{figure} ../../images/hydro-supply-curve.png
:name: figure-hydro-supply-curve

National hydropower supply curve of capital cost versus cumulative capacity potential
```

The hydropower operating parameters and constraints included in ReEDS do
not fully reflect the complex set of operating constraints on hydropower
in the real world. Detailed site-specific considerations involving a
full set of water management challenges are not easily represented in a
model with the scale and scope of ReEDS, but several available
parameters allow a stylized representation of actual hydropower
operating constraints {cite}`stollHydropowerModelingChallenges2017`.

Each hydropower category can be differentiated into “dispatchable” or
“non-dispatchable” capacity, with “dispatchable” defined in ReEDS as the
ability to provide the following services:

1.  Diurnal load following within the capacity and average daily energy limits for each season

2.  Planning (adequacy) reserves with full rated capacity

3.  Operating reserves up to a specified fraction of rated capacity if
    the capacity is not currently being utilized for energy production.

“Non-dispatchable” capacity, on the other hand, provides:

1.  Constant energy output in each season such that all available energy is utilized

2.  Planning reserves equal to the output power for each season

3.  No operating reserves.

Dispatchable capacity is also parameterized by a fractional minimum
load, with the maximum fractional capacity available for operating
reserves as one minus the fractional minimum load. The existing fleet
and its corresponding upgrade potential are differentiated by
dispatchability using data from the Oak Ridge National Laboratory
Existing Hydropower Assets Plant Database
(<https://hydrosource.ornl.gov/dataset/EHA2023>), which classifies plants
by operating mode. Plants with operating modes labeled as Peaking,
Intermediate Peaking, Run-of-River/Upstream Peaking, and
Run-of-River/Peaking are classified as dispatchable in ReEDS, and plants
with other operating modes are classified as non-dispatchable. In total,
47% of existing capacity and 49% of upgrade potential is assumed
non-dispatchable. ReEDS also includes the option to enable hydropower
upgrade pathways where existing non-dispatchable hydropower can be
upgraded to be dispatchable hydropower, or existing dispatchable
hydropower can be upgraded to add pumping and become a pump-back
hydropower facility. A pump-back facility is constrained similarly to a
PSH facility except that input energy can come from natural water
inflows in addition to the grid. These upgrade options can be made
available at a user-specified capital cost. Hydropower upgrades are
unavailable by default because it there is high uncertainty about where
such upgrades are feasible, but these optional features allow users to
explore the potential and value of increasing hydropower fleet
flexibility, which is discussed in detail in  {cite}`cohenAdvancedHydropowerPSH2022`.

The same TEPPC database is used to define region-specific fractional
minimum capacity for dispatchable existing and upgrade hydropower in
WECC. Lacking minimum capacity data for non-WECC regions, 0.5 is chosen
as a reasonable fractional minimum capacity.

Both the NPD and NSD resource assessments implicitly assume inflexible,
run-of-river hydropower, so all NPD and NSD resource potential is
assumed non-dispatchable. Additional site-specific analysis could allow
re-categorizing portions of these resources as dispatchable, but 100%
non-dispatchable remains the default assumption.


#### Biopower

ReEDS can generate electricity from biomass either in dedicated biomass
integrated gasification combined cycle (IGCC) plants or cofired with
coal in facilities that have been retrofitted with an auxiliary fuel
feed. These cofire-ready coal plants can use biomass in place of coal to
supply the fuel for up to 15% of the plant’s electricity generation. A
cofire retrofit costs 305 \$2017/kW based on EIA’s Electricity Market
Module assumptions {cite}`eiaElectricityMarketModule2017a{101}`.

Dedicated and cofired plants source feedstock from the same biomass
supply curves, which are derived from the Oak Ridge National
Laboratory’s *2016 Billion-Ton Report* {cite}`u.s.departmentofenergy2016BillionTonReport2016`.
Data from this report includes estimates of biomass feedstock costs and
total resource availability. Only woody biomass resources are allowed to
be used for biopower plants. No other resource constraints are applied
for nonrenewable energy technologies.

{numref}`figure-biomass-supply-curve-regions` illustrates the resource map and total supply curve by region
as derived from the *2016 Billion-Ton Report* and used in ReEDS.
Nationally, approximately 116 million dry tons of woody biomass are
assumed to be available to the power sector. In addition to the supply
curve price (which represents the cost of the resource in the field),
ReEDS also assumes costs of \$15 per dry ton for collection and
harvesting, as well as an additional \$15 per dry ton for transport, as
based on estimates from a 2014 INL study {cite}`jacobsonFeedstockConversionSupply2014`.
Pathways with more limited biomass model the impact of a halving of the
available resource and a doubling of collection, harvesting, and
transport costs (58 million dry tons and \$60 per ton), whereas the
enhanced resource scenario models the opposite (doubling the available
resource to 232 million dry tons and halving collection, harvesting, and
transport costs to \$15 per ton).

```{figure} ../../images/biomass-supply-curve-regions.png
:name: figure-biomass-supply-curve-regions

Depiction of the regions used for the biomass supply curves (map, top left), based on U.S. Department of Agriculture regional divisions. The line plots to the right indicate the woody biomass supply curves for each region as used in ReEDS, as derived from data in 2016 Billion-Ton Report. The bottom-left plot summarizes the total national supply curve.
```

Because the model assumes zero lifecycle emissions for biomass,
generation sources that use biomass with carbon capture and storage
(BECCS) are assumed to be negative emissions. {numref}`beccs-assumptions` summarizes cost
and performance assumptions for BECCS plants. The uncontrolled emissions
rate of woody biomass fuel is assumed to be 88.5 kg/MMBtu {cite}`bainBiopowerTechnicalAssessment2003`;
after accounting for the heat rate of a BECCS plant and a 90% CCS
capture rate, the negative emissions are approximately -1.22 to -1.11
tonnes/MWh of generation. Fuel consumed in BECCS plants is counted
against the total biomass supply curve described above.

```{table} Cost and Performance Assumptions for BECCS
:name: beccs-assumptions

| BECCS | Capital Cost (\$/kW) | Variable O&M (\$/kWh) | Fixed O&M (\$/kW-yr) | Heat Rate (MMBtu/MWh) | Emissions Rate (tonnes CO<sub>2</sub>/MWh) |
|----|:--:|:--:|:--:|:--:|:--:|
| 2020 | 5,580 | 16.6 | 162 | 15.295 | -1.22 |
| 2035 | 5,333 | 16.6 | 162 | 14.554 | -1.16 |
| 2050 | 5,100 | 16.6 | 162 | 13.861 | -1.11 |
```

#### Marine Hydrokinetic Wave

ReEDS does have a representation of marine hydrokinetic wave
technologies, but this capability is not utilized in any of the recent
or current ReEDS modeling work.


### Conventional Energy Technologies

ReEDS includes all major categories of conventional generation
technologies within its operating fleet or its investment choices. In
the context of ReEDS, “conventional” is defined as thermal generating
technologies driven by coal, gas, oil, or nuclear fuel. Coal
technologies are subdivided into pulverized and gasified (IGCC)
categories, with the pulverized plants further distinguished by 1)
whether SO<sub>2</sub> scrubbers are installed and 2) their vintage[^ref20]
as pre- or post-1995. Pulverized coal plants have the option of adding a
second fuel feed for biomass. New coal plants can be added with or
without CCS technology. Existing coal units built after 1995 with
SO<sub>2</sub> scrubbers installed also have the option of retrofitting
CCS capability.

Natural gas generators are categorized as combustion turbine (CT),
combined cycle (CC), or gas-CC with CCS.[^ref21] There are also nuclear
(steam) generators, landfill gas generators,[^ref22] and oil/gas steam
generators, though the latter two are not offered as options for new
construction besides those that are already under construction. The
model distinguishes each conventional-generating technology by costs,
efficiency, and operational constraints.

Where renewable energy technologies have many unique characteristics,
ReEDS conventional technologies are characterized more generally by the
following parameters:

- Capital cost (\$/MW)

- Fixed and variable operating costs (dollars per megawatt-hour
  \[\$/MWh\])

- Fuel costs (dollars per million British thermal units
  \[\$/MMBtu\])

- Heat rate (MMBtu/MWh)

- Construction period (years) and expenses

- Equipment lifetime (years)

- Financing costs (such as interest rate, loan period, debt fraction,
  and debt-service-coverage ratio)

- Tax credits (investment or production)

- Minimum turndown ratio (%)

- Ramp rate (fraction per minute)

- Planned and unplanned outage rates (%).

Cost and performance assumptions for all new conventional technologies
are taken from the ATB {cite}`nrel2023AnnualTechnology2023`. Regional variations and adjustments
are included and described in [Hydrogen](#hydrogen). Fixed operation and
maintenance costs for coal and nuclear plants increase over time with
the plants age. These escalation factors are taken from the
AEO2023.

In addition to the performance parameters listed above, technologies
are differentiated by their ability to provide operating reserves. In
general, natural gas plants, especially combustion turbines, are better
suited for ramping and reserve provision, while coal and nuclear plants
are typically designed for steady operation. See [Operational Reliability](#operational-reliability) for more
details.

The existing fleet of generators in ReEDS is taken from the NEMS unit
database from AEO2023 {cite}`eiaAnnualEnergyOutlook2023`, with data supplemented from the June
2023 EIA 860M. In particular, ReEDS uses the net summer capacity, net
winter capacity,[^ref23] location, heat rate, variable O&M, and fixed O&M
to characterize the existing fleet. ReEDS uses a modified “average” heat
rate for any builds occurring after 2010: a small, technology-specific
increase on the full-load heat rate is applied to accommodate for units
not always operating at their design point. The modifiers, shown in
{numref}`heat-rate-adjustments`, are based on the relationship between the reported heat rate
the ATB, and the actual observed heat rate, calculated on a fleet-wide
basis for each fuel type.

```{table} Multipliers Applied to Full-Load Heat Rates to Approximate Actual Observed Heat Rates
:name: heat-rate-adjustments 

| **Technology** | **Adjustment Factor** |
|----|:--:|
| Coal (all) | 1.066 |
| Gas-CC | 1.076 |
| Gas-CT | 1.039 |
| OGS | 0.875 |
```

Emissions rates from conventional plants are a function of the fuel
emission rate and the plant heat rate. Burner-tip emissions rates are
shown in {numref}`emissions-rate-by-generator-type`. Because ReEDS does not differentiate coal fuel types,
the coal CO<sub>2</sub> emissions rate in the model is the average of
the bituminous and subbituminous emissions
rate.[^ref24]

```{table} Emissions Rate by Generator Type in Pounds per MMBtu <sup>a</sup> <sup>b</sup>
:name: emissions-rate-by-generator-type

|  Generator  | SO<sub>2</sub> Emissions Rate | NO<sub>x</sub> Emissions Rate | CO<sub>2</sub> Emissions Rate |
|-------------|-------------------------------|-------------------------------|-------------------------------|
|  Hydropower |                           0.0 |                           0.0 |                           0.0 |
|      Gas-CT |                        0.0098 |                          0.15 |                        117.00 |
|      Gas-CC |                        0.0033 |                          0.02 |                        117.00 |
|  Gas-CC-CCS |                        0.0033 |                          0.02 |                         11.70 |
| Pulverized Coal with Scrubbers (pre-1995) | 0.2 |                      0.19 |                        210.55 |
| Pulverized Coal with Scrubbers (post-1995) | 0.1 |                     0.08 |                        210.55 |
| Pulverized Coal without Scrubbers |    1.11 |                          0.19 |                        210.55 |
|   IGCC Coal |                        0.0555 |                         0.085 |                        210.55 |
|    Coal-CCS |                        0.0555 |                         0.085 |                         21.06 |
| Oil/Gas Steam |                       0.299 |                        0.1723 |                        137.00 |
|     Nuclear |                           0.0 |                           0.0 |                           0.0 |
|  Geothermal |                           0.0 |                           0.0 |                           0.0 |
|    Biopower |                          0.08 |                           0.0 |                           0.0 |

```
> <sup>a</sup> {cite}`epaEGRID2007Version1Year2008`

> <sup>b</sup> The assumed CO<sub>2</sub> pollutant rate for land-fill
> gas is zero, so ReEDS does not see the emissions benefits of land-fill
> gas. However, ReEDS can track land-fill gas emissions and the
> associated benefits as a post-processing calculation. Land-fill gas is
> assumed to have negative effective carbon emissions because the
> methane gas would be flared otherwise, thereby it produces the less
> potent greenhouse gas.

Not all parameter data are given in this document. For those values not
included here, see the NREL ATB {cite}`nrel2023AnnualTechnology2023`, or see the values in the
ReEDS repository.[^ref25]. Financing parameters and calculations are
discussed in [Capital Financing, System Costs, and Economic Metrics](#capital-financing-system-costs-and-economicmetrics).


### Storage Technologies

ReEDS includes three utility-scale energy storage options[^ref26]: PSH,
batteries, and CAES. All three storage options are capable of load
shifting (arbitrage), providing planning and operating reserves, and
reducing curtailment of VRE. By default, load shifting can be done only
within a season’s representative day, but ReEDS has options to allow
load shifting across representative days while requiring a specified
fraction of charging energy to be deployed as generation in that day.
Generally, load shifting is accomplished by charging the reservoir
during inexpensive low-demand time-slices and discharging at peak times.
The nameplate capacity of storage can contribute toward planning
reserves (though at a potentially reduced rate, see [Network reinforcement](#network-reinforcement)), and
capacity not being used for charge or discharging can be utilized to
provide any of the operating reserves products represented in ReEDS (see
[Electricity System Operation and Reliability](#electricity-system-operation-and-reliability) 
on how reserves are differentiated in ReEDS). An energy
penalty is associated with storage to provide regulation reserves that
reflect losses due to charging and discharging. Storage is also required
to have sufficient charge to provide operating reserves in addition to
any charge already required for generation in appropriate timeslice.
Batteries are represented with durations of 2, 4, 6, 8, and 10 hours,
CAES is assumed to have a duration of 12 hours, and the PSH storage
duration is either 8, 10, or 12 hours depending on the chosen PSH supply
curve.

The ReEDS framework also allows for standalone thermal energy storage,
though this technology is inactive by default because its site-specific
nature makes it difficult to include in a nationwide optimization
framework. This technology is representative of chilled water and ice
storage units in buildings where, during the summer, cold water or ice
is produced during cooler hours when loads are lower and used to replace
or supplement the air conditioning during the warmer hours. Only units
for commercial buildings are considered. A supply curve for thermal
energy storage units was developed at the NERC subregions level. The
model restricts the use of thermal energy storage devices by the
regional cooling load profile, with power delivered from thermal energy
storage available only during times of high cooling load (e.g., summer
afternoons). Thermal energy storage technologies can contribute to
operating and planning reserves and reduce
curtailment.

Although storage is neither directly linked nor assumed co-located with
renewable energy technologies in ReEDS, it can play an important role in
reducing curtailed electricity from variable generation resources by
charging during time-slices with excess renewable generation. The
ability of storage to reduce curtailment is calculated endogenously.

Existing PSH totals 22 GW, and ReEDS includes the existing CAES
facility in Alabama. New PSH and CAES are location-restricted due to
hydrology and topography (for PSH) and geology (for CAES). There is also
an option to require new PSH to purchase water access from water supply
curves in order to fill new PSH reservoirs, and this constraint can add
cost and further restrict PSH deployment. In contrast, utility-scale
batteries are not restricted to any subset of
regions.

New PSH potential is derived from a national PSH resource assessment
described in Rosenlieb and Cohen 2022 and at
<https://www.nrel.gov/gis/psh-supply-curves.html>. Several PSH supply
curves are available in ReEDS, including alternative storage durations
(8, 10, or 12 hours) and alternative environmental site exclusions,
specifically whether or not new PSH reservoir construction can occur
where there are ephemeral streams as defined by the National Hydrography
Dataset. The PSH resource assessment includes site-level capital costs
calculated from a parametric model that incorporates dam, reservoir, and
other site characteristics. PSH fixed O&M costs and round-trip
efficiency are taken from Mongird et al., 2020, and PSH cost and
resource assumptions are also documented on the NREL ATB website
(www.atb.nrel.gov).

CAES site development costs are estimated based on the underground
geology, where domal salt is the least costly resource at \$1170/kW
(22.6 GW available), bedded salt is the next most costly resource at
\$1,420/kW (37.0 GW), and aquifers (porous rock) are the most costly
resource at \$1,680/kW (61.6 GW) {cite:p}`blackveatchCostPerformanceData2012b, lazardLazardLevelizedCost2016`.
[^ref27] CAES requires a natural gas fuel input when supplying power
output, and its heat rate is assumed to be 4.91 MMBtu/MWh. This
additional fuel input (to the electrical power input during compression)
results in a round-trip efficiency of 125%.

Battery cost and performance assumptions are based on lithium-ion
battery systems, with costs taken from Cole and Frazier {cite:year}`coleCostProjectionsUtilityScale2020`. Low, mid, and high cost projections are available and scale with the
user-defined battery duration. In contrast to all other generator
technologies in ReEDS which have lifetimes that meet or exceed typical
model evaluation windows for book life, the battery is assumed to last
15 years. As a result, its capital cost is uprated by the ratio of a
15-year evaluation window and the evaluation window used by the run. The
batteries are assumed to have a round-trip efficiency of 85%. The
contribution of storage toward the reserve margin requirement is
discussed in [Resource Adequacy](#resource-adequacy). Battery storage has a representative size of
60 MW. Finally, we apply a minimum VOM of \$0.01/MWh (in 2004\$) to all
storage to avoid degeneracy with renewable energy
curtailment.


### Hydrogen

ReEDS has the capability of modeling the use of hydrogen, both as a
form of seasonal storage to meet power system requirements and as a
clean fuel produced by the power sector for use in other
sectors.

In the power sector, hydrogen can be consumed as a fuel in Hydrogen
Combustion Turbines (H2-CTs). H2-CTs are comparable to commercial gas
turbines but can be fired with hydrogen {cite:p}`mitsubishiIntermountainPowerAgency2020, ruthTechnicalEconomicPotential2020`. 
H2-CTs are assumed to have the same heat rate and operation and
maintenance (O&M) cost as regular gas-fired combustion turbines (see
[Conventional Energy Technologies](#conventional-energy-technologies)) but with a 20% higher overnight capital cost, slightly
higher than the 10% value reported by Ruth et al. {cite:year}`ruthTechnicalEconomicPotential2020` in order to
allow the H2-CT to be clutched and act as a synchronous generator.
Existing gas generators can be upgraded to this H2-CT technology by
paying the 20% difference in capital cost between the two
generators.

Power sector hydrogen use is determined by the model’s optimization; as
with natural gas plants and other fuel-based generators, weighs the
costs of investment in H2-CTs and procuring hydrogen against other
options for serving load and meeting other power system constraints. In
contrast, demand for hydrogen produced by the power sector but used
externally in other sectors is specifically exogenously as an input.
This demand is intended to capture hydrogen used in sector such as
transportation or industry and can be specified in terms of a total
national hydrogen by year.

The model includes a range of options for representing the production,
transport and storage or hydrogen, as well as the spatial resolution of
at which hydrogen demand is serviced. These options include: (1) as a
drop-in renewable fuel with a fixed price, (2) endogenous representation
of production with national balancing, and (3) endogenous representation
of production with zonal balancing. Each of these representations is
discussed in more detail below.


#### Drop-in renewable fuel

The first approach models hydrogen as a drop-in renewable fuel that is
available in unlimited quantity at a fixed price (\$/MMBtu). The default
fuel costs for this approach are assumed to be \$20/MMBtu, which is
consistent with estimates of the costs for hydrogen produced using an
electrolyzer powered by dedicated wind or PV; for example, Mahone et al.
{cite:year}`mahoneHydrogenOpportunitiesLowCarbon2020` report a range of \$7–35/MMBtu. This estimate also falls within
the range of current ethanol (\$12/MMBtu) and biodiesel (\$30/MMBtu)
prices {cite}`doeAlternativeFuelPrice2020`. It is also consistent with Hargreaves and Jones
{cite:year}`hargreavesLongTermEnergy2020` which reports \$20/MMBtu for carbon-neutral biogas. As this is
the only hydrogen cost modeled with this approach, this fuel cost
represents an “all-in” cost that includes the cost of production,
delivery, and storage of hydrogen. Users can specify different
trajectories for fuel costs over time.

Under the drop-in renewable fuel approach, the use of curtailed
renewable energy for H2-CT fuel production is not explicitly considered;
to capture this dynamic the production of hydrogen must be endogenously
modeled in ReEDS, which is described in the next section.


#### Endogenous production with national balancing

In this approach hydrogen production is explicitly represented via two
pathways: electrolysis and steam methane reforming (SMR). For either
pathway, ReEDS must invest in sufficient electrolyzer or SMR capacity to
meet hydrogen demands. {numref}`hydrogen-production-assumptions-a`, {numref}`hydrogen-production-assumptions-b`, 
and {numref}`hydrogen-production-assumptions-c` summarize the cost and performance data
on the hydrogen production technologies represented in ReEDS.

```{table} Cost and Performance Assumptions for Hydrogen Production Technologies. Costs are reported in \$2022.
:name: hydrogen-production-assumptions-a

| Electrolyzer | Capital Cost (\$/kW) | Variable O&M<sup>a</sup> (\$/kWh) | Fixed O&M (\$/kW-yr) | Electricity Use (kWh/kg) | Natural Gas Use (MMBtu/kg) |
|:--:|:--:|:--:|:--:|:--:|:--:|
| 2020 | 1,750 | 0 | 101.9 | 56.1 | -- |
| 2035 | 550 | 0 | 32.0 | 53.8 | -- |
| 2050 | 550 | 0 | 25.0 | 51.5 | -- |

```

```{table} Cost and Performance Assumptions for Hydrogen Production Technologies. Costs are reported in \$2022.
:name: hydrogen-production-assumptions-b
| SMR | Capital Cost (\$/kg/day) | Variable O&M (\$/kg) | Fixed O&M (\$/kg/day-yr) | Electricity Use (kWh/kg) | Natural Gas Use (MMBtu/kg) |
|:--:|:--:|:--:|:--:|:--:|:--:|
| 2020 | 649 | 0.087 | 20.9 | 0.88 | 0.192 |
| 2035 | 634 | 0.087 | 20.4 | 0.88 | 0.192 |
| 2050 | 622 | 0.087 | 20.0 | 0.88 | 0.192 |
```

```{table} Cost and Performance Assumptions for Hydrogen Production Technologies. Costs are reported in \$2022.
:name: hydrogen-production-assumptions-c

| SMR-CCS | Capital Cost (\$/kg/day) | Variable O&M (\$/kg) | Fixed O&M (\$/kg/day-yr) | Electricity Use (kWh/kg) | Natural Gas Use (MMBtu/kg) |
|:--:|:--:|:--:|:--:|:--:|:--:|
| 2020 | 1,408 | 0.089 | 45.3 | 1.9 | 0.192 |
| 2035 | 1,239 | 0.089 | 39.8 | 1.9 | 0.192 |
| 2050 | 1,239 | 0.089 | 39.8 | 1.9 | 0.192 |

```

<sup>a</sup> operation and maintenance

Under this representation of hydrogen, ReEDS ensures sufficient
hydrogen production to match total annual demand at a national level.
This means that hydrogen demand from H2-CTs and external sources is
represented on an annual basis, and that hydrogen can be produced in any
location or time period in the model to serve that demand. Users have
the option to apply an adder to the production of hydrogen to represent
additional costs of transporting and storing hydrogen, but these are not
explicitly represented in this formulation.



#### Endogenous production with zonal balancing, transport, and storage

In this approach hydrogen production is explicitly represented, but
instead of matching hydrogen supply and demand at the national level is
matched zonally in each of the model’s balancing areas. The equation
below reflects how for each region *r* in each time period *h* the model
balances hydrogen supply, which includes production (Prod), storage
withdrawals (StorOut), and transfers from neighboring regions *rr*
(Flow), with hydrogen demand, including storage injections (StorIn),
transfers to neighboring regions, and demand from H2CTs and other
sectors.

$$Prod_(h,r) + StorOut_(h,r) + \sum_(rr) Flow_(h,rr,r) \\
= StorIn_(h,r) + \sum_(rr) Flow_(h,rr,r) + H2CT_(h,r) + Exog_(h,r)$$

Hydrogen demand from the power sector is attributed to balancing area
based on H2-CTs usage, whereas exogenous hydrogen demand is allocated to
balancing using regional demand fractions.

To store hydrogen a balancing area must invest in storage capacity.
ReEDS currently represents two forms of geological hydrogen
storage—either in salt caverns or hard rock formations—as well as the
ability to construct storage in underground pipe systems. Data on the
availability of geological storage are taken from , depicted in {numref}`figure-hydrogen-storage-availability`. 
Because of the lack of credible estimates on available reservoir
capacity, ReEDS does not impose limits on the amount of storage that a
balancing area connected to reservoir can
build.

Costs of hydrogen storage are based on estimates from , shown in {numref}`figure-hydrogen-storage-cost-estimate`. 
For geological storage ReEDS assumes \$/kg based on the
economies-of-scale from constructing 2-3 caverns. To reduce model
complexity, ReEDS assumes that each balancing area can only build the
cheapest storage option that it has available to
it.

ReEDS also allows for the modeling of interzonal hydrogen transport.
Transport requires the construction of hydrogen pipelines, and the model
assumes costs estimates based on from the H2 SERA model[^ref28]. Modeling
hydrogen transport in ReEDS is an experimental feature, and because this
feature adds significant runtime the model includes the option for
modeling zonal balancing with transport disabled or a fixed \$/kg
hydrogen transport cost.

```{figure} ../../images/hydrogen-storage-availability.png
:name: figure-hydrogen-storage-availability

Assumed availability of geological hydrogen storage
reservoirs. Data are from Lord et al. {cite:year}`lordGeologicStorageHydrogen2014a`.
```

```{figure} ../../images/hydrogen-storage-cost-estimate.png
:name: figure-hydrogen-storage-cost-estimate

Cost estimates for hydrogen storage. Data taken from Papadias and Ahluwalia {cite:year}`papadiasBulkStorageHydrogen2021`.
```


### Direct Air Capture

The model can also procure negative emissions by removing and storing
CO<sub>2</sub> from the atmosphere using direct air capture (DAC). For
this study, DAC in the ReEDS model is a sorbent design that uses only
electricity as an input, with an energy consumption of 3.72 MWh per
tonne of CO<sub>2</sub> removed. Overnight capital costs are assumed to
be \$1,932 per tonne-year capture capacity, with annual fixed O&M costs
of 4.6% of the capital costs and nonfuel variable O&M cost of \$21 per
tonne.


### CO2 Transport and Storage

ReEDS has the option to use a detailed CO2 network representation that,
when turned on, requires all CO2 captured at CCS facilities (gen-CCS,
SMR-CCS, and DAC) to be transported via liquid CO2 pipelines and
sequestered in underground saline aquifers. "Trunk" pipelines can be
built between BA transmission endpoints and "spur" pipelines can be
build from BA transmission endpoints to the edge of any nearby (\<200
mi) aquifer. These pipelines can be assigned different capital and FO&M
costs, and the several hundred saline aquifers identified by NETL have
\$/tonne breakeven costs that represent the cost of sequestering CO2 in
the aquifer (i.e. permitting, injection facilities, monitoring, and a
100-year trust fund for maintenance).

The network representation includes only saline aquifers with a
reservoir cost of \<\$20/tonne at a 90% capacity factor. The explicit
representation is turned off by default.


### Capital Stock
#### Initial Capital Stock, Prescribed Builds, and Restrictions

Existing electricity generation capacity is taken from the EIA NEMS
unit database {cite}`eiaAnnualEnergyOutlook2023`. Units are mapped to ReEDS technologies based
on a combination of fuel source and prime mover of the generation
technology. Units of the same technology type within a region can be
aggregated or represented individually.[^ref29] If they are aggregated, the
aggregation is done by clustering the units based on heat
rates.

The binning structure is designed flexibly such that users can choose
the appropriate levels of model fidelity and computational speed for
each application. Historical units are binned using a k-means clustering
algorithm for each BA and technology category (e.g., coal with or
without SO<sub>2</sub> scrubbers, and natural gas combined cycle)
combination. The user specifies a maximum number of bins and a minimum
deviation across unit heat rates. Any two plants are eligible to form
separate bins if the difference between their heat rates is greater than
the minimum deviation parameter. The number of bins formed is then equal
to the smaller of the maximum bin number parameter and the number of
units after applying the minimum deviation criteria. For each bin, the
assigned heat rate is equal to the capacity-weighted average of the heat
rates for the units inside the bin. An illustrative example of the
results is depicted for two BAs in {numref}`figure-capacity-binning-example`, assuming a maximum of
seven bins and minimum deviation of 50 BTU per kWh. The horizontal axis
corresponds to the heat rate for a given power plant unit from the NEMS
database, while the vertical axis corresponds to the heat rate each bin
is assigned in ReEDS. Points on the 45-degree line illustrate units for
which the ReEDS heat rate is the same as the NEMS heat rate. The more
tightly clustered the points are around this line, the less the model
will suffer from aggregation bias. The figure illustrates that, in
general, the fewer the number of units in a given technology category
(in this example, nuclear and scrubbed coal), the closer the binned heat
rates are to the actual heat rates.

```{figure} ../../images/capacity-binning-example.png
:name: figure-capacity-binning-example

Example of capacity binning results for two BAs
```

Hydropower has additional subcategories to differentiate
dispatchability as discussed in [Hydropower](#hydropower). In addition, any plants
that are listed as under construction become prescribed builds. In other
words, ReEDS builds any under-construction units, with the units coming
online in the anticipated online year listed in
the database.

For wind technologies, near-term regional growth restrictions reflect
the difficulty of immediately scaling the wind industry. Specifically,
wind plant construction through the 2020 solve year is limited to plants
that are planned to be installed before the end of 2020. After 2020, no
wind capacity limits are implemented.


#### Retirements

Renewable energy generator and battery retirements are (by
default)[^ref30] based on assumed lifetimes. Once a generator has reached
its lifetime, it is retired. Renewable energy and battery lifetime
assumptions are shown in {numref}`generator-and-battery-lifetimes`.
When renewable energy capacity is retired, the resource
associated with that capacity is made available, and ReEDS can choose to
rebuild a renewable energy generator using the newly available resource,
without the need to rebuild the grid interconnection infrastructure. A
consequence of this assumption is that retired renewable capacity can be
replaced without incurring interconnection costs and, with all other
considerations being equal, re-powered or re-built renewable capacity
has lower cost than new “green-field” capacity of the same type.[^ref31]
One exception to this procedure is hydropower, which due to assumed
non-power requirements is never retired unless there is an announced
hydropower capacity retirement listed in the NEMS unit
database.

```{table} Lifetimes of Renewable Energy Generators and Batteries
:name: generator-and-battery-lifetimes

| **Technology** | Lifetime (Years) | **Source** |
|----|:--:|----|
| Land-based Wind | 30 | LBNL Survey {cite}`wiserBenchmarkingAnticipatedWind2019` |
| Offshore Wind | 30 | LBNL Survey {cite}`wiserBenchmarkingAnticipatedWind2019` |
| Solar Photovoltaic | 30 | SunShot Vision {cite}`doeSunShotVisionStudy2012` |
| Concentrating Solar Power | 30 | SunShot Vision {cite}`doeSunShotVisionStudy2012` |
| Geothermal | 30 | Renewable Electricity Futures Study, Vol. 1 {cite}`maiExplorationHighPenetrationRenewable2012` |
| Hydropower | 100 | Hydropower Vision {cite}`doeHydropowerVisionNew2016` |
| Biopower | 50 | ABB {cite:year}`abbABBVelocitySuite2018a` |
| Marine Hydrokinetic | 20 | Previsic et al. {cite:year}`previsicFuturePotentialWave2012` |
| Battery | 15 | Cole and Frazier {cite:year}`coleCostProjectionsUtilityScale2020` |
```

Retirements of existing conventional energy generators in ReEDS are
primarily a function of announced retirement dates and
technology-specific estimated lifetimes, taken from the NEMS plant
database. Estimated retirement dates depend on the size of the unit, and
the most common lifetimes are shown in {numref}`conventional-energy-generator-lifetimes` 
for plants that are smaller or larger than 100 MW. Nuclear plants are assumed to have a mix
of 60- and 80-year lifetimes as explained below. All conventional
generators that are economically built in ReEDS are given the lifetime
of plants greater than 100 MW, and these lifetimes are used as necessary
when the solution period extends beyond 2050.

```{table} Lifetimes of Conventional Energy Generators <sup>a</sup>
:name: conventional-energy-generator-lifetimes

| **Technology** | Lifetime less than 100 MW (Years) | **Lifetime greater or equal to 100 MW (Years)** |
|----|:--:|:--:|
| Gas Combustion Turbine | 50 | 50 |
| Gas Combined Cycle and CCS | 60 | 60 |
| Coal, all techs, including cofired | 65 | 75 |
| Oil-Gas-Steam | 50 | 75 |
| Compressed-Air Energy Storage | 100 | 100 |
```
<sup>a</sup> {cite}`abbABBVelocitySuite2018a`

In addition to age-based retirements, ReEDS includes the option to
endogenously retire technologies (this option is turned on by default).
When doing endogenous retirements, ReEDS is trading off the value
provided to the system by the plant versus the costs incurred by keeping
the plant online. If the value is not sufficient to recover the costs,
ReEDS will choose to retire the plant. ReEDS includes a “retirement
friction” parameter that allows a plant to stay online as long as it is
recovering at least a portion of its fixed operating costs. For example,
if this retirement friction parameter is set to 0.5, then a plant will
only retire if it does not recover at least half of its fixed costs.
Additionally, ReEDS includes a minimum retirement age for existing
conventional plants of 20 years, meaning that a conventional plant is
not allowed to be endogenously retired until it is at least 20 years
old.

ReEDS includes four exogenous nuclear retirement scenario settings. The
four settings are defined by first dividing the currently operating
reactors into two bins. Any plants participating in a restructured
market and all single-reactor plants are assigned to Bin 1. The
remaining plants, which are all multi-reactor plants in a traditional
regulated environment, are assigned to Bin 2. The only exception to
these categorizations is that plants that have announced their intent to
seek a second operating license renewal from the Nuclear Regulatory
Commission (NRC) are included in Bin 2. {numref}`nuclear-plant-capacity` breaks down the bins
and shows total capacity in each case. These bins are categorizations
that reflect the current discussion pointing to more economic pressure
on restructured and single-reactor units {cite:p}`haratykEarlyNuclearRetirements2017, nicholasstecklerHalfNuclearPower2017`.


```{table} Amount of Nuclear Power Plant Capacity (in GW) in Each Bin
:name: nuclear-plant-capacity

| **Plant Category** | **Bin 1** | **Bin 2** |
|----|---:|---:|
| Restructured, Single Reactor | 8.7 | — |
| Restructured, Multi Reactor | 27.5 | 2.0<sup>a</sup> |
| Regulated, Single Reactor | 15.7 | — |
| Regulated, Multi Reactor | — | 42.1 |
| Total | **51.9** | **44.1** |
```

<sup>a</sup> The Peach Bottom plant (2.0 GW) has announced its intent
to seek a second license renewal. Therefore, it is moved from Bin 1 to
Bin 2 even though it is in a restructured
market.

The four nuclear retirement scenarios are: (1) Early Retirement, (2)
60-Year Lifetime, (3) Mid-Case (mix of 60 and 80-year lifetimes), and
(4) 80-Year Lifetime (see {numref}`nuclear-plant-lifetime`). The Early Retirement scenario
retires nuclear capacity in Bin 1 when its lifetime reaches 50 years,
and capacity in Bin 2 at 60 years. The 50-year lifetime emulates the
retirements of recent plants that did have a renewed operating license
but retired before they reached the end of their license. The 60-Year
Lifetime scenario retires all plants at 60 years, which would be at the
end of their first operating license renewal. The 80-Year Lifetime
scenario retires all plants at 80 years, simulating a successful
completion of a second operating license renewal from the NRC. The
Mid-Case scenario serves as the default setting in ReEDS and retires
capacity in Bin 1 at 60 years and capacity in Bin 2 at 80
years.

```{table} Nuclear Power Plant Lifetime for Each Scenario by Bin (years)
:name: nuclear-plant-lifetime

| **Scenario Name** | **Bin 1** | **Bin 2** |
|----|:--:|:--:|
| Early Retirement | 50 | 60 |
| 60-Year Lifetime | 60 | 60 |
| Mid-Case | 60 | 80 |
| 80-Year Lifetime | 80 | 80 |
```


#### Growth Constraints

The ReEDS model can represent either absolute growth constraints (e.g.,
wind builds cannot exceed 100 GW per year) or relative growth
constraints (e.g., wind capacity cannot grow by more than 50% per year).
The growth constraints are designed to target a broader technology group
as opposed to the individual classes of wind, PV, and CSP; as an
example, the growth constraint would restrict the builds of all wind
technologies and classes and not just a specific class. The default
values for the absolute growth constraints are the highest
year-over-year changes of each technology type’s capacity from 2010 to
2020 (computed by appending the necessary EIA AEOs). For CSP, the
default absolute growth limit is assigned the same as PV, as it has not
seen the capacity buildout as PV or wind have as of 2020. The relative
growth limits are applied on a state-level and are based on historical
compounded annual growth rate estimates observed for solar PV from
2012-2022. The penalties are assessed in ReEDS based on the maximum
previous growth observed in the model. For example, if a state
experienced 1,000 MW of new capacity in 2024 and 500 MW of new capacity
in 2025, then the growth penalty would be applied using the 1,000 MW
value even though it is older.

```{figure} ../../images/annual-growth-penalties.png
:name: figure-annual-growth-penalties

Annual growth penalties applied on a state level in ReEDS when the relative growth penalties are enabled.
```

ReEDS also includes minimum growth sizes, specified by technology type.
Those minimum growth sizes are shown in {numref}`min-growth-size-per-tech` and are generally based
on representative plant sizes.

```{table} Minimum growth size for each technology group. Growth below this level will never incur a rowth penalty regardless of starting capacity.
:name: min-growth-size-per-tech

| Technology group | Minimum growth size before a penalty is incurred (MW) |
|----|---:|
| CCS | 300 |
| CSP | 100 |
| Uncontrolled Natural Gas | 300 |
| Hydrogen | 100 |
| Nuclear | 600 |
| Solar PV | 100 |
| Storage | 100 |
| Wind-Offshore | 600 |
| Wind-Onshore | 100 |
```


### Regional Parameter Variations and Adjustments

For most generation technologies, regional cost multipliers are applied
to reflect variations in installation costs across the United States
(see {numref}`figure-regional-capital-cost-multipliers`). These regional multipliers are applied to the base
overnight capital cost presented in earlier sections. The regional
multipliers are technology-specific and are derived primarily from the
EIA/Leidos Engineering report {cite}`eiaCapitalCostEstimates2016` that is the source of capital
cost assumptions for the NEMS model. While the regional costs presented
in the EIA/Leidos Engineering report are based on particular cities, the
regional multipliers for ReEDS are calculated by interpolating between
these cities and using the average value over the ReEDS regions for each
technology. For technologies such as CSP that are not included in the
newer report, we rely on the older EIA/Science Applications
International Corporation report {cite}`eiaUpdatedCapitalCost2013`.

```{figure} ../../images/regional-capital-cost-multipliers.png
:name: figure-regional-capital-cost-multipliers

Maps of regional capital cost multipliers for the various technology types
```

Regions shown in white for offshore wind indicate that there is not
offshore wind resource in that region.  


## Fuel Prices

Natural gas, coal, and uranium prices in ReEDS are based on the most
recent AEO. Coal prices are provided for each of the nine EIA census
divisions. Low and high natural gas price alternatives are taken from
the Low and High Oil and Gas Resource and Technology scenarios. ReEDS
includes only a single national uranium price trajectory. Base fuel
price trajectories are shown in {numref}`figure-input-fuel-price-assumptions` for 
the AEO2023 {cite}`eiaAnnualEnergyOutlook2023`.
Biomass fuel prices are represented using supply curves with five bins
in each region. The costs and resource availability are based on the
*U.S. Billion-Ton Update* study {cite}`doeUSBilliontonUpdate2011`. Biomass costs range from
\$2.02/MMBtu to \$19.43/MMBtu (in 2018\$).

```{figure} ../../images/input-fuel-price-assumptions.png
:name: figure-input-fuel-price-assumptions

Input fuel price assumptions.
```

Natural gas fuel prices are adjusted by the model as explained
below.

Coal and uranium are assumed to be perfectly inelastic; the price is
predetermined and insensitive to the ReEDS demand for the fuel. With
natural gas, however, the price and demand are linked. Actual natural
gas prices in ReEDS are based on the AEO scenario prices but are not
exactly the same; instead, they are price-responsive to ReEDS natural
gas demand. In each year, each census division is characterized by a
price-demand “set point” taken from the AEO Reference scenario but also
by two elasticity coefficients: regional (β<sub>r</sub>) and national
(β<sub>n</sub>) elasticity coefficients for the rate of regional price
change with respect to (1) the change in the regional gas demand from
its set-point and (2) the overall change in the national gas demand from
the national price-demand set point respectively. The set of regional
and national elasticity coefficients are developed through a linear
regression analysis across an ensemble of AEO
scenarios[^ref32]<sup>,</sup>[^ref33] to estimate changes in fuel prices
driven solely by electric sector natural gas demand (as described in
Logan et al. {cite:year}`loganNaturalGasScenarios2013` and Cole, Medlock III, and Jani {cite:year}`coleViewFutureNatural`, though the
coefficients have since been updated for the latest AEO data). Though
there is no explicit representation of natural gas demand beyond the
electricity sector, the regional supply curves reflect natural gas
resource, infrastructure, and nonelectric sector demand assumptions
embedded within the AEO modeling. For details, see the Natural Gas
Supply Curves section of the appendix.

ReEDS includes options for other types of fuel supply curve
representations. Supply curves can be national-only, census-region-only,
or static. With the national-only supply curve, there are census
division multipliers to adjust prices across the census divisions. In
the static case, fuel prices are not responsive to
demand.

The natural gas fuel prices also include a seasonal price adjustor,
making winter prices higher than the natural gas prices seen during the
other seasons of the year. For details, see the Seasonal Natural Gas
Price Adjustments section of the appendix.


## Power System Water Use

The 2020 ReEDS version includes an updated representation of power
system water use that improves upon the formulation described in the
ReEDS version 2019 documentation {cite}`brownRegionalEnergyDeployment2020` as well as {cite}`macknickWaterConstraintsElectric2015`. Though inactive by default to limit computational
complexity, users can activate a power system water use formulation that
characterizes the existing fleet and new generation investments by both
their cooling technology and water source type, if applicable. Cooling
technology affects power system cost and performance, and water use is
constrained using technology withdrawal and consumption rates in
conjunction with water availability and cost data from {cite}`tidwellMappingWaterAvailability2018`. 
The rest of this section describes each component of this formulation.


### Existing Fleet Cooling Technology and Water Source

Thermal generating technologies in ReEDS are differentiated by the
following cooling technology types: once-through, recirculating, pond,
and dry(air)-cooled. Cooling technologies determine water withdrawal and
consumption rates as well as capital cost, operating cost, and heat rate
as described in [Cooling System Cost and Performance](#cooling-system-cost-and-performance). 
Generating technologies without cooling
systems are designated as having no cooling; however, these technologies
can still be assigned water use rates to account for processes such as
evaporation from hydropower reservoirs or cleaning PV arrays. All
power-cooling technology combinations (including water-using
technologies without cooling) are also assigned one of the following six
water source types included in the model: fresh surface water that is
currently appropriated, unassigned/unappropriated fresh surface water,
fresh groundwater, brackish or saline groundwater, saline surface water,
and wastewater treatment facility effluent. These water source types
align with the water supply curves described in [Water Availability and Cost](#water-availability-and-cost).
Representing both cooling technology and water source allows a
high-fidelity representation of water source-sink relationships and
constraints.

Cooling technology and water source of the baseline 2010 generation
fleet and subsequent prescribed builds is assigned using several data
sources mapped to the unit database that exogenously defines capital
stock in ReEDS. The EIA NEMS unit database is
first merged with the 2018 version of the EIA thermoelectric cooling
water dataset {cite}`useiaThermoelectricCoolingWater2018`. Cooling technology assignment uses the “860
Cooling Type 1” field where possible, followed by the “860 Cooling Type
2” and finally “923 Cooling Type”. Hybrid cooling systems are assigned
as recirculating except for hybrid dry/induced draft systems, which are
assigned as dry cooling. Any remaining gaps in cooling technology
assignment are filled using the UCS EW3 Energy-Water Database 
{cite}`unionofconcernedscientistsUCSEW3EnergyWater2012`. This procedure
enables annual updates through yearly reporting of EIA thermoelectric cooling 
water data. Thermal units with no available information on cooling 
technology are assigned recirculating cooling by default.

Water source in ReEDS is assigned where possible using the “Water Type”
and “Water Source” fields in the EIA cooling water dataset and then
supplemented using raw EIA Form 860 plant-level data {cite}`FormEIA860Detailed2018`. 
When the water source is unclear from the type and source, the “Water Source
Name” is used to help discern additional water source types and
determine which units use municipal water. Municipal water is treated as
an intermediary of the ultimate water source, which is defined using
U.S. Geological Survey (USGS) water use data for 2015 that includes
water sources for municipal use {cite}`dieterEstimatedUseWater2017`. Generating
units that use municipal water are assigned the water source that
supplies the majority of municipal water use in the USGS database. The
UCS EW3 database is also used to assign water sources unavailable in EIA
data {cite}`unionofconcernedscientistsUCSEW3EnergyWater2012`. Remaining unknown water
source types are assigned from USGS data using the majority water source
for the power sector, further differentiated by once-through or
recirculating cooling. If there is no USGS data for power sector water
use in the relevant county, the majority source of overall water use is
applied.

Beyond this multi-database approach to assign cooling technology and
water source, water source must be reassigned for some prescribed new
builds if the water availability described in [Water Availability and Cost](#water-availability-and-cost) is
insufficient for that unit’s water needs. For these instances, a final
adjustment procedure that temporary relaxes water use constraints is
used to identify these units and manually modify water source types to
use the BA’s least-cost water source with sufficient availability for
the prescribed unit.


### Cooling System Cost and Performance

Alternative cooling technologies are represented for the following
power system types:

- Coal: all types, including coal with CCS and biomass-cofired
coal
- Gas-CC: including Gas-CC with CCS
- Oil-Gas-Steam: also allows “no cooling” to represent capacity that does not use thermal cooling water (e.g., internal combustion engines)
- Nuclear
- Biopower: also allows “no cooling” to represent capacity that does not use thermal cooling water
- Landfill Gas: also allows “no cooling” to represent capacity that does not use thermal cooling water
- CSP: all thermal storage durations and resource classes

Water use is also characterized and constrained for hydropower, Gas-CT, geothermal, and distributed rooftop PV technologies, albeit without cooling technology disaggregation. This construct allows
total power sector water use to be estimated and could be expanded upon
in later model versions, particularly for geothermal technologies.

Some power-cooling technology pairs are also prohibited for new
construction by default. New, non-prescribed capacity for all
technologies cannot use once-through cooling due to U.S. Environmental
Protection Agency (EPA) regulations and industry trends {cite}`epa40CFRParts2014`. In addition, all new non-prescribed capacity cannot
choose pond cooling because pond cooling designs are site-dependent, and
ReEDS does not have sufficient detail to characterize location-specific
cooling pond design. The model also prevents new nuclear and coal-CCS
capacity from using dry cooling because existing designs have very high
cooling requirements where dry cooling is considered
impractical.

Cooling technology affects capital cost, variable operating cost, heat
rate, water withdrawal rate, and water consumption rate. Cost and heat
rate are adjusted for cooling technology by multiplying baseline
technology data by the factors in {numref}`capital-cost-multipliers`,
{numref}`variable-operations-capital-cost-multipliers`, and {numref}`heat-rate-multipliers`, 
where recirculating cooling is the reference cooling technology {cite}`macknickOperationalWaterConsumption2012`.
Typically, once-through cooling systems are less expensive
and allow higher overall thermal efficiency, while dry cooling is more
expensive and results in lower net thermal efficiency. Pond cooling
systems are typically intermediate to once-through and recirculating
cooling, but the model uses once-through cooling characteristics as an
approximation because actual cost and performance is site-specific. No
data exists for some power-cooling technology combinations (Gas-CC-CCS +
once-through and pond; Coal-CCS + pond, CSP + once-through and pond)
because no existing or planned units of those types
exist.

```{table} Capital Cost Multipliers for Power-Cooling Technology Combinations
:name: capital-cost-multipliers

|   Power Technology   |   Once-Through   |   Recirculating   |   Dry   |   Cooling Pond   |
|----------------------|------------------|-------------------|---------|------------------|
|                Gas-CC|             0.978|              1.000|    1.102|             0.978|
|            Gas-CC-CCS|           	   n/a|         	 1.000|    1.075|           	n/a|
| Pulverized coal with scrubbers (pre-1995)	|  0.981|    1.000|    1.045|             0.981| 
| Pulverized coal without scrubbers         |  0.981|	 1.000|	   1.045|	          0.981| 
| Pulverized coal with scrubbers (post-1995)|  0.981|  	 1.000|	   1.045|	          0.981| 
|             IGCC coal|       	     0.988|	             1.000|	   1.033|             0.988|
|              Coal-CCS|             0.982|	             1.000|	     n/a|	            n/a| 
|         Oil/gas steam|	         0.981|	             1.000|	   1.045|	          0.981| 
|               Nuclear|	         0.981|	             1.000|	     n/a|	          0.981| 
|              Biopower|	         0.981|	             1.000|	   1.045|	          0.981| 
|  Cofired coal (pre-1995)|	         0.981|	             1.000|	   1.045|	          0.981| 
| Cofired coal (post-1995)|	         0.981|	             1.000|	   1.045|	          0.981| 
|                   CSP|	           n/a|	             1.000|	   1.050|	            n/a| 
```

```{table} Variable Operations and Maintenance Cost Multipliers for Power-Cooling Technology Combinations
:name: variable-operations-capital-cost-multipliers

| Power Technology                            | Once-Through | Recirculating | Dry   | Cooling Pond |
|---------------------------------------------|--------------|---------------|-------|--------------|
| Gas-CC                                      | 0.996        | 1.000         | 1.021 | 0.996        |
| Gas-CC-CCS                                  | n/a          | 1.000         | 1.107 | n/a          |
| Pulverized coal with scrubbers (pre-1995)   | 0.989        | 1.000         | 1.051 | 0.989        |
| Pulverized coal without scrubbers           | 0.989        | 1.000         | 1.051 | 0.989        |
| Pulverized coal without scrubbers (post-1995)| 0.989       | 1.000         | 1.051 | 0.989        |
| IGCC coal                                   | 0.996        | 1.000         | 1.021 | 0.996        |
| Coal-CCS                                    | 0.993        | 1.000         | n/a   | n/a          |
| Oil/gas steam                               | 0.989        | 1.000         | 1.051 | 0.989        |
| Nuclear                                     | 0.989        | 1.000         | n/a   | 0.989        |
| Biopower                                    | 0.989        | 1.000         | 1.051 | 0.989        |
| Cofired coal (pre-1995)                     | 0.989        | 1.000         | 1.051 | 0.989        |
| Cofired coal (post-1995)                    | 0.989        | 1.000         | 1.051 | 0.989        |
| CSP                                         | n/a          | 1.000         | 1.050 | n/a          |
```

```{table} Heat Rate Multipliers for Power-Cooling Technology Combinations
:name: heat-rate-multipliers

| Power Technology                            | Once-Through | Recirculating | Dry    | Cooling Pond |
|---------------------------------------------|--------------|---------------|--------|--------------|
| Gas-CC                                      | 0.980        | 1.000         | 1.050  | 0.980        |
| Gas-CC-CCS                                  | n/a          | 1.000         | 1.075  | n/a          |
| Pulverized coal with scrubbers (pre-1995)   | 0.985        | 1.000         | 1.050  | 0.985        |
| Pulverized coal without scrubbers           | 0.985        | 1.000         | 1.050  | 0.985        |
| Pulverized coal with scrubbers (post-1995)  | 0.985        | 1.000         | 1.050  | 0.985        |
| IGCC Coal                                   | 0.980        | 1.000         | 1.050  | 0.980        |
| Coal-CCS                                    | 0.800        | 1.000         | n/a    | n/a          |
| Oil/Gas Steam                               | 0.985        | 1.000         | 1.050  | 0.985        |
| Nuclear                                     | 0.973        | 1.000         | n/a    | 0.973        |
| Biopower                                    | 0.985        | 1.000         | 1.050  | 0.985        |
| Cofired Coal (pre-1995)                     | 0.985        | 1.000         | 1.050  | 0.985        |
| Cofired Coal (post-1995)                    | 0.985        | 1.000         | 1.050  | 0.985        |
| CSP                                         | n/a          | 1.000         | 1.000a | n/a          |
```

<sup>a</sup> There are currently no data to inform a heat rate
multiplier for CSP.

More efficient-less expensive cooling technologies typically require
greater volumes of water withdrawal and consumption, creating a tradeoff
between cost and water use. Withdrawal and consumption rates for
power-cooling technology combinations are shown in {numref}`water-withdrawal-rates` and {numref}`water-consumption-rates`
{cite}`macknickOperationalWaterConsumption2012`. {numref}`water-withdrawal-and-consumption-rates` includes water use rates for power
technologies that are not differentiated by cooling technology; aside
from geothermal these values are negligible but could be modified by the
user if desired. Further, the model can accommodate BA-specific
withdrawal and consumption rates, so the values shown below could be
made regionally heterogeneous with sufficient data. Water withdrawal and
consumption rates coupled with assignment of water source type allow
ReEDS to characterize power system water demand for each technology, BA,
and water source combination.

```{table} Water Withdrawal Rates for Power-Cooling Technology Combinations (gal/MWh)
:name: water-withdrawal-rates

| Power Technology | Once-Through | Recirculating | Dry | Cooling Pond |
|----|----|----|----|----|
| Gas-CC | 11,380 | 255 | 2 | 5950 |
| Gas-CC-CCS | n/a | 506 | n/a | n/a |
| Pulverized coal with scrubbers (pre-1995) | 36,350 | 1,005 | 0 | 12,225 |
| Pulverized coal without scrubbers | 36,350 | 1,005 | 0 | 12,225 |
| Pulverized coal with scrubbers (post-1995) | 27,088 | 587 | 0 | 17,914 |
| IGCC Coal | 18,136 | 393 | 0 | 9,635 |
| Coal-CCS | 56,483 | 1,224 | n/a | n/a |
| Oil/gas steam | 35,000 | 1,203 | 0 | 5,950 |
| Nuclear | 44,350 | 1,101 | n/a | 7,050 |
| Biopower | 35,000 | 878 | 0 | 450 |
| Cofired coal (pre-1995) | 35,000 | 878 | 0 | 450 |
| Cofired coal (post-1995) | 35,000 | 878 | 0 | 450 |
| CSP | n/a | 786 | 26 | n/a |
```

```{table} Water Consumption Rates for Power-Cooling Technology Combinations (gal/MWh)
:name: water-consumption-rates

| Power Technology | Once-Through | Recirculating | Dry | Cooling Pond |
|----|----|----|----|----|
| Gas-CC | 100 | 205 | 2 | 240 |
| Gas-CC-CCS | n/a | 378 | n/a | n/a |
| Pulverized coal with scrubbers (pre-1995) | 250 | 687 | 0 | 545 |
| Pulverized coal without scrubbers | 250 | 687 | 0 | 545 |
| Pulverized coal with scrubbers (post-1995) | 113 | 479 | 0 | 545 |
| IGCC coal | 90 | 380 | 0 | 32 |
| Coal-CCS | 217 | 921 | n/a | n/a |
| Oil/gas steam | 240 | 826 | 0 | 240 |
| Nuclear | 269 | 672 | n/a | 610 |
| Biopower | 300 | 553 | 0 | 390 |
| Cofired coal (pre-1995) | 300 | 553 | 0 | 390 |
| Cofired coal (post-1995) | 300 | 553 | 0 | 390 |
| CSP | n/a | 786 | 26 | n/a |
```

```{table} Water withdrawal and consumption rates for technologies that are undifferentiated by cooling technology (gal/MWh)
:name: water-withdrawal-and-consumption-rates

| Power Technology | Withdrawal Rate | Consumption Rate |
|----|----|----|
| Hydropower | 1 | 1 |
| Gas-CT | 1 | 1 |
| Geothermal | 40 | 40 |
| Landfill-Gas | 1 | 1 |
| Distributed rooftop PV | 1 | 1 |
```

### Water Availability and Cost

All generating capacity that exists in a given model year is required
to have access to water if that technology uses water. The quantity of
required water access is defined conservatively to ensure sufficient
water is available to generate at maximum power output during the
expected annual low water flow condition. To align with annualized water
availability data, this requirement is formulated as the annual volume
of water needed to operate continuously at maximum output for the entire
year (100% capacity factor), i.e., the product of generating capacity
(MW), water use rate (gal/MWh), and 8760 hours per year. For capacity
that uses surface water, requirements are based on the water consumption
rate to account for the return of most withdrawn water directly to the
water source at the site of withdrawal. For all other water sources,
water access requirements are based on withdrawal rates because these
water types (e.g., groundwater, wastewater effluent) are not generally
returned to the site of withdrawal.

Generating capacity in the initial 2010 model year is assumed to have
secured sufficient water access prior to 2010. However, any new
prescribed or optimized investments must procure water access from a
power sector water availability supply curve developed by Sandia
National Laboratories {cite}`tidwellMappingWaterAvailability2018`. For use in ReEDS, water
availability and cost are aggregated to the BA resolution for each of
five water source types: fresh surface water that is currently
appropriated, unassigned/unappropriated fresh surface water, fresh
groundwater, brackish or saline groundwater, and wastewater treatment
facility effluent. Saline surface water is available to
existing capacity that currently uses it, but this water source is
assumed unavailable to new capacity due to current regulatory
constraints and industry expectations {cite}`epa40CFRParts2014`.
Tidwell et al. {cite:year}`tidwellMappingWaterAvailability2018` use a unique resource assessment and costing methodology
for each water source type, based on technical and legal considerations.
Costs include both capital and annualized operating costs associated
with each water source. Unassigned/unappropriated fresh surface water is
assumed to have negligible access cost, and costs typically increase in
the order of fresh groundwater, appropriated fresh surface water,
wastewater, and brackish/saline groundwater. Appropriated water is only
relevant to western U.S. water law, so there is no appropriated water in
the east, and many western regions lack unappropriated water (i.e., 100%
of total water is appropriated).

When capacity retires, its water access is automatically available to
any new capacity at the cost associated with the capacity’s water source
and region. For the initial 2010 fleet, all capacity that uses fresh
surface water is designated as using the “appropriated fresh surface
water” category so that retired water access is given the cost of other
appropriated water in that region. For the eastern U.S. where water
appropriation is inapplicable, retired fresh surface water access is
assigned a small nominal cost to avoid over procurement of water in the
model. This structure implies that any water access owned by the power
sector remains in the power sector and that increased competition does
not affect water supply or cost. Scenario analysis and future model
development could explore this assumption in greater
detail.

Similar to retirements, changes in water needs due to upgrades or
refurbishments are also accounted for in the water access
requirement.

```{figure} ../../images/water-availability-and-cost.png
:name: figure-water-availability-and-cost

Water availability and cost for each water type in each ReEDS balancing area.
```


### Water Constraints

Several model constraints govern the ReEDS power sector water use
formulation. Water withdrawal and consumption quantities are tracked for
each power technology, cooling technology, water source, power
technology vintage, BA, timeslice, and year, providing high resolution
with which to examine power sector water use. Separately, water access
requirements are related explicitly to the capacity available for each
power technology, cooling technology, water source, power technology
vintage, BA, and year based on either the withdrawal or consumption rate
as described in [Water Availability and Cost](#water-availability-and-cost). This water access is then limited by the
total access available for each water source and region as defined by
the water allocation in 2010 and the supply available to post-2010
capacity.

Quantities of water used for each power technology, cooling technology,
water source, power technology vintage, and BA are then constrained
within each season based on the seasonal allocation of available water
access. Water access must be purchased from the water availability
supply curve before water can be used. Hydrology data is used to define
the seasonal allocation of unassigned/unappropriated fresh surface water
{cite}`macknickWaterConstraintsElectric2015`, and all other water types are assumed
available uniformly throughout the year. Additional detail on seasonal
water allocation and the potential for changes over time requires
additional data, but the framework generally allows the capability for
incentivizing water sources that are more available when electricity
demands are higher.


## Transmission

ReEDS considers two categories of transmission: “local interconnection” of generation
resources within the 134 model zones, and “interzonal” or
“long-distance” transmission between the model zones. These two
categories of transmission share underlying cost data but are
represented differently within the model. We begin with a discussion of
transmission costs, then describe the separate representations of
“interconnection” and “long-distance” transmission within ReEDS.


### Transmission costs

Estimated costs for transmission lines are generated by defining a
high-geographic-resolution cost surface, then utilizing a
least-cost-path algorithm to identify a representative transmission line
path between two points {cite}`lopezSolarPhotovoltaicsLandBased2024a`. The final \$/MW cost for a
particular route is then given by the integrated \$/MW-mile values for
the cost surface points traversed by the least-cost
route.

Base voltage-dependent \$/MW-mile transmission costs are taken from
four sources: Southern California Edison for CAISO and the Northeast,
WECC/TEPPC for non-CAISO areas in the Western Interconnection, MISO for
the Midwest, and a representative utility for the Southeast. These base
transmission costs are shown on the left side of {numref}`figure-transmission-cost-input-data`. Cost
multipliers based on terrain type (hilly, with 2% ≤ land slope \< 8%,
and mountainous, with 8% ≤ land slope) and land class (pasture/farmland,
wetland, suburban, urban, and forest) are taken from the same four
sources. A separate 90m-resolution CONUS dataset of terrain and land
classes is then combined with the base transmission costs, terrain
multipliers, and land class multipliers to generate the cost surface
used in the least-cost-path routing algorithm.

```{figure} ../../images/transmission-cost-input-data.png
:name: figure-transmission-cost-input-data

Overview of transmission cost input data used in reV model calculations, used to generate ReEDS model inputs.
```

All transmission also incurs FOM costs, which are approximated as 1.5%
of the upfront capital cost per year.


### Local generator interconnection

There are three components of local generator interconnection
represented in ReEDS: geographically resolved spur lines and substation
upgrades, geographically resolved reinforcement of the existing
transmission network, and a geographically independent cost adder for
all technologies.


#### Spur lines and substation upgrades

Spur lines represent short-distance transmission built to connect new
wind and solar generation capacity to a “point of interconnection” (POI)
on the existing transmission system. For a given wind/solar site (the
~50,000 reV supply curve points discussed above), substations within the
same state are considered as possible POIs. Least-cost paths are
calculated to all candidate substations, and the substation with the
lowest resulting path-dependent spur-line cost is taken as the POI for
that wind/solar site. An appropriate spur-line voltage is chosen based
on the available wind or solar capacity at that site, with lower
available capacity leading to a lower spur-line voltage and a higher
associated \$/MW-mile cost. The cost of upgrading the POI substation is
included in the spur-line cost. Additional sources and details are
provided by Lopez et al {cite:year}`lopezImpactSitingOrdinances2023`.


#### Network reinforcement

Network reinforcement represents upgrades to the existing transmission
network required to avoid congestion when moving power from the POI to
load centers. It is intended to represent the costs associated with
interconnection queues, which represent a major bottleneck for the
deployment of new wind and solar in the US. We estimate network
reinforcement costs by tracing a path along existing transmission lines
from each substation POI to each zone “center” within the same state;
the zone center is usually taken as the largest population center in the
model zone, but is sometimes (for zones without large urban centers)
assigned to a high-voltage substation within the zone. A cost for each
reinforcement route is calculated using the cost surface described in
[Transmission costs](#transmission-costs), with capex costs multiplied by 50% to represent the lower
cost for reconductoring compared to greenfield transmission
construction. The single lowest-cost route for each POI is then
selected; the associated reinforcement cost \\$/MW\] and transmission
distance \MW-miles\] are incurred for every MW of new wind/solar
capacity added at all reV sites associated with that
POI.[^ref34]

{numref}`figure-local-generation-interconnection-components` illustrates the concepts of spur lines and reinforcement
lines, and {numref}`figure-interconnection-cost-distribution` shows the resulting distribution of interconnection
costs for land-based wind and utility-scale PV under the three siting
regimes. {numref}`figure-utility-scale-pv-costs` and {numref}`figure-land-based-wind-costs` show maps of the estimated spur-line
costs, reinforcement costs, total interconnection costs, and total
supply curve costs (including land-cost adders) for utility-scale PV and 
land-based wind under reference-access siting assumptions.

```{figure} ../../images/local-generation-interconnection-components.png
:name: figure-local-generation-interconnection-components

Illustration of local generation interconnection components.
```

```{figure} ../../images/interconnection-cost-distribution.png
:name: figure-interconnection-cost-distribution

Interconnection cost distribution for land-based wind (blue) and utility-scale PV (orange) under different siting assumptions.
```

```{figure} ../../images/utility-scale-pv-costs.png
:name: figure-utility-scale-pv-costs

Supply-curve costs for utility-scale PV with reference-access siting.
```

```{figure} ../../images/land-based-wind-costs.png
:name: figure-land-based-wind-costs

Supply-curve costs for land-based wind with reference-access siting.
```


#### Intra-zone transmission cost adder for net increases in generation capacity

In addition to the interconnection costs described above, we also apply
a flat intra-zone transmission cost adder of \$100/kW to net increases
in generation and AC/DC converter capacity within each model zone. This
value is taken from historical interconnection costs for fossil gas
capacity as reported in Seel et al. 2023 and is taken to represent a
“floor” for network upgrades that are required even if new capacity is
added at the optimal location (assuming that past additions of fossil
capacity have been placed to minimize interconnection costs). The
\$100/kW adder is subtracted from the reinforcement cost applied to wind
and solar to avoid double counting. As we assume that new generation
capacity will reuse the network infrastructure from retiring capacity,
the intra-zone transmission cost adder is only applied to *net*
increases in generation capacity.


### Interzonal transmission

- High level 
   - Pipe and bubble / transport model 
   - Distribution losses 


#### Existing transmission capacity

```{figure} ../../images/ac-transmission-capacity.png
:name: figure-ac-transmission-capacity

Existing AC transmission capacity in ReEDS.
```

Short description of ITL paper

The transmission network in ReEDS is a
synthetic network developed from nodal data assembled as part of the
North American Renewable Integration Study (NARIS) \[37\]. This dataset
relies on nodal transmission models developed for the Eastern, Western,
and ERCOT interconnections under the guidance of the North American
Reliability Corporation (NERC) and includes ~56,000 buses, ~94,000
transmission lines, and ~37,000 transformers. Capacity expansion models,
such as ReEDS, typically use zonal representation to remain tractable,
forgoing the modeling of individual generation, consumption, or
transmission assets and instead grouping them into zones which are
treated as copper plates. Assigning generation and demand units to their
respective zones is intuitive, however deriving the transmission
topology from the resolved nodal data is more involved than aggregating
steady state rated capacity across zonal interfaces due to the physics
of electrical power flow in meshed networks. In \[38\] the authors
propose a method for estimating the interface transfer limits between
zones from nodal transmission data utilizing a DC power flow
approximation. In this approach two independent optimizations are
performed to maximize the sum of flows in the forward direction on the
transmission lines crossing the interface and to minimize the sum of
flows in the reverse direction crossing the interface. The power flow is
constrained by the line ratings as described in
(5).

$$-k(l) \le F(l) \le k(l) $$

(5)

The relationship between line flows and bus injections or withdrawals
is dictated by the power transfer distribution factor (PTDF) matrix
described in (6). The PTDF relates the change in transaction amount
(amount of power injected at one zone and withdrawn in another zone) to
the change in power flow on a line. For instance, $_{}$ represents that
fraction of power transferred from zone *m* to zone *n* that flows over
a transmission line connecting zone *i* and zone
*j.*

$$F(l) \sum_{b}^{B} p(l,b)G(b) \quad \forall l$$

(6)

Additional constraints are applied to individual buses for which bus
type data are available, limiting injections for load buses and
withdrawals for generation buses, and both injections and withdrawals
for transmission buses. In conjunction these constraints establish a
more stringent limit for interface transfer capacities as compared to
the approach which sums the line ratings across interfaces. This method
for deriving interface transfer limits is used to create the
transmission networks in both the default BA resolution of ReEDS. 
At the BA resolution the optimization
is run within each U.S. interconnection separately as they operate
nearly independently due to limited transfer capacity \[39\]. Due to the
relative density of the eastern interconnection, subsets of the network,
defined by a distance threshold from the interface in questions, are
solved iteratively to reduce the complexity of the optimization
\[38\].

We also drop sub-230 kV lines from interfaces where they make up less
than half of the total interface transfer capacity (which isn’t
described in the ITL paper)

- Map of existing capacity (r and transgrp
resolution)

  - Extra constraint on inter-transgrp flows
   
- Existing B2B and LCC HVDC


#### Costs and routes for new AC transmission additions

```{figure} ../../images/new-ac-transmission-cost-assumptions.png
:name: figure-new-ac-transmission-cost-assumptions

Costs assumed for new AC transmission additions.
```

- 500 kV single circuit
- Losses
- Least-cost paths
- FOM costs
- Financial multipliers / CRF
- Options for limiting new capacity


#### High-voltage direct current (HVDC) “macrogrids”

- LCC (point-to-point)
    - Costs and losses
- VSC (meshed)
    - Costs and losses
    - Operational constraints
    

### User-adjustable transmission assumptions

- Hurdle rates

ReEDS includes a default hurdle rate of \$0.01/MWh (in
2004\$) in order to reduce degeneracy between curtailment and
transmission losses. Users can adjust the hurdle rate to any value that
might meet their needs.

- PRM trading
- Transmission investment and capacity limits
- Lots of other stuff


### Transmission System

ReEDS uses a synthetic network with 134 nodes
defined by roughly 300 corridors for the contiguous 48 states. Each
corridor has a nominal carrying capacity limit that is
determined for the start-year (2010) based on power-flow analysis using
ABB’s GridView model and NERC-reported line limits {cite}`nerc2010LongtermReliability2010`. The
carrying capacity of DC transmission connections are taken from project
websites. A few notable DC transmission connections that are modeled in
ReEDS are listed in {numref}`dc-transmission-connections`.

In later years, ReEDS can expand these carrying capacities, though the
model cannot build new node-to-node pathways. Transmission expansion is
limited before 2022 based on new construction that is already planned
{cite}`abbABBVelocitySuite2013`. After 2022, that limitation is dropped. ReEDS constrains
transmission flows in each of the representative time-slices when
dispatching generation and contracting operating reserves, and available
transmission capacity can also be used for firm power contracts to meet
system adequacy needs.

```{table} List of Notable DC Transmission Connections Modeled in ReEDS
:name: dc-transmission-connections

|             **Project**             | **Capacity (MW)** |
|-------------------------------------|------------------:|
|                 Pacific DC Intertie |             2,780 |
|         Intermountain Power Project |             1,920 |
|     Miles City Intertie (West-East) |               200 |
| Virginia Smith Intertie (West-East) |               200 |
|         Segall Intertie (West-East) |               110 |
|       Artesia Intertie (West-ERCOT) |               200 |
|     Blackwater Intertie (West-East) |               200 |
|     Rapid City Intertie (West-East) |               200 |
|          Lamar Intertie (West-East) |               210 |
|                             CU HVDC |             1,500 |
|                        Square Butte |                   |
|     Oklaunion Intertie (ERCOT-East) |               220 |
|         Welsh Intertie (ERCOT-East) |               600 |
```


In general, the modeled nodes are located at the largest population
center of each BA, although some manual adjustments are made.[ref^35]
Distances between BA nodes are estimated by tracing the “shortest path”
distance along existing transmission lines, giving preference for the
trace follow higher voltage lines. Voltages for each transmission line
were defined using the Homeland Security Infrastructure Project (HSIP)
transmission database and converted into 1-km grid. The maximum voltage
in each grid cell was identified and assigned a weight based on the
voltage classification per {numref}`voltage-class-weights` to create a tension grid. Using this
tension grip, a least “cost” (lowest weight) path was traced between
every BA-to-BA corridor was determined using the tension grid. Finally,
the great circle formula is used to calculate the distance of the traced
paths. The lengths of DC corridors are taken from values
reported on project websites.

```{table} Weights for Each Voltage Class
:name: voltage-class-weights

| **Voltage Class (kV)** | **Weight** |
|----|---:|
| No line | 1,000 |
| 100–161 | 10 |
| 230–300 | 5 |
| 345 | 3 |
| 500 | 2 |
| 735 and above | 1 |
```

Transmission network flows in ReEDS are limited based on the nominal
carrying capacity of the corridors. ReEDS can choose to
build additional transmission capacity on the existing network to reduce
congestion, but expansion of AC-DC-AC interconnection ties are not
allowed under default assumptions. New long-distance HVDC lines are not
allowed by default, but can be specified in the model inputs. ReEDS does
not represent reactive power and does not address AC-power-flow issues
of voltage, frequency, or limiting phase angle differences. Intra-BA T&D
networks are similarly ignored, effectively ignoring the effects of
transmission congestion within each region.

Transmission and distribution losses are
considered in the model. There are bulk transmission losses of 1% per
100 miles for power that flows between BAs. In addition, distribution
losses of 5% are assumed and thus added to the end-use demand ([Electricity Load](#electricity-load))
to scale end-use demand to busbar load. Distribution losses do not
apply to rooftop PV, as they are assumed to be downstream within
distribution networks, but they do apply at a lower rate to DUPV
systems, which are assumed to connect directly to low-voltage
distribution substations ([Electricity Load](#electricity-load)).


### International Electricity Trade

ReEDS is capable of endogenously representing Canada and Mexico, 
but our default model configuration only covers the
contiguous United States and represents electricity trade with Canada
exogenously. In the default configuration, imports and exports are
specified by Canadian province based on the National Energy Board’s
(NEB) Canadian Electricity Futures Reference Scenario {cite}`nebCanadaEnergyFutures2018`, 
with net exports across all regions shown in {numref}`figure-canada-imports-exports` (values beyond NEB
projections to 2040 are held constant at the 2040 value). Each province
is required to send electricity to or receive electricity from any of
the ReEDS BAs that have connecting transmission lines to that province,
with the split among BAs approximated based on the transmission
connecting the BAs to the provinces. Seasonal and time slice estimates
for imports and exports are based on the historical monthly flows
between the countries.[^ref36] Canadian imports are assumed to be from
hydropower and are counted toward RPS requirements where allowed by
state RPS regulations. Canadian imports also count toward reserve margin
requirements.

```{figure} ../../images/canada-imports-exports.png
:name: figure-canada-imports-exports

Imports from Canada to the United States and exports from the United States to Canada
```


## Electricity System Operation and Reliability

ReEDS finds the least-cost way of building and operating the
electricity system while meeting certain requirements that are dominated
by the need to meet electricity load while maintaining system adequacy
and operational reliability.


### Electricity Load

The primary constraint in ReEDS is to serve electricity load in each
hour and BA. The end-use electricity load projection used in ReEDS is
exogenously defined. There are many exogenous load profiles available in
the model, designed to accommodate various study needs and
sensitivities. Especially as the electrification of non-electric energy
uses creates significant regional and temporal shifts to the electric
sector load representation, the choice of load profile is important as
it contributes to the technology deployment mix and
quantity.

The ReEDS load profiles are all hourly, and at the ReEDS BA level
resolution, However, their sources and processing through the model vary
slightly, as are described in the following
subsections.


#### Evolved Energy Research Load Profiles

The newest load profile addition to the model is the adoption of new
load profiles from Evolved Energy Research (EER) which feature the
impacts of the Inflation Reduction Act. EER’s EnergyPATHWAYS model has
been the source of previous ReEDS load profiles, as described in [Electrification Futures Study Load Profiles](#electrification-futures-study-load-profiles).
It uses a bottom-up methodology, building load profiles for each
end-use sector before aggregating them together, yielding an hourly,
state, subsector level load profile. Their results were disaggregated to
the ReEDS BA level and aggregated to reflect total end-use load in the
ReEDS model. The default load profile in ReEDS Version 2023 “reflects
relatively conservative assumptions about the impact of demand-side
provisions in the Inflation Reduction Act (relative, compared to other
scenarios developed by EER)” {cite}`gagnon2023StandardScenarios2024a`.
The Inflation Reduction Act (IRA) features many tax credits and
subsidies for electric end-use technologies such as electric vehicles
and heat pumps, to name only a couple. More information about the
provisions in the IRA can be found in X. Other EER load profiles feature
100% economy wide decarbonization by 2050 or business as usual
electrification assumptions. Compound annual growth rates and 2050
CONUS-wide annual demand for these profiles are shown in {numref}`growth-rates-and-electric-load`. One
benefit of these load profiles is that they feature 7 weather years of
data (2007-2013), allowing us to compute resource adequacy based on
various weather conditions.


```{table} Compound annual growth rates and 2050 electric load values for a variety of EER load profiles available in ReEDS.
:name: growth-rates-and-electric-load

|  | CAGR (2024 through 2050) | 2050 CONUS-wide Electric Load (TWh/year) |
|----|----|----|
| IRA Low (default) | 1.8% | 6,509 |
| Business as Usual | 0.9% | 5,054 |
| 100% economy-wide decarbonization by 2050 | 2.8% | 8,354 |
```


#### Historical Load Data + AEO Growth Factor Profiles

The second method with which load can be modeled in ReEDS is with a
historical (until 2010), hourly data set, which is then multiplied by
load growth factors from AEO. The historical data are sourced directly
from regional transmission organization (RTO) and independent system
operator (ISO) websites for the applicable regions, with load data being
requested at the most granular resolution available and for weather year
2012. For regions served by utilities, FERC Form 714 hourly load data
are used. Hourly BA-level profiles are averaged to the selected
representative time-slice level. These 2012 weather year profiles are
then scaled to ensure a match with the 2010 state-level annual retail
energy load data from EIA’s Electricity Data Browser {cite}`eiaElectricPowerDetailed2015`. Within
a state in ReEDS, further adjustments to load profiles use county level
load participation factors from Ventyx {cite:year}`ventyxVentyxVelocitySuite2014`. 
The regional growth factors for years after 2010 are from the AEO scenario 
electricity consumption by state. For each model year in ReEDS, the regional 
load profiles are scaled by regional growth factors, but the shape of the
load profile is assumed to be constant throughout the study period. For
capacity credit calculations, hourly load from the 2007-2013 weather
years are used (see [Resource Adequacy](#resource-adequacy)).

The end-use load, described in the previous paragraph, is defined at
the meter level. ReEDS includes inter-BA transmission system losses in
the optimization but does not represent distribution losses, so the
end-use load must be scaled up to busbar load to account for
distribution losses. The 5% distribution loss factor used for this
conversion is estimated based on a combination of EIA and ReEDS numbers.
ReEDS is required to generate sufficient power in each time-slice and BA
(allowing for transmission of power but accounting for losses) to meet
this busbar load. [^ref37]


#### Electrification Futures Study Load Profiles

The ReEDS model also contains detailed electrification load profiles
were developed as part of the Electrification Futures Study (EFS) using
EnergyPATHWAYS {cite}`sunElectrificationFuturesStudy2020a`. There are three levels of
electrification load. Reference matches the ReEDS reference load using
AEO 2018 disaggregated to the subsector level reaching 4790 TWh of
annual demand and 860 GW peak demand. The Medium and High
electrification cases layer on top of the Reference electrification case
the incremental growth from EnergyPATHWAYS. Medium electrification
reaches 5800 TWh of annual demand and 1130 GW of peak demand and High
6700 TWh of annual demand and 1320 GW of peak demand. Hourly load
representation with electrification scenarios uses a single 2012 weather
year. This demand data is duplicated to match 7-year weather profiles,
which results in loss of synchronicity between weather and demand data
but we are able to capture greater interannual variability during peak
hours.

Electrification of natural gas consuming end uses impacts natural gas
demand beyond the electric power sector. Alternate economy wide natural
gas scenarios are available for use with electrification cases, which
improve the representation of changing natural gas consumption outside
of the electric sector.


#### Load Adjustment Method for End Use Profiles

ReEDS includes a methodology to incorporate changes to hourly electric
load shapes derived from analysis of other modeling tools. Regional
hourly load changes are paired with a defined regional adoption
trajectory for this load change by year. Combining these two factors
allows for ReEDS to changes to load profiles specific to region, year,
and hour. A further unique capability of this method is that an
arbitrary number of load changes and adoption trajectories can be
provided allowing for sophisticated changes to load shapes with a small
number of provided parameters.

```{figure} ../../images/reeds-load-adjustment-method.png
:name: figure-reeds-load-adjustment-method

ReEDS Load adjustment method.
```

This methodology is that it allows for ReEDS load profiles to be
adjusted quickly within an analysis scenario. This methodology is based
upon methods developed to incorporate changes to electric power demand
associated with geothermal heat pumps (GHP) and example hourly change
profiles and adoption scenarios derived from that analysis are
available.


### Resource Adequacy

Resource adequacy is “the ability of supply- and demand-side resources
to meet the aggregate electrical demand” {cite}`nercGlossaryTermsUsed2016`. Planning reserve
requirements in ReEDS ensure adequate resource is available at all
times, within an acceptable probability of failing to do so. In
practice, this constraint is enforced by requiring the system to have
sufficient firm capacity to meet the forecasted peak demand plus a
reserve margin. This constraint is enforced for each season to
accommodate the potential for peak net load to shift seasons as
renewable penetration increases.

Each technology is assigned a capacity credit[^ref38] reflecting its
expected availability when power is needed, typically during the
highest-risk hours, which are ideally identified as the hours with
highest loss of load probability (LOLP)[^ref39]. For conventional
non-variable generators in ReEDS, the CC is
one.


#### Capacity credit formulation
**VRE Capacity Credit**

For VRE technologies (i.e., wind and solar), ReEDS estimates a seasonal
capacity credit for each region/class combination via an hourly LDC
approximation of expected load carrying capability (ELCC)[^ref40] performed
between solve years.[^ref41] ELCC can be described as the amount of
additional load that can be accommodated by adding those generators
while maintaining a constant reliability level. The “8760-based”
methodology can capture the highest load and net load hours, which
typically represent the highest risk hours, and can thereby support a
reasonable representation of capacity credit. Details of this LDC
approach, as well as a comparison against a former statistical method,
can be found in Frew et al. {cite:year}`frew8760BasedMethodRepresenting2017a`, though that approach has been
expanded to consider 7 years of wind, solar, and load data (2007-2013)
rather than just a single year.

The LDC approach for calculating capacity credit is based on explicit
hourly (8,760 hours x 7 years) tracking of time-synchronous load and VRE
resources. The capacity method uses a capacity factor proxy that is
applied to top 10 hours in load and net load-duration curves (LDCs and
NLDCs) in each season to estimate ELCC by season. {numref}`figure-cv-calculation-ldc-approach` graphically
represents the ReEDS capacity credit methodology. The LDC reflects the
total load in a given modeling region, which is sorted from the hours of
highest load to lowest load and is shown by the blue line. The NLDC
represents the total load minus the time-synchronous contribution of
VRE, where the resulting net load is then sorted from highest to lowest,
as shown by the solid red line.[^ref42] The NLDC(δ), which represents
further addition of VRE resources, can be created by subtracting
the time-synchronous generation of an incremental capacity addition from
the NLDC, where the resulting time series is again sorted from highest
to lowest; this is shown by the dashed red
line.

```{figure} ../../images/cv-calculation-ldc-approach.png
:name: figure-cv-calculation-ldc-approach

LDC-based approach to calculating CV
```

ReEDS calculates the ELCC as the difference in the areas between the
LDC and NLDC during the top 10 hours of the duration curves in each
season, as represented by the dark blue shaded area in {numref}`figure-cv-calculation-ldc-approach`. These
10 hours are a proxy for the hours with the highest risk for loss of
load (i.e., the LOLP).[^ref43] Similarly, the contribution of an additional
unit of capacity to meeting peak load is the difference in the areas
between the NLDC and the NLDC(δ), as shown by the light blue shaded area
in {numref}`figure-cv-calculation-ldc-approach`. To ensure resource adequacy, ReEDS calculates capacity
credit based on a 1,000-MW incremental capacity size of new solar and
wind builds. These areas are then divided by the corresponding installed
capacity and number of top hours (10 hours per season in this case,
although the number of hours can be adjusted by the user) to obtain a
fractional seasonal-based capacity credit.

The resulting existing and marginal capacity credit[^ref44] values then
feed into ReEDS to quantify each VRE resource’s capacity contribution to
the planning reserve requirement. Existing VRE capacity credit
calculations are performed by region and technology. For all candidate
VRE resources that might be built in the coming year, the *marginal*
capacity credit is calculated by region, technology, and resource class.
In all cases, the VRE profile is compared against the aggregated
resource assessment region (RAR) load profile for determining the
capacity credit ({numref}`figure-cv-calculation-ldc-approach`). We use the RAR-level load profile to
simplify the challenge of representing the ability of transmission to
wheel VRE capacity from one BA to another. Essentially, we assume a
copper plate within each RAR for the purpose of sharing VRE capacity. We
use RAR regions rather than NERC regions for this assumption because
transmission and trading tend to be more closely related to RAR regions
than NERC regions.

**Storage Capacity Credit**

The storage capacity credit method in ReEDS characterizes the increase
in storage duration that is needed to serve peak demand as a function of
storage penetration. The potential of storage to serve peak demand is
considered by performing several simulated dispatches against the load
profiles within each of the resource assessment regions shown in {numref}`figure-cv-calculation-ldc-approach`.

Load profiles net of wind and PV generation are used to capture the
effects of VRE resources on the overall net load profile shape in a
region using the load, wind, and solar data from
2007-2013.

For each season and reliability assessment zone, a storage dispatch is
simulated with peaking capacity prioritized over all other services
(reflecting capacity market prioritization as discussed by Sioshansi, et
al. {cite:year}`sioshansiDynamicProgrammingApproach2014`).Transmission constraints are ignored within each reliability
assessment zone for computational efficiency; this copper plate
transmission assumption only applies to the capacity credit
calculation—all transmission constraints are enforced in the actual
planning reserve margin constraint and other system planning and
operation modelling in ReEDS. Optimal coordination of dispatch among
energy storage resources is also assumed. The transmission and
coordination assumptions together allow for all storage within a
reliability assessment zone to be represented as a single aggregate
resource. The round-trip efficiency of this aggregated storage resource
is assumed to be equal to the energy-capacity-weighted average
round-trip efficiency of all installed storage capacity in that
region.

All round-trip efficiency losses are included in storage charging. For
example, a storage resource with a round-trip efficiency of 85% and a
power capacity of 10,000 MW can dispatch 10,000 MW to the grid for 1
hour using 10,000 MWh of energy capacity. However, when the same
resource draws 10,000 MW from the grid for 1 hour, its state-of-charge
increases by only 8,500 MWh.

{numref}`figure-energy-capacity-requirements-for-storage` illustrates the dispatch and calculation of the energy
requirement for 5,000 MW of storage to receive full capacity credit in
the NYISO region in 2020. First, the storage power capacity is
subtracted from the peak load to set a net load maximum. Storage is
required to discharge whenever the load profile exceeds this maximum, to
ensure the peak net load (load minus storage in this example) is equal
to the peak load minus the power capacity of the storage device. The
storage is allowed to charge at all other times while ensuring the load
maximum is not exceeded.

```{figure} ../../images/energy-capacity-requirements-for-storage.png
:name: figure-energy-capacity-requirements-for-storage

**Model results for determining energy capacity requirements for storage in NYISO in 2020 for a 3-day example in August.** 47,000 MWh is determined to be the necessary energy capacity for 5,000 MW of storage to receive full capacity credit. A depth of discharge of 0 indicates that the storage is full.
```

This dispatch is then used to calculate the energy requirement for
storage to receive full capacity credit. At the beginning of the season,
the state-of-charge of storage within the region is assumed to be full.
The state-of-charge (or depth of discharge, as it is shown in {numref}`figure-energy-capacity-requirements-for-storage`) 
is tracked over the course of the time-series with the maximum
depth of discharge left unconstrained. This means the maximum depth of
discharge value over the course of the season is equal to the amount of
energy capacity that is needed for storage to receive full capacity
credit. Dividing this energy by the power capacity used produces the
minimum fleet-wide average duration (hours) for storage to receive full
capacity credit. In the example in {numref}`figure-energy-capacity-requirements-for-storage`, 5,000 MW of peak demand
reduction from storage would require 47,000 MWh of energy to receive
full capacity credit, or a duration of 9.4
hours.

We repeat this process in each region for each season over a large
range of storage power capacities (from 0% to 90% of peak demand in
100-MW increments). The result of each dispatch is used to produce the
“power-energy curve” in {numref}`figure-storage-peak-capacity-determination`, which allows us to calculate the
marginal capacity credit for additional storage. The curve gives storage
energy capacity that is required for full capacity credit as a function
of storage penetration.[^ref45] At any point along the curve, the slope of
the tangent to the curve represents the number of hours needed for
marginal storage to receive full capacity credit. The incremental
capacity credit of an additional unit of storage is equal to the
duration of the additional unit installed divided by the duration
requirement (slope) at the point on the curve corresponding to the
installed storage penetration.

```{figure} ../../images/storage-peak-capacity-determination.png
:name: figure-storage-peak-capacity-determination

Determining storage peaking capacity potential in ReEDS.
The slope of each dashed line is the power-to-energy ratio for the
duration specified. Model results are for ERCOT in 2050. Note these
capacities are cumulative, starting from the shortest duration and
moving to the longest.
```

{numref}`figure-storage-peak-capacity-determination` also illustrates how 
we create a more tractable solution by
reducing the number of combinations considered. Storage in ReEDS is
considered in several discrete durations, and these discrete durations
are used to define the requirements needed to receive full capacity
credit. Instead of a continuous function represented by the constantly
varying slope of the power-energy curve, we create several discrete peak
duration “bins” representing duration requirements. We start by plotting
a line with constant slope equal to the shortest duration considered and
find where it intersects with the power-energy curve. Then, starting
from that point, we plot a line with the next shortest duration and find
the point where it intersects with the power-energy curve, and so on,
until we have obtained the cumulative limit for each discrete duration
of storage to serve peak demand.

As an example, the first segment (having a slope of two) requires two
hours to provide full capacity credit, even though it may be physically
possible for some small amount of storage with a duration less than two
hours to receive full capacity credit. In this example, at the point
where 4,309 of 2-hour storage has been added, the lines intersect and
the interpolation shifts to a slope of 4 hours, so a device with 4 hours
is now required to achieve full capacity credit. The model is still
allowed to build 2 hours storage, but it will only receive a 50% (2/4)
capacity credit, or the duration of the installed storage device divided
by the discrete peak duration “bin”. At each point, the marginal
capacity credit is calculated by the physical capacity of the
incremental unit, divided by the discrete duration requirement slope at
any point along the curve.

The limit for each duration to serve peak demand from {numref}`figure-storage-peak-capacity-determination` is
passed back to the ReEDS model, and the model optimizes the capacity
credit of all storage (existing and new investments) together. One
advantage of this is that it informs the model of when the capacity
credit of storage should go up or down in response to changes in the net
load profile shape. Another advantage is that total storage peaking
capacity can be assessed in conjunction with other services storage can
provide such as curtailment recovery, energy arbitrage, and operating
reserves[^ref46], and a least-cost solution can be obtained
overall.

Building on the results in the example above, {numref}`figure-installed-battery-capacity` shows the
actual installed capacities in ERCOT from the low battery cost
sensitivity scenario (discussed further in the results section). For
each battery storage duration available to the model, installed battery
capacity as well as the resource adequacy contribution determined by the
model are shown. This resource adequacy contribution is the result of
the model optimizing all grid services storage can provide, with
capacity credit of all storage subject to the constraints of the peaking
capacity limits from {numref}`figure-storage-peak-capacity-determination`.

```{figure} ../../images/installed-battery-capacity.png
:name: figure-installed-battery-capacity

Installed battery capacity and resource adequacy contribution (capacity derated by capacity credit) in ReEDS.
Model results for ERCOT in 2050.
```

This dynamic assessment of storage capacity credit enables the model to
identify the limitations of energy storage to provide peaking capacity.
It allows the model to identify the benefits, if they exist, of
deploying short-duration resources at reduced capacity credit for energy
arbitrage purposes or other grid services captured in the model.
Alternatively, the model is also free to deploy longer-duration storage
even when shorter durations would receive full capacity credit if this
leads to a least-cost solution for meeting all grid services. It also
allows the model to respond to changes in net load shape from wind and
PV deployment. The capacity credit of storage can change from one solve
year to the next as a result of these net load profile shape
changes.

Peaking capacity potential for longer durations of storage are also
assessed within the model. The potential for 12- and 24-hour storage is
included in the assessments described in {numref}`figure-energy-capacity-requirements-for-storage` 
and {numref}`figure-storage-peak-capacity-determination`. This
is meant to accommodate the potential to derate the capacity credit of
ten-hour batteries and capture the capacity credit of pumped-hydro and
compressed-air energy storage (which are assumed to have 12 hours of
duration in ReEDS).

After this potential is determined, the actual storage capacity credit
in ReEDS is determined within the optimization. The durations of storage
devices that are installed by the model are evaluated based on the
peaking capacity potential of storage ({numref}`figure-energy-capacity-requirements-for-storage`). When determining the
contribution of storage toward resource adequacy, two constraints were
added to the model to make the capacity credit of storage dynamic and
flexible to the many changes in the system that can affect storage
capacity credit. The constraints for the formulation of storage capacity
credit in ReEDS are as follows:

$$\sum_{pd}^{}{C_{pd,id} = C_{id}}$$

$$\sum_{id}^{}{C_{pd,id}*{cc}_{pd,id} \leq L_{pd}}$$

where L is the limit of peaking storage capacity (i.e. the megawatt
values from Figure 5), C is the installed storage capacity, id is the
duration of installed storage, pd is the duration of the peak demand
contribution being considered, and cc is the capacity credit of an
installed duration (id) of storage when applied to a specific peaking
duration (pd). Storage capacity credit is equal to installed duration /
peak duration, with a maximum of 1. For each duration of installed
storage id, its capacity can contribute to any duration of peak demand
pd, but the total installed storage capacity C<sub>id</sub> must be
equal to the sum of its contributions toward each duration of peak
demand. And for each duration of peak demand pd, the total contribution
of each installed duration id of storage capacity (adjusted for their
capacity credit cc) cannot exceed the limit of peaking storage capacity
L of that pd.

For example, consider a simple example where there is 100 MW of peaking
storage potential for each storage duration considered in ReEDS: two,
four, six, eight, ten, 12, and 24 hours. In this example, 200 MW of
two-hour storage, 100 MW of four-hour storage, and 50 MW of six-hour
storage are already installed. The model would optimize the capacity
credit of storage by giving 100 MW of two-hour storage full capacity
credit for its two-hour contribution, the 100 MW of four-hour storage
full capacity credit for its four-hour contribution, and the 50 MW of
six-hour storage full capacity credit for its six-hour contribution
({numref}`figure-storage-capacity-credit-allocation-example`). In this example, 
the peaking potential limit of two- and
four-hour storage have been reached, so the remaining 100 MW of two-hour
storage would receive a capacity credit of 1/3 and contribute 33.3 MW
for its six-hour peak demand contribution. The model could then build
16.7 MW of six-hour storage at full capacity credit, at which point the
potential for six-hour storage to meet peak demand would be reached as
well. The model would then be able to build two-, four-, or six-hour
storage at a derated capacity credit with their contribution going
toward the eight-hour peak demand “bin,” or it could build 8-hour
storage with full capacity credit.

```{figure} ../../images/storage-capacity-credit-allocation-example.png
:name: figure-storage-capacity-credit-allocation-example

An example of storage capacity credit allocation in ReEDS.
200 MW of 2-hour batteries exist but there is only 100 MW of 2-hour
peaking capacity potential. Since there is also 100 MW of 4-hour
batteries serving all 100 MW of 4-hour peaking storage potential, the
remaining 100 MW of 2-hour storage provides 33.3 MW towards the 6-hour
peaking storage potential.
```

Now consider the same example but in addition to the two-, four-, and
six-hour storage installed, there is also 300 MW of pumped-hydro storage
in this region ({numref}`figure-storage-capacity-credit-allocation-example2`). 
Pumped-hydro storage in ReEDS has a duration
of 12 hours, but the potential for 12-hour storage to serve peak demand
is only 100 MW. Rather than giving the remaining 200 MW of pumped-hydro
a capacity credit of ½ for its contribution to the 24-hour peak demand
period, it is optimal for the model to fill the 10- and 8-hour peak
demand “bins” with the remaining pumped-hydro capacity at full capacity
credit since there is no other storage allocated to those peak demand
periods. Now, after the model builds 16.7 MW of six-hour storage at full
capacity credit, the 8-, 10-, and 12-hour bins are already filled by
pumped-hydro storage. So, if the model wants to build additional storage
capacity, it will shuffle around the allocated storage capacity to the
optimal “bins” as it fills the 24-hour bin. In this example, if any
8-hour storage is built it will be allocated to the 8-hour bin and some
pumped-hydro capacity will be pushed out of that bin and re-allocated to
the 24-hour bin at ½ capacity credit (12 hours / 24 hours). So, even
though the duration required for storage to receive full capacity credit
at this point is 24 hours, 8-hour storage would receive a marginal
capacity credit of ½ because there is an excess of 12-hour storage
already installed in the system.

```{figure} ../../images/storage-capacity-credit-allocation-example2.png
:name: figure-storage-capacity-credit-allocation-example2

The same example from {numref}`figure-storage-capacity-credit-allocation-example` but this time with 300 MW of 12-hour pumped hydro storage. Since there is only 100 MW of 12-hour peaking potential, remaining pumped-hydro capacity is allocated to serve shorter peak durations.
```

Storage capacity credit is sensitive to a variety of factors on the
power system, so rather than ignoring the many factors that can
influence storage capacity credit we simply pass the model information
on what storage *could* do to serve peaking capacity based on load shape
and storage duration and then allow the model to choose the least-cost
option based on the suite of available resources and the entire set of
storage revenue streams that are represented within the ReEDS
model.

Denholm et al. {cite:year}`denholmPotentialBatteryEnergy2019` and Frazier et al. {cite:year}`frazierAssessingPotentialBattery2020` demonstrated how the
storage peaking potential of storage interacts with VRE
penetration.


#### "Stress periods” formulation

- Thematic overview
    - Use the same dispatch constraints as representative
periods, but:
        - Scale up load by PRMN
        - No weighting to hours (so they don’t
count toward VOM costs, fuel costs, emissions constraints; same as
capacity credit)
        - Inter-period operation of storage is not currently
supported
    - ReEDS2PRAS
        - Typical generator sizes
        - PRAS – probabilistic outages
    - Stress metrics and iteration
    
Several shortcomings arise under the capacity credit-based approach for 
evaluating resource adequacy. In
ReEDS, planning resource can be traded between the Federal Energy
Regulatory Commission (FERC) Order 1000 regions, however the capacity
credit is still assessed where the resource is sited, misrepresenting
the evaluation for some generation assets. Additionally, identifying
stress periods using peak net load hours can potentially miss system
stress that results from events spanning consecutive days, such as
extreme weather. The alternative stress period formulation in ReEDS
attempts to mitigate some of these deficiencies. In this approach, a
probabilistic resource adequacy suite (PRAS) developed by NREL is
brought into the loop, allowing ReEDS to pass the system design to the
resource adequacy model after every solve year. The PRAS model is
described in a separate publication \[42\] , but its use in conjunction
with the ReEDS model is included briefly here. Essentially PRAS ingests
the ReEDS build out and utilizes 7 years of load and weather data to
identify the periods with the highest risk of unserved energy, these
periods are then passed back to ReEDS to ensure sufficient capacity is
built. Within PRAS the expected unserved energy is evaluated by running
a sequential Monte Carlo model to simulate the probability of individual
assets failing over the full multi-year optimization horizon producing
results for unserved energy. The simulation is run for multiple outage
draws after which the collective system stress periods can be
identified.


#### Planning Reserve Margins

The planning reserve margin fractions applied in ReEDS are based on
reserve margin requirements for NERC reliability subregions {cite}`nerc2010LongtermReliability2010`
(see {numref}`figure-offshore-wind-resource`). Each ReEDS BA must meet the requirement, but regions can
engage in bilateral contracts for firm capacity subject to transmission
limits on AC or DC corridors. The planning reserve margin is enforced
seasonally such that each BA much meet the reserve margin requirement in
each of the four seasons.

The planning reserve margin is constant over time for all regions
except ERCOT. Because ERCOT was below its NERC-recommended level in
2018-2020, the ERCOT reserve margin is set to the actual levels of 10.9%
and 8.6% for 2018 and 2019, respectively, and at the projected level of
10.6% for 2020 {cite}`ercotNewsReleaseERCOT2019`. The years from 2021 and onward are set at
13.75%, and future planning reserve margin levels are anticipated to
meet or exceed that target from 2021 and
onward.


### Operational Reliability

In addition to ensuring adequate capacity to satisfy long-term planning
reserve requirements, ReEDS requires operational reliability—that is,
the ability to continue operating the bulk-power system in the event of
a sudden disturbance {cite}`nercGlossaryTermsUsed2016`. In practice, ancillary reserve
requirements ensure there is sufficient flexibility from supply-side and
demand-side technologies to rebalance fluctuations in generation and
demand.

ReEDS represents three type of operating reserve products, including,
spinning, regulation, and flexibility reserves {cite}`coleOperatingReservesLongTerm2018`. The requirement specified for each product in each time-slice is
a function of load, wind generation, and photovoltaic capacity (during
daytime hours).[^ref47] Technologies providing these reserve products must
be able to ramp their output within a certain amount of time ({numref}`operating-reserve-reqs`).

```{table} Summary of Operating Reserve Requirements
:name: operating-reserve-reqs

| Reserve Product | Load Requirement (% of load)<sup>a</sup> | Wind Requirement (% of generation)<sup>b</sup> | PV Requirement (% of capacity)<sup>b</sup> | Time Requirement to Ramp (minutes) |
|----|---:|---:|---:|---:|
| Spinning | 3% | — | — | 10 |
| Regulation | 1% | 0.5%<sup>c</sup> | 0.3%<sup>c</sup> | 5 |
| Flexibility | — | 10% | 4% | 60 |
```

<sup>a</sup> See Lew et al. {cite:year}`lewWesternWindSolar2013`.  
<sup>b</sup> Reserve requirements for wind and PV are derived from the
outcomes from Lew et al. {cite:year}`lewWesternWindSolar2013`. The flexibility requirement for wind is
estimated as the ratio of the change in the reserve requirement to the
change in wind generation from the Lew et al. High Wind scenario; the
requirement was estimated similarly for PV using the Lew et al. High
Solar scenario.  
<sup>c</sup> The estimated regulation requirements (0.5% wind generation
and 0.3% PV capacity) are based on incremental increases in regulation
reserves across all scenarios in Lew et al.
{cite:year}`lewWesternWindSolar2013`.

All ancillary reserve requirements must be satisfied in each BA for
each time-slice; however, reserve provision can be traded between BAs
using AC transmission corridors. Trades are only allowed within an RTO
and not across RTO boundaries. The amount of reserves that can be traded
is limited by the amount of carrying capacity of an AC transmission
corridor that is not already being used for trading
energy.

The ability of technologies to contribute to reserves is limited by the
ramping requirement for a given reserve product, the plant ramp rate,
and online capacity ({numref}`generation-techs-flexability-params`). Online capacity is approximated in ReEDS
as the maximum generation from all time-slices within a modeled day.
Reserves can be provided by generation and storage technologies that are
turned on but not fully dispatched in a time-slice. In addition,
demand-side interruptible load can also contribute to reserve
requirements, if enabled in a scenario. Nuclear, PV, and wind are not
allowed to contribute toward the supply of
reserves.

The cost for providing regulation reserves is represented in ReEDS
using data from {cite}`hummonFundamentalDriversCost2013`; see {numref}`cost-regulation-reserves`. Because ReEDS does
not clearly distinguish between coal fuel types, \$12.5/MWh is the
assumed regulation cost for all coal technologies. The cost of providing
regulation reserves from Gas-CT, geothermal, biopower, land-fill gas,
and CAES is assumed to be the same as oil/gas
steam.

```{table} Flexibility Parameters of the ReEDS Generation Technologies
:name: generation-techs-flexability-params

|  | Assumed Ramp Rate (%/min) | Upper Bound (% of online capacity) = Ramp Rate (%/min) × Ramp Requirement (min) |  |  |
|----|:--:|:--:|:--:|:--:|
|   |  | Spinning | Regulation | Flexibility |
| Gas-CT<sup>a</sup> | 8 | 8×10=80 | 8×5=40 | 8×60=480, so 100 |
| Gas-CC<sup>a</sup> | 5 | 5×10=50 | 5×5=-25 | 5×60=300, so 100 |
| Coal<sup>a</sup> | 4 | 4×10=40 | 4×5=20 | 4×60=240, so 100 |
| Geothermal<sup>b</sup> | 4 | 4×10=40 | 4×5=20 | 4×60=240, so 100 |
| CSP with Storage<sup>c</sup> | 10 | 10×10=100 | 10×5=50 | 10×60=600, so 100 |
| Biopower<sup>b</sup> | 4 | 4×10=40 | 4×5=20 | 4×60=240, so 100 |
| Oil/Gas Steam<sup>a</sup> | 4 | 4×10=40 | 4×5=20 | 4×60=240, so 100 |
| Hydro | 100 | No Upper Bound | No Upper Bound | No Upper Bound |
| Storage | 100 | No Upper Bound | No Upper Bound | No Upper Bound |
```

<sup>a</sup> See {cite}`bloomEasternRenewableGeneration2016`.  
<sup>b</sup> Geothermal and biopower values are assumed to be the same
as oil/gas steam units. In practice, geothermal plants typically do not
ramp given their zero or near-zero variable costs, and therefore only
provide energy and not operating reserves.  
<sup>c.</sup> See {cite}`jorgensonEstimatingPerformanceEconomic2013`.

```{table} Cost of Regulation Reserves
:name: cost-regulation-reserves

| Generator Type              | Cost of Regulation Reserves (2013$/MWh) |
|-----------------------------|----------------------------------------|
| Supercritical Coal          | 15                                     |
| Subcritical Coal            | 10                                     |
| Combined Cycle              | 6                                      |
| Gas/Oil Steam               | 4                                      |
| Hydro                       | 2                                      |
| Pumped Storage Hydropower   | 2                                      |
```


## Climate Impacts

Previous versions of ReEDS, including the 2018 version {cite}`cohenRegionalEnergyDeployment2019`, 
included a representation of climate impacts, and Section 7 of
the 2018 ReEDS documentation describes that capability. Recent changes
to the ReEDS time resolution are not compatible with the former climate
impacts representation, and it is expected that ReEDS climate impacts
capabilities will be restored for the 2024 model
version.


## Policy Descriptions

Policies modeled in ReEDS include federal and state-level emission
regulations, tax incentives, and portfolio standards. This section
primarily focuses on existing policies, but additional frameworks 
that exist in the model are discussed in [Other Policy Capabilities](#other-policy-capabilities).


### Federal and State Emission Standards
#### Cross-State Air Pollution Rule

ReEDS applies the Cross-State Air Pollution Rule (CSAPR) using caps on
power plant emissions to the states in the eastern half of the United
States over which the rules are imposed. From 2017 onward, CSAPR annual
emission allowance budgets for NO<sub>x</sub> are applied at the state
level using the Phase 2 caps {cite}`epaEGRID2007Version1Year2008`. The caps are applied only
during the ozone season. ReEDS applies a seasonal estimate of these
ozone season caps that adjusts for the overlap of ReEDS season
definitions and ozone season definitions. States can trade allowance
credits within the eligible trading groups, but must keep emissions
below the required assurance levels.

Sulphur Dioxide (SO<sub>2</sub>) emission limits are not represented in
the model because the caps would not be binding in the model except in
historical years.


#### Mercury and Air Toxic Standards

Because compliance with the Mercury and Air Toxic Standards (MATS) has
already been largely achieved, we do not represent MATS in the ReEDS
model.


#### California Carbon Cap

California’s Global Warming Solution Act of 2016 (referred to as
Assembly Bill 398 or AB 398) established a program to reduce
economy-wide greenhouse gas emissions to 1990 levels by 2020. In 2016,
legislation was passed that codified the 2030 greenhouse gas target to
40% below 1990 levels. In ReEDS, these state carbon caps are modeled as
a cap on electricity-system CO<sub>2</sub> emissions from generators
either located in California or serving load in the state. Direct
CO<sub>2</sub> emissions from generators located in California count
toward the cap. Imported electricity is assumed to have a emissions rate
of 0.26 ton CO<sub>2</sub>/MWh {cite}`carbCaliforniaGreenhouseGas2019`.

Because California’s greenhouse gas reduction targets are legislated
for all economic sectors while ReEDS only models the electricity sector,
we rely on published economy-wide modeling results to estimate electric
sector-specific caps that are used in ReEDS. In particular, we apply
power sector caps based on the annual CA electric sector emissions (from
in-state and imported electricity) from California Public Utilities
Commission {cite}`cpucDecisionSettingRequirements2018`, which provides guidance for a 42 million
tCO<sub>2</sub> cap by 2030. We enforce that cap from 2030 to 2050. The
pre-2030 cap ramps linearly from 60 million tCO<sub>2</sub> in 2020 to
the 42 million tCO<sub>2</sub> in 2030. Note that we also model
California’s RPS policy.


#### Regional Greenhouse Gas Initiative

The Regional Greenhouse Gas Initiative (RGGI) cap-and-trade program
limits the CO<sub>2</sub> emissions for fossil fuel-fired power plants
in eleven states: Connecticut, Delaware, Maine, Maryland, Massachusetts,
New Hampshire, New Jersey, New York, Rhode Island, Vermont, and
Virginia.

We enforce allowance budgets from the updated model rule adopted in
2017.[^ref48] We ignore the provision for privately banked allowances and
therefore use the unadjusted budgets: 165 million short tons in 2012
declining to 91 million by 2014, then declining 2.5% per year from 2015
to 2020. According to the 2017 Model Rule, the 2021 cap is set at 75
million short tons and decreases by 2.275 million tons per year until
2030. Beginning in 2020, we also enforce an additional budget of 18
million short tons for the addition of New Jersey to the set of states
included in the RGGI[^ref49]. The budget for New Jersey is set to decline
by 30% through 2030[^ref50]. Similarly, beginning in 2021, we apply an
additional cap of 27.16 million short tons for the addition of Virginia
as a RGGI state. This cap is set to decline at a rate of 0.84 short tons
per year.[^ref51] We assume the budget remains constant beyond 2030. We do
not model banking of allowances, emissions offsets, or recycling of
initiative allowance revenues.


### Federal and State Tax Incentives
#### Federal Tax Credits for Clean Electricity and Captured Carbon

Existing federal tax incentives are included in ReEDS, aligned with the
Inflation Reduction Act of 2022 (IRA). These include the PTC and the ITC
for clean electricity, the 45U credits for existing nuclear generation,
the 45Q credit for capturing and storing carbon, and the Modified
Accelerated Cost Recovery System (MACRS) depreciation schedules. [^ref52]
Current technology-specific depreciation schedules are modeled for all
years, because we assume they are permanent parts of the tax
code.

Four clean electricity production and investment tax credits are
represented in ReEDS:

- **Clean Electricity Production Tax Credit (PTC):** \$26/MWh for 10
years (2022 dollars) plus a bonus credit that starts at \$1.3/MWh and
increases to \$2.6/MWh by 2028 
- **Clean Electricity Investment Tax Credit (ITC):** 30%, plus a bonus credit that starts at an additional 5% and
increases to 10% by 2028 (for totals of 35% and 40% respectively)
- **Captured CO<sub>2</sub> Incentive (45Q):** \$85 per metric ton of
CO<sub>2</sub> for 12 years for fossil-CCS and bioenergy-CCS, and \$180
per metric ton of CO<sub>2</sub> for 12 years for direct air capture;
nominal through 2026 and inflation adjusted after that
- **Existing Nuclear Production Tax Credit (45U):** This tax credit is \$15/MWh (2022
dollars), but it is reduced if the market value of the electricity
produced by the generator exceeds \$25/MWh. As a simplification, this
dynamic calculation was not directly represented in ReEDS. Instead, to
represent the effect of this provision, existing nuclear generators are
not subject to economic retirement in ReEDS through 2032. 


Note that IRA allows for bonus credits for both the clean electricity PTC and ITC (but
not applicable to 45U or 45Q) if a project either meet certain domestic
manufacturing requirements or is in an “energy community.” Projects can
obtain both bonus credits if they meet both requirements, which would
equate to \$5.2/MWh for the PTC and 20% for the ITC. In ReEDS, we assume
projects will, on average, capture one of the bonus credits by 2028, the
value of which is expressed in the summary above. In practice, there
will likely be greater diversity of captured credits amongst projects.
Relatedly, the values above are based on the assumption that all
projects will meet the prevailing wage
requirements.

Under IRA, eligible clean electricity projects can select whether to
take the PTC or the ITC. As implemented in ReEDS, however, an a priori
analysis was performed to estimate which credit was most likely to be
more valuable, and the technology was assigned that credit. The
assignments are:

- **PTC:** Onshore wind, utility-scale PV, and biopower 
- **ITC:** Offshore wind, CSP, geothermal, hydropower, new nuclear, pumped storage
hydropower, distributed PV, and batteries. 

As represented in ReEDS, the
value of the tax credits is reduced by 10% for non-CCS technologies and
7.5% for CCS technologies, as a simple approximation of the costs of
monetizing the tax credits (such as tax equity financing).[^ref53] These
cost penalties are not reflected in the values given for each incentive
above.

The clean electricity PTC and ITC are scheduled to start phasing out
when electricity sector greenhouse gas emissions fall below 25% of 2022
levels, or 2032, whichever is later. Once the tax credits phase out,
they remain at zero—there is no reactivation of the credits if the
emissions threshold is exceeded at a later point. The exact value of the
threshold that would trigger the IRA clean electricity tax credits
phasing out has not been announced but is estimated at 386 million
metric tons of CO<sub>2</sub>e in this modeling. The 45Q and 45U credits
do not have a dynamic phaseout and are instead just scheduled to end at
the end of 2032.

In the dGen model, distributed PV was assumed to take an ITC: the 25D
credit for residential, and the Section 48 credit for commercial and
industrial. For residential projects placed in service through 2032 the
ITC was assumed to be 30%, declining to zero for projects placed in
service in 2036. For commercial and industrial projects coming online
through 2035 the ITC was assumed to be 40%, dropping to zero after that.
These representations are simplifications, as there can be greater
diversity in captured value depending on factors such as ownership type
and tax status. Furthermore, due to limitations of the models used in
this study, the dynamic phase-out of the Section 48 ITC was not
reflected. In practice, most scenarios did not cross the emissions
threshold specified in IRA at this point, and therefore the adoption of
commercial and industrial distributed PV in the later years of those
scenarios was potentially underestimated.

IRA includes additional bonus credits (up to 20%) for up to 1.8 GW per
year for solar facilities that are placed in service in low-income
communities. The dGen model runs used in this analysis did not have an
explicit representation of that additional bonus credit. Instead, 0.9 GW
per year of distributed PV was added to the original dGen estimates
through 2032. The estimate of 0.9 GW reflects the assumption that some
of the projects capturing the bonus credit may not be additional (i.e.,
they would have occurred anyway even if the bonus credit was not
available).

All the IRA tax credits are assumed to have safe harbor periods,
meaning a technology can capture a credit as long as it started
construction before the expiration of the tax credit. The maximum safe
harbor periods are assumed to be 10 years for offshore wind, 6 years for
CCS and nuclear, and 4 years for all other technologies. Generators will
obtain the largest credit available within their safe harbor window,
meaning that once a credit starts to phase down or terminate, ReEDS
assumes that efforts were made to start construction at the maximum
length of the safe harbor window before the unit came online. In
practice this means ReEDS will show generators coming online and
capturing the tax credits for several years beyond the nominal year in
which they expired.


### State Renewable Portfolio Standards

ReEDS models state RPSs, including technology set-asides and renewable
energy certificates (RECs) that can count toward RPS compliance. RPS
rules are complex and can vary significantly between states. The RPS
representation in ReEDS attempts to model the primary impacts of these
RPS rules but includes many simplifying assumptions. In addition, in
recent years there have been numerous changes to RPS legislation. We
periodically update our representation to capture the recent changes to
the legislation; however, the numerous and frequent changes to state
laws create challenges to having a precise representation of all RPS
legislation.

{numref}`cost-regulation-reserves` shows the respective RPS targets and technology set-asides for
years 2020, 2030, and 2050 as a percentage of state electricity sales as
modeled within ReEDS. These values—along with many other data that we
use to represent nuanced RPS rules—are based on data compiled by
Lawrence Berkeley National Laboratory, which takes into account the
in-state REC multiplier incentives and load adjustments (e.g.,
sales-weighted RPS targets considering different load-serving entities
subject to compliance, such as investor-owned utilities, municipal
utilities, and cooperatives).[^ref54] Solar includes UPV and ro­oftop PV,
wind includes both land-based and offshore technologies, and distributed
generation (DG) includes rooftop PV and ground-mounted PV systems
located within the distribution network.[^ref55] ReEDS also models
alternative compliance payments for unmet RPS requirement for both main
RPS targets and solar set-asides as is consistent with the available
data.<sup>69</sup>

Technology eligibility for state RPS requirements is appropriately
modeled for each state.<sup>69</sup> For instance, California’s RPS does
not allow in-state rooftop solar technologies to contribute toward its
RPS. Additionally, every state has specific rules regarding hydropower
generation’s eligibility toward contributing RECs, which are usually
based on each unit’s vintage and size (e.g., small hydro with specific
capacity cut-offs are eligible in some states). ReEDS models these as
allowable generation fractions from Barbose {cite:year}`barboseStateRenewablesPortfolio2023`, 
which is imposed on each state’s total hydropower generation thereby limiting
the amount of hydropower RECs that each state could produce.

{numref}`cost-regulation-reserves` also lists the allowable states from which each state may
import RECs; interstate REC transactions that are required to be bundled
with energy are marked with an asterisk. Except for California, ReEDS
enforces an upper limit on the total RECs (both bundled and unbundled)
that can be imported for that state’s RPS compliance. For California
alone, due to its unique out-of-state rules, ReEDS enforces two upper
limits, one on the total unbundled REC imports and the other on the
total bundled REC imports. There is a myriad of possibilities of
interstate REC transactions, in terms of both which two states can
transact and the quantity of those transactions. To constrain the
solution space of ReEDS to credible values, the interstate REC trading
modeling is based on historical observations {cite}`holtPotentialRPSMarkets2016`, as shown in
the final two columns of {numref}`cost-regulation-reserves`. The out-of-state total REC import
percentages for each state in are limited to those observed in 2012–2013
{cite}`heeterCrossstateRPSVisualization2015`.

Several states have implemented policies directed at offshore wind. To
represent these actions in ReEDS, we prescribe a floor to offshore wind
capacity based on known projects and policy mandates. Specifically, we
include offshore wind capacity that meets at least one of three
criteria: (1) currently operating capacity; (2) projects in active
solicitation processes; and (3) to meet statutory policy requirements.
The projects are based on tracking conducted for the NREL Offshore Wind
Technologies Market Report and state totals are shows in {numref}`offshore-wind-capacity`.
The model allows for economic deployment of offshore wind capacity beyond
these levels. All prescribed offshore wind projects are assumed to be
rebuilt once they are retired.

Finally, voluntary renewable energy credits are also represented in
ReEDS. Only renewable energy technologies are allowed to supply
voluntary RECs, and Canadian imports are not allowed.
The voluntary REC requirement is based on the
observed amount of voluntary RECs from Heeter et al. {cite:year}`heeterStatusTrendsVoluntary2021`
and the requirement is assumed to grow by the smallest amount that has been
observed year-over-year (0.1624% in absolute terms). The voluntary
requirement includes an alternative compliance payment of \$10/MWh (in
2004\$).

```{table} Cumulative Offshore Wind Capacity (MW) Mandated in ReEDS
:name: offshore-wind-capacity

| State | 2020 | 2030 | 2040 | 2050 |
|----|---:|---:|---:|---:|
| CA | — | 3,100 | 4,707 | 4,707 |
| MA | — | 4,092 | 6,492 | 6,492 |
| MD | — | 5,044 | 8,500 | 8,500 |
| ME | — | 144 | 144 | 144 |
| NC | — | 2,800 | 2,800 | 2,800 |
| NJ | — | 5,100 | 11,000 | 11,000 |
| NY | — | 4,362 | 9,000 | 9,000 |
| RI | 30 | 1,538 | 1,538 | 1,538 |
| VA | 12 | 2,599 | 5,200 | 5,200 |
| Total | **42** | **28,779** | **49,381** | **49,381** |
```


### 9.4. 9.4 Clean Energy Standards

As of July 2023, 15 states had clean energy standards (CESs) (see Table
29). CES values are effective values[^ref56] and are taken from Barbose
{cite:year}`barboseStateRenewablesPortfolio2023`. These CESs are in effect 
generalized versions of RPSs; their model representations are very similar
with technology eligibility being the only difference. For all but one of 
the CES policies (Massachusetts), we assume all zero-carbon-emitting sources
(on a direct emissions basis) can contribute to the CES requirement. This 
includes all renewable energy technologies (including hydropower and distributed
PV), nuclear power, and imports from Canada.[^ref57] The modeled CES
policies set a floor on electricity generated from clean energy
technologies but does not cap generation from nonclean sources. As a
result, in the model representation, a state can continue to generate
from existing fossil plants if the amount of clean energy generation
exceeds the requirement (even if the requirement approaches 100% of
sales). Most of the CES policies are assumed to start in 2030 and ramp
to their final targets by 2040 or 2050.[^ref58] For other aspects of the
CES model representation, we use the same assumptions as the
corresponding state RPS. These include assumptions about credit trading
and variations in load-serving entity requirements. In the case of
Virginia, fossil plants are required to retire per the schedule
indicated in the clean energy policy.[^ref59] Based on discussions with
stakeholders, fossil plants in Illinois and New York are also required
to retire once the policy reaches the nominal 100%
target.

```{table} Clean Energy Requirement as a Percentage of In-State Sales
:name: clean-energy-req

| **State** | **2020** | **2025** | **2030** | **2035** | **2040** | **2045** | **2050** |
|----|---:|---:|---:|---:|---:|---:|---:|
| CA | 0% | 0% | 55% | 70% | 85% | 100% | 100% |
| CO | 19% | 32% | 44% | 47% | 50% | 52% | 55% |
| MA | 20% | 28% | 37% | 45% | 54% | 63% | 71% |
| NM | 0% | 0% | 45% | 60% | 75% | 90% | 100% |
| NY | 0% | 0% | 75% | 87% | 100% | 100% | 100% |
| WA | 0% | 0% | 80% | 87% | 93% | 100% | 100% |
| VA | 0% | 24% | 39% | 56% | 76% | 96% | 100% |
```

### Storage Mandates

Seven state storage mandates are represented in ReEDS. The storage
mandate are summarized in {numref}`energy-storage-mandates`. The mandates are required to be met
with battery storage, and any duration of storage
qualifies.

```{table} Energy storage mandates, with required capacity listed in MW.
:name: energy-storage-mandates

| **State** | **2020** | **2030** | **2050** |
|----|:--:|:--:|:--:|
| CA | 1,325 | 2,325 | 2,325 |
| MA | 50 | 50 | 50 |
| NJ | 600 | 2,000 | 2,000 |
| NV |  | 1,000 | 1,000 |
| NY | 500 | 3,000 | 3,000 |
| OR | 2.5 | 2.5 | 2.5 |
| VA | 42.7 | 1,350 | 3,100 |
```


### Nuclear Power Plant Policies

There are four states that have enacted that provide compensation or
other assistance for in-state nuclear power plants: Connecticut,
Illinois, New Jersey, and New York. For these states, the nuclear power
plants are not allowed to retire until after the policy expires, unless
the power plant already has an announced retirement date. The policy
end-dates are taken from EIA {cite:year}`eiaElectricPowerMonthly2019a`.

Additionally, there are several states that do not allow new nuclear
power.[^ref60] These states include California, Connecticut, Illinois,
Maine, Massachusetts, Minnesota, New Jersey, New York (Long Island
only), Oregon, Rhode Island, and Vermont.


### Other Policy Capabilities
In addition to the existing policies described above, ReEDS also
includes several optional policy implementations that are useful for
exploring alternative futures or the impact of existing policies. These
additional policy frameworks include:

- **National Clean Energy Standard:** This framework allows the user to
  specify which technologies count as “clean energy” and enforce a
  minimum limit for the penetration of these clean energy
  technologies.

- **National Renewable Portfolio Standard:** This standard enforces a
  national RPS, with the RPS trajectory defined by the
  user.

- **Carbon Cap-and-Trade:** This feature allows the user to specify
  national-or subnational carbon cap-and-trade policies, including
  options to represent trading limitations and banking and borrowing of
  allowances.

- **Carbon Tax:** This feature implements a user-specified carbon tax
  on burner-tip emissions from the power
  sector.

- **National Emissions Limit:** This framework limits the total
  national emissions according to user-specified values. The limit is
  often referred to as a carbon cap or CO<sub>2</sub>
  cap.

- **Alternative ITC and PTC Schedules:** In addition to the ITC and PTC
  schedules described in [Federal and State Tax Incentives](#federal-and-state-emission-standards),
  the ITC and PTC can be modified to apply for any number of years and to any
  technology.

- **Alternative Financing Measures:** Policy-related financing impacts
  such as MACRS or the under-construction provisions for the ITC and PTC
  can be modified as specified by the user.


## Capital Financing, System Costs, and Economic Metrics
### Financing of Capital Stock

The financing assumptions used in ReEDS are taken directly from the
2023 ATB spreadsheet {cite}`nrel2023AnnualTechnology2023`, using the 
“Market Factor Financials” and the 20-year capital recovery period options. 
The ATB has technology-specific and time-varying financing parameters, 
including interest rate, rate of return on equity, debt fraction, and tax 
rate. Other elements of the ATB included in ReEDS include construction
schedules, MACRS depreciation schedules, and inflation rates. These
values are further defined and explained in the ATB, with additional
explanation of our financing implementation detailed in the Capital Cost
Financial Multipliers appendix of this
document.

In previous versions of ReEDS, technology-specific costs of capital
were reflected through technology-specific discount rates. Due to the
different model structure of the intertemporal mode, and the desire to
keep the financial representations the same between modes, since the
2019 version the model has had only a single technology-agnostic
discount rate. Instead of varying the discount rate, the impact of any
difference between a technology’s weighted average cost of capital
(WACC) and the system average WACC is captured in a lump-sum adjustment
that represents the present-value of the higher (or lower) return to
capital. This representation implicitly assumes that differences in
financing terms primarily come from diversifiable risk, as opposed to
non-diversifiable risk.


### Electric Sector Costs

Two system-wide cost metrics are calculated from each ReEDS run: a
present value of direct electric sector system costs and electricity
price. These cost calculations are not part of the ReEDS optimization
process; they are calculated after the ReEDS optimizations have been
conducted. ReEDS also includes a postprocessing option for estimating
the health costs of air pollution, described further
below.


#### Present Value of Direct Electric Sector Cost

The present value system cost metric accounts for capital and operating
expenditures incurred over the entire study horizon for all technology
types considered, including generation, transmission, and storage. The
cost in each future year is discounted by a user-defined discount rate,
and by default it is set to 5%. Not to be confused with the discount
rate used in the optimization for investment decisions, the *investment*
discount rate is selected to represent private-sector investment
decisions for electric system infrastructure, and it approximates the
expected market rate of return of investors. All costs incurred before
the start of the specified economic horizon are assumed to be sunk and
are therefore not included in the system cost metric. Details about how
the system costs are calculated in ReEDS can be found in the Present
Value of Direct Electric Sector Cost section of the
appendix.


#### Electricity Price

ReEDS calculates “competitive” electricity prices at different regional
aggregation levels 
{cite:p}`murphyGenerationCapacityExpansion2005, ventosaElectricityMarketModeling2005, eiaAnnualEnergyOutlook2017a`. This calculation takes advantage of the linear programming
formulation of the model. Specifically, the marginal price on a model
constraint represents how much the objective function would change given
a change in the right side of the constraint. Each constraint can be
viewed as a market with a marginal price and quantity. At optimality,
the total revenue (i.e., the product of price and quantity) across all
constraints equals the objective function value. The constraints within
ReEDS are written such that the marginal values from the load
constraints can be used as a proxy for the competitive electricity
price. The load constraints are linked to the supply-demand balance
constraints, capacity constraints, operating reserve constraints, and
others through load variables. Taking the marginal value from the load
balance constraint, we can find the marginal value of an additional unit
of load (e.g., MWh) to the system, accounting for other requirements.
Specifically, the reported competitive prices in ReEDS capture five
categories of requirements, including energy, capacity, operating
reserves, and state-level and national-level RPS requirements (see Table
31). The competitive prices can be reported at different regional
aggregation level, scaled by requirement quantities. Details about how
these prices are calculated in ReEDS can be found in the Marginal
Electricity Prices section of the appendix.

```{table} Relationships of Constraints to Grid Services Used to Calculate the Competitive Electricity Price
:name: grid-service-constraints

| Constraint Category | Grid Service (s)      | Region (r)  | Time (h)    | Units - Price (p_srht) | Units - Quantity (q_srht) |
|---------------------|-----------------------|-------------|-------------|------------------------|---------------------------|
| Operation           | Energy                | BA          | Time-slice  | $/MWh                  | MWh                       |
| Operation           | Flexibility Reserve   | BA          | Time-slice  | $/MW-h                 | MW-h                      |
| Operation           | Regulation Reserve    | BA          | Time-slice  | $/MW-h                 | MW-h                      |
| Operation           | Spinning Reserve      | BA          | Time-slice  | $/MW-h                 | MW-h                      |
| Resource Adequacy   | Capacity              | BA          | Season      | $/kW-yr                | kW                        |
| Policy              | State RPS             | State       | Annual      | $/MWh                  | MWh                       |
| Policy              | National RPS          | National    | Annual      | $/MWh                  | MWh                       |
| Policy              | CO2 Cap               | National    | Annual      | $/metric ton           | metric ton                |
| Policy              | RGGI CO2 Cap          | Regional    | Annual      | $/metric ton           | metric ton                |
| Policy              | SB32 CO2 Cap          | Regional    | Annual      | $/metric ton           | metric ton                |
```

Besides “competitive electricity prices”, ReEDS also calculates the
average cost of electricity at the national, BA-level or state-level by
taking the annualized total costs of building and operating the system
in a specific geographic area and divided that by the electricity load
in that area. Annualized costs for existing (i.e., pre-2010) power
plants are also considered given plants’ initial investment costs and
the built year. BA-level average electricity prices also consider the
impact of energy and capacity trading. These prices reflect the average
costs to serve the load in certain areas. Detailed calculation equations
can be found in the Average Electricity Prices section of the
appendix.


#### Cost of Health Damages from Air Pollution

In addition to direct system costs, ReEDS also includes a
postprocessing step for estimating health damages associated with air
pollution. Currently this focuses on mortality from long-term exposure
to fine particulate matter (PM<sub>2.5</sub>)[^ref61] from fossil fuel
combustion in the electric sector.

To estimate health damages, ReEDS relies on estimates of the mortality
risk per tonne of emissions from three reduced complexity air quality
models (AP2, EASIUR, and InMAP).[^ref62] Each of these models estimates
PM<sub>2.5</sub> formation associated with emissions of precursor
pollutants (NO<sub>x</sub> and SO<sub>2</sub>). To generate annualized
premature mortality, each model applies a concentration response
function from one of two studies linking exposure to PM<sub>2.5</sub> to
increased mortality risk. These two studies, referred to as the American
Cancer Society Study (ACS) and Harvard Six-Cities Study (H6C) provide
estimates of the relationship between pollution exposure and premature
mortality {cite}`gilmoreIntercomparisonSocialCosts2019`. The result is an estimate of the
mortality risk per tonne of pollutant emitted in each U.S. county. This
marginal damage estimate can be aggregated to the ReEDS balancing area
level and multiplied by total emissions to estimate total
mortality.

As a final step, annual premature deaths from air pollution can be
translated into a monetary value by applying a value of a statistical
life. For this ReEDS relies on the U.S. Environmental Protection
Agency’s estimate of \$7.4 million in 2006 dollars {cite}`epau.s.environmentalprotectionagencyMortalityRiskValuation2014` inflated to a 
present-day dollar value (\$9.9 million in 2021 dollars). These costs can 
then be translated into costs per unit of generation and cumulative (discounted)
cost over the study period.

The approach described here focuses on direct emissions from the
electric power sector, and thus does not capture estimates from other
sectors (such as transportation, buildings, and industry) or upstream
emissions (such as from fossil fuel extraction or power plant
manufacturing). It also does not quantify any social costs of climate
change from CO<sub>2</sub> or other greenhouse gas
emissions.


### Modeled Economic Metrics

ReEDS calculates multiple economic metrics for analyzing investment
decisions in the model, including:

- Levelized cost of energy (LCOE)

- Technology value

- Net value of energy (NVOE)

- Net value of capacity (NVOC)

- System profitability

These metrics are described in detail below.


#### Levelized Cost of Energy

LCOE measures the unit cost of electricity of a specific technology,
which is normally calculated as lifetime costs divided by energy
production. Specifically, the LCOE is calculated as follows 
{cite}`nrel2019AnnualTechnology2019`:

$$LCOE = \frac{FCR \times CAPEX + FOM}{CF \times 8,760} + VOM + FUEL$$

where FCR is the fixed charge rate; CAPEX is the capital expenditures;
FOM is the fixed operations and maintenance costs; CF is the capacity
factor; 8,760 is the number of hours in a year; VOM is variable
operations and maintenance costs; and FUEL is fuel costs (if
applicable).

In each model year, ReEDS reports the LCOE for all technology options
considering different variations in tax credit treatments and capacity
factor assumptions. ReEDS also calculates the LCOE for technologies that
are built in this model year using the generation from these
technologies.


#### Technology Value

ReEDS reports the value that generators receive from providing grid
services. Value is calculated as the product of service prices and
service provision quantities. For example, the value of a generator that
comes from providing energy service to meet planning reserve margin
requirement is calculated as the price of capacity multiplied by the
amount of firm capacity the generator can provide. The reported revenues
capture energy, capacity, operating reserve, and state-level and
national RPS requirements. Revenues can be normalized either by the
amount of generation or by the amount of installed
capacity.

Revenues are closely related to, but are different from the electricity
price and service requirement quantity parameters. Revenues consider the
*provision* of different services from a certain generator in a region,
whereas service requirement quantities calculate the *demand* of
different services in a region. The sum of revenues from all generating
technologies in a specific region does not necessarily equal the sum of
products of all service prices and corresponding service
requirements.


#### Net Value

ReEDS reports different economic viability metrics that consider both
*costs* and *values* of generating technologies to fully evaluate the
economic competitiveness of a certain technology, and to provide
intuitive explanations about investment decisions in the model. “Values”
of a generator reflect the potential economic benefit from displacing or
avoiding the cost of providing the services from other (marginal)
assets, while “costs” aggregate all different sources of costs needed to
build and operate a power plant to provide services. We define “net
value” as the difference between values and costs. Net value is related
to a concept in linear programming called “reduced cost.” Mills and
Wiser {cite:year}`millsEvaluationSolarValuation2012` describe reduced 
cost in the context of electricity system modeling.

We report three types of such metrics to assess the economic viability
of generators: net value of energy, net value of capacity, and system
profitability metrics ({numref}`net-value-metrics`). These metrics are reported both for
new investments in certain model year and for existing generators that
have been built.

```{table} Summary of Net Value Metrics
:name: net-value-metrics

|            Metric            | Conceptual Expression [Typical Units] |
|------------------------------|---------------------------------------|
| Net value of energy (NVOE)   | (Value – Cost)/Energy [$/MWh]         |
| Net value of capacity (NVOC) | (Value – Cost)/Capacity [$/kW-yr]     |
| System profitability         | f(Value/Cost) [unitless]              |
```

Net value of energy (NVOE) measures the unit profit of a specific
technology, calculated as the difference between generator revenue and
costs, then normalized by the energy production. The typical unit is
dollars per megawatt-hour (\$/MWh). Similarly, net value of capacity
(NVOC) measures the unit profit of a specific technology, calculated as
the difference between generator revenue and costs, then normalized by
the installed capacity. The typical unit is dollars per megawatt
(\$/MW).

Both of these two metrics are normalized metrics; because the
denominators vary broadly for different generator types, they may not
reflect the competitiveness of technologies consistently. Therefore, we
report a third type of economic viability metric, namely system
profitability metrics, which are essentially unitless functions of the
ratio between values and costs. Examples include profitability index
(value/cost) and return on investment (value/cost minus one). We report
both metrics in ReEDS, acknowledging that there are other formats of
system profitability metrics.

These economic viability metrics help explain investment decisions in
the model. Specifically, for all types of new investment in a certain
model year, the model considers all the costs to build and operate a
certain technology as *costs*, and the contribution of the technology to
all binding constraints as *values* (i.e., service provision). Typical
value sources are discussed above in [Technology Value](#technology-value). In calculations of
economic viability metrics, however, other types of “values”
are included to fully reflect model decisions. For example, an increase
of ancillary service requirements that are due to higher wind
penetration is counted as a negative value stream for wind, and it is
included in the metrics calculation here. Therefore, these metrics fully
reflect all the model constraints related to the investment
decision.


## Model Linkages
### ReEDS-PLEXOS

The ReEDS reduced-form dispatch and variable renewable parameterization
aims to represent enough operational detail for realistic capacity
expansion decisions, but the model cannot explicitly represent detailed
power system operations. To verify the feasibility of ReEDS solutions
and better inform its representation of system operation, NREL has
developed utilities to implement a ReEDS capacity expansion solution for
any solve year in the PLEXOS production-cost model
(PCM).

PLEXOS is a commercial PCM tool capable of representing individual
generating units and transmission nodes for least-cost dispatch
optimization at hourly or subhourly time resolution. It can incorporate
unit-commitment decisions and detailed operating constraints (e.g., ramp
rates, minimum runtime) to simulate realistic power system operations.
NREL has previously used PLEXOS in several analyses such as the Western
Wind and Solar Renewable Integration Study and the Eastern Renewable
Grid Integration Study {cite:p}`lewWesternWindSolar2013, bloomEasternRenewableGeneration2016`.

The ReEDS-PLEXOS linkage involves disaggregating the ReEDS solution and
adding necessary parameters for to the resolution necessary for PLEXOS.
To facilitate the translation, the existing linkage maintains the
spatial resolution of ReEDS and operates PLEXOS as a zonal model
matching ReEDS BAs to PLEXOS transmission zones. PLEXOS uses the ReEDS
transmission line capacity, and reactance and resistance are calculated
from ReEDS transmission properties to represent the aggregated
transmission system. Generating capacity within each zone is, however,
converted from aggregate ReEDS capacity to individual units in PLEXOS
using a characteristic unit size for each technology. For consistency,
ReEDS cost and performance parameters are used when possible and
reasonable, but values are taken from the average across WECC data when
parameters are not available from ReEDS or are available but used
inconsistently in ReEDS due to structural differences between the
models.[^ref63]

Once the ReEDS solution is converted to a PLEXOS database, one can
simulate hourly dispatch over a full year and compare results with ReEDS
outcomes. A consistent solution builds confidence in the effectiveness
of ReEDS capacity expansion decisions, while inconsistencies and
reliability concerns such as load shedding indicate the need for
improving capacity expansion model structures. Additional details are
available in Frew et al. {cite:year}`frewSunnyChanceCurtailment2019`.


### ReEDS-Cambium

Leveraging the capabilities of the ReEDS-PLEXOS linkage, a third
model—Cambium—has been developed. Cambium draws from ReEDS and PLEXOS
model solutions to assemble a structured database of hourly cost and
operational data for modeled futures of the U.S. electric sector. In
addition to directly reporting some metrics from both ReEDS and PLEXOS
(e.g., capacity buildouts from ReEDS and generation by technology from
PLEXOS), Cambium post-processes the outputs from both models to develop
new metrics that are designed to be useful for long-term
decision-making, such as a long-run marginal emission
rate.[^ref64]

Data sets derived through Cambium can be viewed and downloaded at
<https://cambium.nrel.gov/>. The documentation for Cambium contains
descriptions of the metrics reported in the databases and the methods
for calculating those metrics.


### ReEDS-JEDI

A linkage between ReEDS outputs and the Jobs and Economic Development
Impact Models (JEDI) allows the analysis of technology-specific economic
results (jobs, earnings, value added, total output) to ReEDS scenarios.
Currently, linkages have been built for the JEDI land-based wind,
photovoltaics, natural gas, and coal models, so economic results are
limited to these technologies alone. ReEDS outputs of capacity,
generation, fuel use, capital cost, O&M cost, and fuel cost by BA are
processed through the JEDI models to produce state-level economic
results.


### ReEDS-reV

The ReEDS supply curve for renewable technologies, including onshore
wind, CSP, utility scale PV, and geothermal are produced by reV. The
ReEDS-reV linkage allows for regional ReEDS investment decisions to be
mapped backed to individual reV supply curve sites. Site-specific supply
curve data from reV is binned for the ReEDS supply curve into five spur
line cost bins, from which investment decisions are made. By tracking
the timing and investment decisions within each of these bins, the
ReEDS-rev linkage maps regional capacity back to the individual sites
from which the bins were derived.

The resulting siting data is used to further the understanding of the
ReEDS capacity expansion decisions and identify areas for improvement
for resource siting in reV. The ReEDS-reV linkage is a key component in
the translation of ReEDS capacity expansion results to a nodal
production cost modeling databases.


## References
```{bibliography}
:cited:
```


## Appendix
### Natural Gas Supply Curves

The ReEDS model does not explicitly model the U.S. natural gas (NG)
system, which involves multiple sectors of the economy and includes
complex infrastructure and markets. Rather, a regional supply curve
representation is a used to approximate the NG system as it interacts
with the electric sector. For more information on the impact of natural
gas representation in ReEDS, see Cole et al.
{cite:year}`coleViewFutureNatural`.

The premise of using regional supply curves is that the price in each
region will be a function of both the regional and national NG demand.
The supply curves are parameterized from AEO scenarios for each of the
nine EIA census divisions (see {numref}`figure-offshore-wind-resource`). Two methods exist to
parameterize the natural gas supply curves and both are discussed here.
The first method which involves estimating a linear regression of prices
on regional and national quantities has been used in previous version in
ReEDS and is discussed first. The second method is relatively new to
ReEDS and involves parameterizing a constant elasticity of supply curve
and is discussed second. Through multiple tests, we have found minimal
differences in results between the two versions (1% or less of a change
in national generation by technology).

**Linear Regression Approach**

The AEO scenarios were used to estimate parameters for the following NG
price-consumption model:

```{figure} ../../images/ng-price-consumption-model.png
:name: 1-ng-price-consumption-model

[1]
```

where *P<sub>i,j</sub>* is the price of natural gas (in \$/MMBtu) in
region *i* and year *j*, the *α* parameters are the intercept terms of
the supply curves with adjustments made based on region
(*α<sub>i</sub>*), year (*α<sub>j</sub>*), and the region-year
interaction (*α<sub>i,j</sub>*), *β<sub>nat</sub>* is the coefficient
for the national NG demand (*Q<sub>nat</sub>*, in quads),
*β<sub>i</sub>* is the coefficient for the regional NG demand
(*Q<sub>i,j</sub>*) in region *i*. Note that the four *α* parameters in
\[1\] can in practice be represented using only
*α<sub>i,j</sub>*.

The β terms are regressed from AEO2014 scenarios, with nine of the 31
AEO2014 scenarios removed as outliers {cite}`eiaAnnualEnergyOutlook2014`. These outlier
scenarios typically include cases of very low or very high natural gas
resource availability, which are useful for estimating NG price as a
function of supply but not for estimating NG price as a function of
demand—for given supply scenarios. The national and regional β terms are
reported in {numref}`figure-census-division-values`. We made a specific post-hoc adjustment to the
regression model’s outputs for one region; the βi term for the West
North Central division was originally an order of magnitude higher than
the other βi values because the West North Central usage in the
electricity sector is so low (0.05 quad[^ref65] in 2013, compared to
~0.5 quad or more in most regions). The overall natural gas usage (i.e.,
not just electricity sector usage) in West North Central is similar to
the usage in East North Central, so intuitively it makes sense to have a
βi for West North Central relatively close to that of East North
Central. We therefore manually adjusted the West North Central βi term
to be 0.6 (in 2004\$/MMBtu/quad) and recalculated the alpha terms with
the new beta to achieve the AEO2014 target prices. The situation in West
North Central whereby such a small fraction of NG demand goes to
electricity is unique; we do not believe that the other regions warrant
similar treatment.


```{figure} ../../images/census-division-values.png
:name: figure-census-division-values

*β* values for the nine census divisions
```

The “National” value at the far left is *β<sub>nat</sub>*. A *β* of 0.2
means that if demand increases by one quad, the price will increase by
\$0.20/MMBtu (see Equation \[1\]).

The *α* terms are then regressed for each individual scenario assuming
the same *β* values for all scenarios. Although the *β* terms are
derived from AEO2014 data, *α* terms are regressed using AEO2018 data
for the scenario they are intended to represent {cite}`eiaAnnualEnergyOutlook2019a`. Thus, we
assume natural gas price elasticity has remained constant while price
projections shift over time as represented by the *α*
values.

**Comparison of Elasticities from Regression Approach to Literature Values**

Technical literature tends to report the price elasticity of supply and
the price elasticity of demand, which are estimates of the supply and
demand, respectively, of a good given a change in price. In the
formulation given by Equation \[1\], we attempt to estimate a value that
is similar to the price elasticity of demand—we estimate a change in
price given a change in demand. Therefore, we present here a comparison
against the price elasticity of demand as the closest available proxy,
noting however that it is not necessarily identical to estimates of β.
Price elasticity of demand is typically negative but is reported here as
a positive number for convenience.

External sources are varied and often vague in their estimates of price
sensitivity of natural gas. Using the reported domestic NG market demand
given for 2012 in AEO2014, the β values reported here yield an overall
NG sector elasticity value of 0.36–0.92 (higher values of β correspond
to lower elasticity values). Arora {cite:year}`aroraEstimatesPriceElasticities2014` estimated the price elasticity
of demand for NG to be 0.11–0.70, depending on the granularity and time
horizon of the NG price data considered. Bernstein and Griffin {cite:year}`bernsteinRegionalDifferencesPriceelasticity2006`
examined the price elasticity of demand for residential NG usage, and
they estimated the long-run elasticity to be 0.12–0.63 depending on the
region. The Energy Modeling Forum at Stanford University reports NG
price elasticity of demand for 13 different energy models {cite}`huntingtonEMF26Changing2013`. 
The reported elasticity ranges from 0 to 2.20 depending on the
year, model, and scenario considered. For the NEMS model, which is used
for the AEO, the elasticity ranges from 0.22 to 0.81 depending on the
year and scenario {cite}`huntingtonEMF26Changing2013`.

The EPA’s proposed Clean Power Plan included a projection that natural
gas usage will increase by 1.2 quads in 2020, resulting in an 8%–12%
increase in NG prices for the electric sector {cite}`smithEPACleanPower2014`. This
corresponds to a *β<sub>nat</sub>* of 0.38–0.51 in
2004\$/MMBtu/quad.

**Constant Elasticity of Supply**

The second method for representing gas price adjustments leverages a
constant elasticity of supply curve for census division prices as a
function of the quantities consumed. The general form of the equation
relies on a reference price ($\overline{p}$), a reference quantity
($\overline{q}$), and a price elasticity of supply ($\epsilon$)[^ref66] to
determine the endogenous price ($p$) based on an endogenous quantity
($q$) such that:

$$p = \overline{p}\left( \frac{q}{\overline{q}} \right)^{\epsilon}$$

When parameterizing for the census division representations, the supply
curve should reflect the change in price given a change in the census
division’s quantity consumed in the electricity sector. To the best of
our knowledge, no published studies estimate the elasticity of supply
for natural gas specific to each sector and region. Therefore, the
calibrated curve needs to consider the change in the census division’s
price given a change in the consumption of natural gas in the region’s
electricity sector with respect to other regions and sectors. To do
this, the reference price, numerator, and denominator in the previous
equation are adjusted to reflect the consumption change only in the
electricity sector. Explicitly, the constant elasticity of supply
parameters are now indexed by census division ($r$) and sector
$s \in \{ electricity,\ \ industrial,\ \ residential,\ \ commercial,\ \ vehicles\}$).
The equation used to populate the supply curve in the model
becomes:

$$p_{ele,r} = {\overline{p}}_{ele,r}\left( \frac{\sum_{s^{'} \notin ele,r^{'} \notin r}^{}{\overline{q}}_{s^{'},r^{'}} + q_{ele,r}}{\sum_{s,r}^{}{\overline{q}}_{s,r}} \right)^{\epsilon}$$

A potential addition to this representation, included as a switch in
the model, also includes national price adjustments as deviations from
the reference point. By denoting the national price as $p_{ele,nat}$,
the deviation from the benchmark price based on national quantities
consumed in the electricity sector can be computed
as:

$$\Delta p_{ele,nat} = {\overline{p}}_{ele,nat}\left( 1 - \frac{\sum_{s^{'} \notin ele,r}^{}{{\overline{q}}_{s^{'},r} + \sum_{r}^{}q_{ele,r}}}{\sum_{s,r}^{}{\overline{q}}_{s,r}} \right)^{\epsilon}$$


### Seasonal Natural Gas Price Adjustments

We use natural gas futures prices to estimate the ratio of winter to
non-winter natural gas prices to implement seasonal gas price
differences in ReEDS. We chose futures prices for two reasons: (1) ReEDS
represents a system with no unforeseen disturbances, which is similar to
futures prices and (2) historical natural gas prices have fluctuated
greatly since the deregulation of natural gas
prices.

{numref}`figure-natural-gas-futures-prices` shows the cyclical nature of the natural gas futures prices.
{numref}`figure-natural-gas-futures-prices-by-season` breaks the same prices out into seasons, showing that the
non-winter seasons have nearly the same price while wintertime prices
are consistently higher. Wintertime prices are on average 1.054 times
higher than non-winter prices. The standard deviation of this price
ratio is 0.004, indicating that the ratio shows very little year-to-year
variation.

```{figure} ../../images/natural-gas-futures-prices.png
:name: figure-natural-gas-futures-prices

Natural gas futures prices from the New York Mercantile Exchange for July 10, 2014
```

The prices show the higher wintertime prices and the cyclical nature of
the prices.

```{figure} ../../images/natural-gas-futures-prices-by-season.png
:name: figure-natural-gas-futures-prices-by-season

Natural gas futures prices from {numref}`figure-natural-gas-futures-prices` separated by season.
```

Non-winter prices are nearly the same while wintertime prices are
consistently higher.

A seasonal natural gas price multiplier is calculated in ReEDS based on
the natural gas price ratio such that wintertime prices are 1.054 times
higher than non-winter prices without changing the year-round average
price. Mathematically, this can be expressed as

| $$P_{year - round} = W_{winter}P_{winter} + \left( 1 - W_{winter} \right)P_{non - winter}$$ | \[2\] |
|----|----|
| $$P_{winter} = 1.054P_{non - winter}$$ | \[3\] |
| $$P_{winter} = \rho P_{year - round}$$ | \[4\] |
| $$P_{non - winter} = \sigma P_{year - round}$$ | \[5\] |

where P is the natural gas price for the period indicated by the
subscript, W<sub>winter</sub> is the fraction of natural gas consumption
that occurs in the winter months, and $\rho$ and $\sigma$ are the
seasonal multipliers for winter and non-winter, respectively. The
multipliers $\rho$ and $\sigma$ are determined by solving Equations
\[2\] through \[5\].


### Capital Cost Financial Multipliers

The financial multiplier represents the present value of revenue
requirements necessary to finance a new investment, including
construction financing, return to equity holders, interest on debt,
taxes, and depreciation. The formula is based on {cite}`shortManualEconomicEvaluation1995`.

```{figure} ../../images/capital-cost-financial-multipliers.png
:name: figure-capital-cost-financial-multipliers 

```

1.  **Construction cost multiplier:** additional cost for finance
construction
2. **Financing multiplier:** adjust required returns for
diversifiable risk
3. **Depreciation Expense:** reduce the taxable income by
the depreciation expense
4. **Depreciable Basis:** reduce the depreciable
basis due to the investment tax credit
5. **Investment tax credit:** reduce
the tax liability by the ITC
6. **Taxes:** additional revenues are required
to pay taxes

**Construction Cost Multiplier:** The construction cost multiplier
(CC<sub>mult</sub>) captures the cost to finance the construction of the
plant at construction interest rate *i*. We use a mid-year discounting
and account for the deduction of interest payments for
taxes.

$$CC_{mult} = 1 + \sum_{t}^{}{x_{t}\  \bullet \left\{ (1\  + \ i)^{t} - \ 1 \right\} \bullet (1 - T)}$$

The derivation of the construction cost multiplier is given
below.

The total payment (*TP)* required to finance *x* percent of
construction investment (*Inv*) at interest rate *i* in construction
year *t---*where *t* is defined relative to the in-service date (t=0 is
the final year of construction; t=1 is penultimate year of construction;
etc.)---is the following:

$${TP}_{t} = \ x_{t}\  \bullet \ Inv\  \bullet \ (1\  + \ i)^{t}$$

Define the interest payment (*I*) in year *t* as a function of the
total payment (*TP*) and the principal payment
(*P*):

$$I_{t}\  = \ {TP}_{t}\  - \ P_{t}$$

$\ \ \ \ \  = \ x_{t}\  \bullet \ Inv\  \bullet \ (1\  + \ i)^{t}\  - \ x_{t}\ *\ Inv$

$\ \ \ \ \  = \ x_{t}\  \bullet \ Inv\  \bullet \left\{ (1\  + \ i)^{t}\  - \ 1 \right\}$

The tax savings (*S*) from interest deductions in year *t* at tax rate
*T* is equal to:

$$S_{t}\  = \ I_{t}\  \bullet T$$

Therefore, the absolute net change in the investment cost due to
construction financing is the interest payments less the tax
savings:

$$\Delta\ cost\ (absolute)\  = \sum_{t}^{}{I_{t} - S_{t}}$$

$$= \sum_{t}^{}{I_{t} - I_{t} \bullet T}$$

$$= \sum_{t}^{}{I_{t} \bullet (1 - T)}$$

$$= \sum_{t}^{}{x_{t}\  \bullet \ Inv\  \bullet \left\{ (1\  + \ i)^{t} - \ 1 \right\} \bullet (1 - T)}$$

Finally, the total relative change in the investment cost due to
construction financing is:

$\Delta\ cost\ (relative)$ =

$$= \left( Inv + \sum_{t}^{}{I_{t} - S_{t}} \right)\ /\ Inv\ $$

$$= 1 + \frac{1}{Inv} \bullet \sum_{t}^{}{x_{t}\  \bullet \ Inv\  \bullet \left\{ (1\  + \ i)^{t} - \ 1 \right\} \bullet (1 - T)}$$

$$= 1 + \sum_{t}^{}{x_{t}\  \bullet \left\{ (1\  + \ i)^{t} - \ 1 \right\} \bullet (1 - T)}$$

**Financing Multiplier:** The financing multiplier (not to be confused
with the financial multiplier) is an adjustment to reflect either higher
or lower returns to capital, relative to the system-wide average return
to capital. Conceptually, it is a multiplier that reflects the total
present-value of a stream of higher (or lower) payments to capital,
relative to what the payments would be at the system’s average cost of
capital. For example, if a technology’s WACC ($WACC_{tech})$ is 7% and
the system-wide WACC is 5% ($WACC_{sys})$, and the technology is being
evaluated for a 20-year horizon (l) at a real discount rate of 5%
($d_{r})$, the financing multiplier (${fin}_{mult})$ would be 1.25, per
the equation below. This multiplier represents that the total
present-value of the returns to capital for this technology must be
higher (by an amount equal to 25% of the initial investment), relative
to a technology with average financing terms. The difference is the
technology WACC and system WACC represents the difference is returns to
capital due to diversifiable risk.

$${fin}_{mult} = 1 + \left( WACC_{tech} - WACC_{sys} \right) \bullet \frac{1 - \frac{1}{\left( {1 + d}_{r} \right)^{l}}}{d_{r}}$$

To derive the above equation, begin with the definition of the capital
recovery factor (*CRF*) for real discount rate ($d_{r})$ and economic
horizon (*l*):

$$CRF = \frac{Annuity}{Present\ Value\ of\ Annunity} = \frac{d_{r}}{1 - \frac{1}{\left( {1 + d}_{r} \right)^{l}}}$$

$$Present\ Value\ of\ Annuity = \frac{1}{CRF} \bullet Annuity$$

Therefore, for every dollar invested in a technology, the absolute
difference in required return is:

$\Delta\ returns\ (absolute) = \$ 1 \bullet WACC_{tech} \bullet \frac{1}{CRF} - \$ 1 \bullet WACC_{sys}*\frac{1}{CRF}$

Finally, the relative difference in required return per dollar invested
is:

$$\Delta\ returns\ (relative) = \frac{\$ 1 + \Delta}{\$ 1} = 1 + \Delta$$

**Depreciation Expense:** The present value of depreciation (PVdepr)
expense is computed based on the fraction of the plant value that is
depreciable in each year. All investments use a MACRS depreciation
schedule with $f_{t}^{depr}$ representing deprecation fraction in year
t. This depreciation is sheltered from taxes, which is reflected by the
term $1 - T*PV_{depr}$ in the financial multiplier equation
above.

$$PV_{depr} = \sum_{t}^{}{\frac{1}{\left( 1 + d_{n} \right)^{t}} \bullet f_{t}^{depr}}$$

**Depreciable Basis:** The eligible cost basis for MACRS depreciation
expense is reduced by one-half the effective value of the tax
credit:

$$PV_{depr}*\left( 1 - \frac{{ITC}_{eff}}{2} \right)$$

**Investment Tax Credit:** The value of the ITC is reduced, to reflect
the costs of monetizing it ($m_{ITC}$). The effective investment tax
credit value (${ITC}_{eff})$ reduces the tax burden of the
investments.

$${ITC}_{eff} = ITC \bullet m_{ITC}$$

**Taxes:** The denominator term of the financial multiplier equation,
“1-T”, reflects the additional revenues necessary to pay taxes. The tax
burden is adjusted for depreciation expenses as well as the effective
investment tax credit.

**Weighted Average Cost of Capital:** The technology-agnostic, nominal
discount rate is represented as the average WACC. Where, d<sub>f</sub>
is the debt fraction, *rore<sub>n</sub>* is the nominal rate of return
on equity, *T* is the effective tax rate, and *I<sub>n</sub>* is the
nominal interest rate on debt.

$$d_{n} = (1 - df)*{rore}_{n} + (1 - T)*df*I_{n}$$

### Present Value of Direct Electric Sector Cost

The equations in this section are used to calculate the present value
cost of building and operating the system for some defined economic
analysis period. To calculate the present value of total system cost,
the cost in each future year $t$ is discounted to the initial year of
the economic analysis period, $t_{0}$, by a social discount rate,
$d_{social}$. The real social discount rate used here for present value
calculation is different from the investment discount rate assumptions,
or cost of capital (WACC) assumptions.

The present value, or $PV$ in the equation, consists of two cost
components: 1) the present value of all operational costs in the model
for the analysis period, $PV_{operational}$, including fixed and
variable operating and maintenance costs for all sectors, as well as
fuel costs and 2) the present value of all new capital investments,
$PV_{capital}$. The present value of energy system costs is then
calculated as:

$$PV = PV_{operational} + PV_{capital}$$

Operational costs, $PV_{operational}$, and capital costs
category,$\ PV_{capital}$, are discounted from year $t$ by
$\frac{1}{\left( 1 + d_{social} \right)^{t - t_{0}}}$ for each year in
the analysis period:

$$PV_{operational} = \sum_{t = t_{0}}^{t_{f}}{C_{op,t} \times \frac{1}{\left( 1 + d_{social} \right)^{t - t_{0}}}}$$

$$PV_{capital} = \sum_{t = t_{0}}^{t_{f}}{C_{cap,t} \times \frac{1}{\left( 1 + d_{social} \right)^{t - t_{0}}}}$$

where $C_{op,t}$ is the operational costs in year t, and $C_{cap,t}$ is
the capital costs in year $t$. For all ReEDS system cost results, we
assume the operational costs for the non-modeled year are the same as
the closest model year.

In this present value calculation, the economic analysis period is
2018–2050. The social discount rate used for present value calculations,
$d_{social}$, is assumed to be 7% (real). This is different from the
WACC assumption for investment decisions


### Marginal Electricity Prices

ReEDS marginal “competitive” electricity prices are derived from the
linear programming formulation.

In standard form, the primal formulation of a linear program
is:

$$(P)\ \ \ \ \min{c^{T}x}$$

$${s.t.}{\ \ \ \ \ Ax \geq b}$$

$$\ \ \ \ \ \ \ \ \ \ \ \ \ \ x \geq 0$$

The associated dual formulation of the primal
is:

$$(D)\ \ \ \ \max{y^{T}b}$$

$${s.t.}{\mathbf{\ \ \ \ \ }y^{T}A \leq c^{T}}$$

$$\ \ \ \ \ \ \ \ \ \ \ \ \ \ y \geq 0$$

Consider a simplified formulation of the ReEDS model with a subset of
constraints: (1) resource limits, (2) capacity limits, (3) supply/demand
balance, (4) planning reserve margin requirement, (5) operating reserve
requirement, and (6) national and/or state-level RPS requirements. The
primal formulation is:

**Parameters**

$capcost_{i}$: capital cost of model plant i (\$/MW)

$vomcost_{i}$: variable O&M cost of model plant i (\$/MWh)

$s_{i}$: available supply of model plant i (MW)

$load$: electric load (MW)

$cv_{i}$: capacity value of model plant i (MW)

$f^{prm}$: planning reserve margin (unitless)

$f^{or}$: operating reserve requirement (unitless)

$f^{RPS}$: national and/or state-level RPS requirement (unitless)

**Variables**

$C_{i}$: capacity of model plant i (MW)

$G_{i}$: generation of model plant i (MWh)

$OR_{i}$: operating reserve allocation of plant *i* (MWh)

$$minimize\ \sum_{i}^{}{capcost_{i} \bullet C_{i} + vomcost_{i} \bullet G_{i}}$$

Subject to: 

$$C_{i} \leq s_{i}\ \ \ \ \ \forall i\ \ \ \ \ \lbrack 1\rbrack$$

$$\frac{G_{i}}{8,760} + \frac{OR_{i}}{8,760} - C_{i} \leq 0\ \ \ \ \ \forall i\ \ \ \ \ \lbrack 2\rbrack$$

$$\sum_{i}^{}{G_{i} = load}\ \ \ \ \ \lbrack 3\rbrack$$

$$\sum_{i}^{}{{cv_{i} \bullet C}_{i} \geq \frac{\left( 1 + f^{prm} \right)}{8760} \bullet load}\ \ \ \ \ \ \lbrack 4\rbrack$$

$$\sum_{i}^{}{OR_{i} \geq f^{or} \bullet load}\ \ \ \ \ \lbrack 5\rbrack$$

$$\sum_{i \in RE}^{}{G_{i} \geq f^{RPS} \bullet load}\ \ \ \ \ \lbrack 6\rbrack$$

$$C_{i}, G_{i},OR_{i} \geq 0\ \ \ \ \ \forall i \ \ \ \ \ \lbrack 7\rbrack $$

Constraints \[1\] define the resource limits for each model plant.
Constraints \[2\] limit how capacity is allocated for each model plant
(i.e., for energy or reserves). Constraint \[3\] requires the total
generation supplied to equal the load. Constraint \[4\] ensures the
total firm capacity meets the planning reserve margin requirement.
Constraint \[5\] ensures the total operating reserves meet the operating
reserve requirement. Constraint \[6\] requires that total generation
from renewable technologies meets the state-level and national RPS
requirements.

From the dual formulation of the primal, the objective function is*:*

$$y^{T}b = y_{1} \bullet s + y_{2} \bullet 0 + y_{3} \bullet load + y_{4} \bullet \frac{(1 + prm)}{8760} \bullet load + y_{5} \bullet f^{or} \bullet load + y_{6} \bullet f^{RPS} \bullet load$$

Reformulating the primal with Constraints \[3\], \[4\], \[5\], and
\[6\] “linked” with a “load” variable, *L*, an alternative, but
equivalent, primal formulation is the following:

$$minimize\ \sum_{i}^{}{capcost_{i} \bullet C_{i} + vomcost_{i} \bullet G_{i}}$$

Subject to:

$$C_{i} \leq s_{i}\ \ \ \ \ \forall i\ \ \ \ \ \lbrack 1\rbrack$$

$$\frac{G_{i}}{8760} + \frac{OR_{i}}{8760} - C_{i} \leq 0\ \ \ \ \ \forall i\ \ \ \ \ \lbrack 2\rbrack$$

$$\sum_{i}^{}{G_{i} - L \geq 0}\ \ \ \ \ \lbrack 3^{'}\rbrack$$

$$\sum_{i}^{}{{cv_{i} \bullet C}_{i} - \frac{\left( 1 + f^{prm} \right)}{8760} \bullet L \geq}0\ \ \ \ \ \ \lbrack 4^{'}\rbrack$$

$$\sum_{i}^{}{OR_{i} - f^{or} \bullet L \geq 0}\ \ \ \ \ \lbrack 5'\rbrack$$

$$\ \sum_{i \in RE}^{}{G_{i} - f^{RPS} \bullet L} \geq 0\ \ \lbrack 6'\rbrack$$

$$C_{i}, G_{i},OR_{i} \geq 0\ \ \ \ \ \lbrack 7\rbrack$$

$$L = load\ \ \ \ \ \lbrack 8'\rbrack$$

From the dual formulation of the alternative primal, the objective
function is:

$$y^{T}b = y_{1} \bullet s + y_{2} \bullet 0 + y_{3^{'}} \bullet 0 + y_{4^{'}} \bullet 0 + y_{5^{'}} \bullet 0 + y_{6^{'}} \bullet 0 + y_{8^{'}} \bullet load$$

Equating the dual objective functions from the two equivalent primal
formulations, we find that the marginal off the linking constraint
\[8’\] is a blending of all constraints containing the “load” variable,
including, constraints \[3\], \[4\], \[5\], and \[6\]:

$$y_{8^{'}} \bullet load\mathbf{=}y_{3} \bullet load + y_{4} \bullet \frac{\left( 1 + f^{prm} \right)}{8760} \bullet load + y_{5} \bullet f^{or} \bullet load + y_{6} \bullet f^{RPS} \bullet load$$

$$y_{8^{'}} = y_{3} + y_{4} \bullet \frac{\left( 1 + f^{prm} \right)}{8760} + y_{5} \bullet f^{or} + y_{6} \bullet f^{RPS}$$

Therefore, we define the marginal off the linking constraint
$\lbrack y_{8^{'}}\rbrack$ as the “all-in” marginal price of electricity
(i.e., change in total cost \[objective function\] given a small change
in load). This marginal electricity price includes the energy price,
capacity price, operating reserve prices, and potential RPS prices.
Marginal electricity prices are reported at BA level with different
requirement categories. These prices can be aggregated at different
regional level, weighted by corresponding requirement quantities for
certain category.


### Average Electricity Prices

Average electricity prices are calculated as the annualized total costs
of building and operating the system in certain geographic area, divided
by the electricity load in that area. At national level, the prices are
calculated as:

$$p(costtype,\ year) = \frac{systemcost_{costtype,year}}{load_{year}}$$

where system costs include both annualized capital and operational
costs. Annualized costs for existing (i.e. pre-2010) power plants are
also considered given plants’ initial investment costs and the built
year.

At BA-level, average electricity prices also consider the impact of
energy and capacity trading:

$$p(costtype,BA,year)$$
$$ = ca{pital}_{costtype,BA,year} + o{peartional}_{costtype,BA,year}$$
$$ + \lbrack \sum_{n}^{}{import_{n,p,h,year} \times price_{n,h,year}}$$
$$ - \sum_{n}^{}{export_{p,n,h,year} \times price_{p,h,year}} \rbrack _{energy} $$
$$ + \lbrack \sum_{n}^{}{import_{n,p,szn,year} \times price_{n,szn,year}} $$
$$ - \sum_{n}^{}{export_{p,n,h,year} \times price_{p,szn,year}} \rbrack _{capacity}$$

Where n, p and BA all indicate balancing areas, $import_{n,p,h,t}$
indicates energy or capacity transfer from n top;$\ export_{p,n,h,t}$
indicates energy or capacity transfer from p to n. Capital costs also
include annualized costs for pre-2010 power plants.

Specifically, the energy import/export is calculated as:

$$\sum_{n}^{}{import_{n,p,h,t} \times price_{n,h,t}} = \sum_{n}^{}{powerfracupstream_{n,p,h,t} \times gen_{p,h,t} \times price_{n,h,t} \times hours_{h} \times (1 + loss_{n,p,h,t})}$$

$$\sum_{n}^{}{export_{p,n,h,t} \times price_{p,h,t}} = \sum_{n}^{}{powerfracdownstream_{p,n,h,t} \times gen_{p,h,t} \times price_{p,h,t} \times hours_{h}}$$

where t is year, p and n are both balancing areas, h indicates time
slices.


### Spatial Resolution Capabilities

The ReEDS model has four default spatial resolutions, shown in
{numref}`figure-available-region-options`. The default settings use the model balancing areas (bottom
left of {numref}`figure-available-region-options`). The model also includes a custom aggregation
capability that enables users to select any aggregation of regions built
from counties or balancing areas. National-scale county-level resolution
runs are extremely computationally intensive, so require simplifications
in other aspects of the model (e.g., fewer timesteps, solve years, or
technologies) to be able to produce a solution, and even with
simplifications it requires hundreds of gigabytes of memory to process
the county-level inputs. Any runs that use aggregated states require
that state policies be turned off because the model does not have any
built-in features for aggregating state policies for states that have
been combined.

```{figure} ../../images/available-region-options.png
:name: figure-available-region-options

Region options available in the ReEDS model for doing model runs.
```

The spatial framework built into the ReEDS model allows for other
spatial resolutions. For example, nodal datasets can be represented in
the model. When running with nodal data, each renewable energy resource
site can only be associated with a single node, so the node assignments
have to be done before a model run is
performed.

The model also has the capability to use mixed resolutions. For
example, California can be represented using model balancing areas,
while the rest of the United States is represented at state resolution.
This can enable finer detail for a specific region of interest, while
still capturing trades with neighboring regions as lower resolution, but
with a reasonable solution time.


#### Data Inputs and Handling

Nearly all ReEDS data inputs that include a spatial dimension are
specified at the model balancing area resolution.[^ref67] In order to be
able to perform runs at county-level resolution, some inputs are
included at both the county-level and balancing area-level
resolution.


#### Transmission Data

Transmission capacity between counties is based on nodal transmission
network data (see {numref}`figure-nodal-transmission-network-data`) collected as part of the North American
Renewable Integration Study {cite}`brinkmanNorthAmericanRenewable2021a`. Nodes from
the data set are spatially matched to counties using nodal coordinates and
a shapefile of U.S. counties (described below). With this dataset there
are a few dozen counties have no transmission nodes or capacity, which
may be the result of missing data. To address this, nodes and lines are
added to ensure that every county has at least one transmission
interface. This is done by either adding a node on existing lines that
cross a county but did previously have nodes in that county, or if there
are no transiting lines by adding a node to the county centroid and
matching to the closest node in a neighboring
county.

```{figure} ../../images/nodal-transmission-network-data.png
:name: figure-nodal-transmission-network-data

Nodal transmission network data. Black lines are those from the dataset, and red lines are the lines that were added to ensure that every county included at least one interface.
```

Power flow constraints imposed by the topology of the network can limit
the true transfer capacity between two counties to a level below the
physical capacity of the lines connecting those counties. ReEDS
estimates these interface capacity limits using an optimization method
that finds the maximum transfer values given network characteristics,
the location of generators and load, and other constraints {cite}`brownGeneralMethodEstimating2023`.
Because interface limits are typically less influenced by parts
of the network that are further away, the method is run on a subset of
the network. This subset is selected by including all parts of the
network that are a specified number of “hops” away from the interface
being optimized. A comparison of the results from the optimization
method with different hops found that total transfer capacity saturated
after 6 hops, so this value was used when calculating the county-level
transfer limits used in ReEDS. Since the transfer capacity can differ
depending on the direction, the optimization is run once in each
direction (forward and reverse) for each interface.

After the optimization, some counties have zero transfer capacity in
one or both directions; these are replaced with either the transfer
capacity estimated in the other direction if it is non-zero or the
thermal capacity of the line. To estimate metrics such as TW-mi of
transfer capacity, ReEDS uses the distance between the centroids of the
two counties in the interface. The final transmission limits calculated
using this method are show in {numref}`figure-transfer-limits`.

```{figure} ../../images/transfer-limits.png
:name: figure-transfer-limits

Final transfer limits used in the county-level input dataset for the forward direction.
```


#### Wind and Solar Supply Curve Data

Supply curves for wind and solar are based on data from the renewable
energy potential model (reV), which provides total resource potential,
representative resource profiles, and any location-dependent supply
curve costs {cite}`maclaurinRenewableEnergyPotential2021`. Each supply curve 
point from the reV model is mapped directly to its corresponding county. These 
supply curve points are then aggregated by ReEDS to produce county level supply
curves.

The reV model includes estimates of the cost of investments needed to
reinforce the transmission network with the addition of more wind and
solar. For the ReEDS balancing area spatial representation, these
network reinforcement costs are calculated by determining the least cost
interconnection point and then estimating the transmission upgrades
needed between that point and balancing area’s interregional network
node. Since the county-level resolution now explicitly represents
transmission investments between counties, the network reinforcement
costs from reV are not included in the transmission cost estimates of
the county supply curves. Spur line costs, or the cost to build from the
resource site to the interconnection point, are still taken from reV. In
the future the reV model may be adapted to produce network reinforcement
costs at the county level, though they might be sufficiently small that
ignoring them would be appropriate.


#### Power Plant Capacity Data

Capacity data in ReEDS for existing units, prescribed builds, and
prescribed retirements[^ref68] are taken from the National Electricity
Modeling System (NEMS) power plant database. The power plants in this
database include latitude and longitude to give their location. These
locations are mapped to counties to provide the county assignment for
the power plants. In a few isolated cases, hydropower units that were on
a county boundary were manually assigned to a county to better align
with the jurisdiction that operates that plant. For example, the
Columbia River serves as a boundary line for several counties, and
hydropower plants on the Columbia were assigned to the county’s public
utility district that owns and operates that dam, rather than to the
county that mapped to the specific latitude and longitude
value.


#### Shape Files

Matching transmission nodes to counties and plotting maps of
county-level results requires shapefiles of U.S. counties. For this
purpose, ReEDS relies on the 2022 vintage of TIGER/Line Files published
by the Census Bureau, which includes all legal boundaries and names as
of January 1, 2022 {cite}`u.s.censusbureau2022TIGERLine2022`. The shapefiles 
are converted to the ESRI:102008 coordinate reference system and any
counties outside the continental U.S. are dropped.


#### Scaling Datasets to County Resolution

All datasets besides those described above were downscaled from the
balancing area resolution to county level resolution using one of five methods:

**Uniform Disaggregation:**

All counties within a balancing area are assigned the same value as the
one used for the balancing area.

**Downscaling based on population:**

The “population” disaggregation method uses population fractions as
multipliers to calculate county-level data from BA-level inputs. The
multipliers used in this method represent the fraction of a county’s
population with respect to its corresponding ReEDS BA. Population data
used to create the multipliers are sourced from the 2021 Population
Totals dataset provided by the US Census Bureau \[link\]. Example data
for ReEDS BAs p29 and p30 are shown below in {numref}`population-fraction-ex-data`.

```{table} Example data of population fractions used in downscaling ReEDS input data based on population.
:name: population-fraction-ex-data

| ReEDS Balancing Area (BA) | County | Population Fraction |
|----|----|----|
| p29 | p04001 | 1 |
| p30 | p04019 | 0.956 |
| p30 | p04023 | 0.044 |
```

Since only one county exists in the ReEDS BA “p29,” the population
fraction for that county is 1. On the other hand, two counties exist in
the ReEDS BA “p30”: the population fractions show that 95.6% of the
population of p30 live in county p04019, while 4.4% of the population
lives in p04023. To disaggregate by population, the dataset is mapped to
regionally-indexed BA-level ReEDS input data and the Population Fraction
is multiplied by the values of the BA-level dataset.

**Downscaling based on geographic size:**

The geographic size disaggregation method operates similarly to the
“population” disaggregation method but instead uses the fraction of a
county’s geographic area with respect to its corresponding ReEDS BA as
fractional multipliers for downscaling BA-level input data to county
level. Geographic area data used to create the multipliers are sourced
from the 2022 TIGER/Line US County Shapefile provided by the US Census
Bureau \[link\] and found in the inputs folder of the ReEDS
repository.

**Downscaling based on the existing hydropower capacity:**

The existing hydropower disaggregation method uses the fraction of
existing hydropower capacity in a given county with respect to the total
hydropower capacity of the county’s corresponding ReEDS BA as fractional
multipliers for downscaling BA-level input data to county level.
Existing hydropower capacity data used to calculate these fractional
multipliers are sourced from the EIA-NEMS generator database included in
the ReEDS inputs. This down-scaling method is used for
hydropower-specific data, such as hydropower upgrades.

**Downscaling based on transmission line size:**

Fractional multipliers used in the transmission line size
disaggregation method represents the ratio of transmission capacity
between a given US county and a Canadian balancing area in relation to
the total transmission capacity of the county’s corresponding US
balancing area. As an example: if US balancing area p1 is comprised of 2
counties, and 300 MW of transmission capacity exists between county 1
and the Canadian balancing area and 100 MW of transmission capacity
exists between county 2 and Canadian balancing area, then the ratio of
3/4 (0.75) is used to disaggregate data between county 1 and the
Canadian balancing area while a ratio of 1/4 (0.25) is used to
disaggregate data between county 2 and the Canadian balancing area.
Transmission data used to create these multipliers are sourced from the
same nodal dataset used to create the transmission interface limits
described above. Note that transmission lines found in the source data
are considered to be bidirectional: therefore, when calculating the
total transmission capacity between a US BA and Canadian BA both
directions must be considered. This down-scaling method is applied to
Canadian import and export inputs.

We selected one of the 5 downscaling methods above for each of the
inputs that included a spatial dimension. The choice was made using
analyst judgement. The input structure of ReEDS is such that if an
appropriate county-level dataset becomes available, it can be used in
place of the downscaled dataset.


#### Input Data Handling

Because some input data are specified at both the balancing area
resolution and the county resolution, the inputs used for a given run
will depend on the spatial resolution selected for that run. The input
scripts include logic that will read in the file with the appropriate
spatial resolution, and use that for the remainder of the run. In the
case of mixed resolutions, both files will be read in, and the
appropriate regions will be concatenated to create a single input file
with the specified spatial resolutions.

ReEDS has been set up to run so that only data for the regions being
modeled will be included in the model. For example, if doing a run that
includes only the state of North Dakota, the inputs processing step of
ReEDS will filter all input data to include only the data for North
Dakota.[^ref69]

Spatial datasets are dynamic within the model itself, so the model is
agnostic to the region names.


#### Challenges and Benefits of Enhanced Spatial Resolution

The greater spatial resolution available in ReEDS with county-level
inputs creates a variety of opportunities to apply the ReEDS model to
answer questions. It enables specific regions of the country to be
captured to greater resolution, enabling more granular outputs of power
plant siting, transmission expansion, and emission impacts. The higher
resolution can also highlight key regional boundaries or interfaces that
might not have been present in a lower resolution model run. Our testing
has also shown that county-level resolution can lead to better estimates
of curtailment because there is more detail on the underlying
transmission system.

The enhanced spatial resolution also comes with a variety of
challenges. These include runtime, especially as the number of regions
considered grows. Much of our testing showed that a 10-fold increase in
the number of regions led to at least a 10-fold increase in solve time,
though runtime ultimately depends on the machine specifications and the
model options selected for that particular run. Another major challenge
is sourcing appropriate input data. If the down-scaling methods
described above are not suitable for answering the questions of a
particular analysis, then new data will be to be procured. Additionally,
even the best transmission datasets we had available still had
omissions, so it is unclear if key data will be missing for studying a
particular region.

Finally, enhanced spatial resolution can lead to false precision, where
users see model solutions at high spatial resolution, and put more stock
into that model solution than is warranted due to uncertainty in the
data or methods used. For example, Mehrtash et al. {cite:year}`mehrtashDoesChoicePower2023` 
show that the choice of transmission power flow representation can have 
significant impact on the model solution.


### Differences from the 2020 Model Version

{numref}`model-differences` summarizes the key differences from the 2020 model version.
{numref}`dgen-model-differences` summarizes the key differences in the dGen model, which is
used to provide the rooftop PV input projections for ReEDS.

```{table} Key Differences in Model Inputs and Treatments for ReEDS Model Versions
:name: model-differences

| Inputs and Treatments | 2020 Version (July 2020) | 2023 Version (July 2023) |
|----|----|----|
| Fuel prices | AEO2020 | AEO2023 |
| Demand growth | AEO2020 | AEO2023? |
| Generator technology cost, performance, and financing | ATB 2020<sup>a</sup> | ATB 2023<sup>a</sup> |
| Endogenous retirements | On by default; when turned on, plants retire when they cannot recover at least half of their fixed O&M | On by default; when turned on, plants retire when they cannot recover at least half of their fixed O&M |
| Coal fixed O&M | Escalates from 2019 using assumptions from AEO2019 | Escalates from 2019 using assumptions from AEO2019 |
| Nuclear fixed O&M | Escalates from 2019 using assumptions from AEO2019 | Escalates from 2019 using assumptions from AEO2019 |
| Wind, solar, and load data | Includes data for 2007–2013; dispatch is done using 2012 data and capacity credit calculations are done using 2007–2013 data {cite}`coleConsiderationsMaintainingResource2020`| Includes data for 2007–2013; dispatch is done using 2012 data and capacity credit calculations are done using 2007–2013 data {cite}`coleConsiderationsMaintainingResource2020` |
| Electrification | Includes three levels of electrification | Includes three levels of electrification |
| Demand-side flexibility | Includes three levels of flexibility | Includes three levels of flexibility |
| Renewable fuel combustion turbine | Includes combustion turbine that runs on a generic renewable fuel with a minimum 6% capacity factor | Includes combustion turbine that runs on a generic renewable fuel with a minimum 6% capacity factor |
| Upgrades | Thermal technologies can be upgraded (e.g., by adding CCS). | Thermal technologies can be upgraded (e.g., by adding CCS). |
| Storage curtailment recovery | Uses hourly net load profiles and a dispatch algorithm to determine the amount of curtailment that can be recovered by storage | Uses hourly net load profiles and a dispatch algorithm to determine the amount of curtailment that can be recovered by storage |
| Battery storage durations | Includes 2-, 4-, 6-, 8-, and 10-hour battery storage | Includes 2-, 4-, 6-, 8-, and 10-hour battery storage |
| Storage capacity credit | Calculated using seven years of hourly data; capacity credit bins by duration allow for nonlinear changes in the optimization model; one-hour buffer accounts for uncertainty in forecasts and ability to dispatch | Calculated using seven years of hourly data; capacity credit bins by duration allow for nonlinear changes in the optimization model; one-hour buffer accounts for uncertainty in forecasts and ability to dispatch |
| Wind and solar capacity credit | Calculated using seven years of hourly resource and load data | Calculated using seven years of hourly resource and load data |
| Wind supply curve | Spatially-explicit modeling of multiple exclusions and setbacks from buildings, roads, transmission rights-of-way, and radar along with other exclusion layers | Spatially-explicit modeling of multiple exclusions and setbacks from buildings, roads, transmission rights-of-way, and radar along with other exclusion layers |
| Wind degradation | Annual degradation of 0.27% per year represented based on empirical data {cite}`hamiltonHowDoesWind2020` | Annual degradation of 0.27% per year represented based on empirical data {cite}`hamiltonHowDoesWind2020` |
| PV degradation | 0.7%/yr per the ATB 2020 | 0.7%/yr per the ATB 2020 |
| Wind and solar curtailment | Modeled using a simplified hourly dispatch model | Modeled using a simplified hourly dispatch model |
| Pumped-hydro capital cost | Declines over time per Hydropower Vision {cite}`doeHydropowerVisionNew2016` | Declines over time per Hydropower Vision {cite}`doeHydropowerVisionNew2016` |
| Storage energy arbitrage value | Calculated using hourly prices | Calculated using hourly prices |
| Minimum capacity factor for NGCT | 1% per PLEXOS runs of the 2019 Standard Scenarios | 1% per PLEXOS runs of the 2019 Standard Scenarios |
| Tax credits | Use a four-year safe harbor construction period; December 2019 production tax credit update represented; tax credits for CCS represented (use of captured carbon is not considered) | Use a four-year safe harbor construction period; December 2019 production tax credit update represented; tax credits for CCS represented (use of captured carbon is not considered) |
| State policies | Policies as of June 2020 | Policies as of June 2020 |
| Nuclear power plant assistance | Assistance for Connecticut, Illinois, New Jersey, New York, and Ohio represented | Assistance for Connecticut, Illinois, New Jersey, New York, and Ohio represented |
| Outage rates | Outage rates based on 2014–2018 Generating Availability Data System data | Outage rates based on 2014–2018 Generating Availability Data System data |
```

<sup>a</sup> The default cost recovery period is 20 years in ReEDS and
30 years in the ATB.

```{table} Key Differences in dGen Model Versions**
:name: dgen-model-differences

| Inputs and Treatments | 2019 Version | 2020 Version |
|----|----|----|
| Demand growth | AEO2019 | AEO2020 |
| Technology cost | ATB 2019 | ATB 2020 |
| Tariff set | Curated in January 2019 | Curated in June 2020 |
| Wholesale electricity prices | ReEDS 2019 | ReEDS 2020 |
| State and utility net energy metering policies | Updated in March 2019 | Updated in June 2020<sup>a</sup> |
```
 
<sup>a</sup> If states have no mandated NEM expiry dates, a distributed
solar penetration threshold was implemented, which was determined from
values of peer states.


[^ref1]: “Regional Energy Deployment System Model,” NREL,
    <https://www.nrel.gov/analysis/reeds/>

[^ref2]: Production technologies include those that produce hydrogen or
    caption carbon from the air.

[^ref3]: VRE is also sometimes referred to as Variable Renewable Energy
    Resource

[^ref4]: “Regional Energy Deployment System Model,” NREL,
    <https://www.nrel.gov/analysis/reeds/>

[^ref5]: Here, the t+1 notation is used heuristically, as the model year
    subsequent to *t* can be *t+1, t+2, t+3,* etc.

[^ref6]: The current default is 20 years, but it can be adjusted by the
    user.

[^ref7]: Hydropower’s contribution to planning reserves depends on its
    categorization as dispatchable or non-dispatchable, which is
    discussed in [Hydropower](#hydropower).

[^ref8]: CO<sub>2</sub> equivalent emissions from upstream methane are
    sensitive to assumptions regarding leakage rate and the time horizon
    for methane global warming potential. Other life cycle emissions
    (often with considerable uncertainty) are not included here,
    including methane from hydropower, biomass net emissions, CO2
    leakage from CCS, and other emissions. Methane leakage is not
    included in emissions estimates for transportation or
    residential/commercial/ industrial end-use applications, or in
    historical estimates of electricity sector emissions.

[^ref9]: A ReEDS-India model version has also been developed. Details of
    the implementation are not discussed here.

[^ref10]: These additional geographical layers defined in ReEDS do not
    necessarily align perfectly with the actual regions, except for
    state boundaries, which are accurately represented.

[^ref11]: The full spatial resolution capability with county-level data was
    not available publicly until version 2024.1.0
    (<https://github.com/NREL/ReEDS-2.0/releases/tag/v2024.1.0>).

[^ref12]: All renewable resource assessments are independent and mutually
    exclusive of each other due to their unique nature and to allow
    ReEDS to dynamically evaluate cost-optimal capacity expansion
    without any upstream ranking of which technologies would be
    preferred at a given site. This implementation ignores any possible
    land-use conflicts between multiple technologies at the same site,
    but spatial aggregation and resource heterogeneity is expected to
    alleviate this limitation.

[^ref13]: CSP refers to solar thermal power and not concentrating PV.

[^ref14]: Where given in the sections below, renewable energy resource
    potential values refer to the resource potential represented in
    ReEDS and not the total technical resource potential. The renewable
    potential capacity modeled in ReEDS includes exclusions in the
    pre-processing steps for the model, such as site exclusions, assumed
    transmission access limits, or a narrower set of technologies
    considered. Lopez et al. {cite:year}`lopezLandUseTurbine2021b` present 
    renewable technical potential for the United States.

[^ref15]: Individual wind sites are grouped into ten resource classes for
    ReEDS, based on average wind speed (The wind resource is not evenly
    binned into the 10 classes, as the better classes have higher
    resolution (smaller bins)).

[^ref16]: Represents the difference in overnight capital cost from the 5 MW
    system (the smallest reported) and the 100 MW system from {numref}`figure-cv-calculation-ldc-approach`
    of Fu, Feldman, and Margolis {cite:year}`fuSolarPhotovoltaicSystem2018`.

[^ref17]: <https://nsrdb.nrel.gov/>

[^ref18]: The solar multiple (SM) is defined as the ratio of the design
    solar field aperture area to the aperture area required to produce
    the power cycle design thermal input (and power output) under
    reference environmental conditions.

[^ref19]: Historical and announced trough-based systems are characterized
    with technology-appropriate characteristics.

[^ref20]: While differentiating pre- and post-1995 is somewhat arbitrary,
    it allows the model to better represent performance differences
    between relatively old and new coal technologies.

[^ref21]: Retrofits from Gas-CC to Gas-CC-CCS are also allowed.
    Additionally, Gas-CT plants are allowed to be retrofitted to burn a
    renewable energy fuel, such as hydrogen, green methane, or
    biodiesel. These retrofits can occur with existing Gas-CT plants or
    with new builds. Within ReEDS these plants are called RE-CT plants,
    and have the same O&M and heat rate as Gas-CT plants.

[^ref22]: Landfill gas generators are classified as conventional generators
    but can count toward renewable portfolio standard requirements.

[^ref23]: Net winter capacity is used to adjust the capacity available in
    ReEDS during winter timeslices. It is applied as a ratio between net
    winter capacity and net summer capacity.

[^ref24]: See <https://www.eia.gov/tools/faqs/faq.cfm?id=74&t=11>, accessed
    November 11, 2016.

[^ref25]: See <https://www.nrel.gov/analysis/reeds/request-access.html> to
    get access to the repository.

[^ref26]: Hydrogen can also be deployed to meet seasonal storage needs and
    is discussed more in [Hydrogen](#hydrogen).

[^ref27]: Values in 2016\$

[^ref28]: For details see <https://www.nrel.gov/hydrogen/sera-model.html>.

[^ref29]: The level of plant aggregation is a scenario input option. Plants
    can be aggregated to one plant type per region or left at their
    native unit-level resolution.

[^ref30]: When running with endogenous retirements, any technology type can
    be eligible to be retired endogenously by the model. However, some
    technologies are not represented properly to be appropriately
    considered for endogenous retirements.

[^ref31]: ReEDS does not account for any decommissioning costs for
    renewable or any other capacity type.

[^ref32]: Supply curves are nonlinear in practice, but a linear regression
    approximation has been observed to be satisfactory under most
    conditions.

[^ref33]: The elasticity coefficients are derived from all scenarios of
    AEO2018, but the price-demand set points are taken from any one
    single scenario of the AEO.

[^ref34]: This heuristic method of tracing a path from the POI to the
    largest load center in the zone is highly simplified and does not
    represent all the considerations involved in an actual
    interconnection study.

[^ref35]: For example, Vancouver and Portland are the largest populations
    centers in the southern Washington and northern Oregon regions
    respectively. However, these centers are only about 10 miles apart.
    Modeling such a short distance between these nodes would potentially
    create a bias for transmission investments between Washington and
    Oregon. So Yakima was used in lieu of Vancouver as the node location
    for southern Washington.

[^ref36]: See <https://www.neb-one.gc.ca/nrg/sttstc/lctrct/stt/lctrctysmmr/lctrctysmmr-eng.html>.

[^ref37]: Load balancing is implemented with equality constraints, so there
    is no physical representation of lost load and an associated cost.

[^ref38]: In ReEDS, capacity credit is defined as the fraction of nameplate
    capacity that contributes to the planning reserve requirement.

[^ref39]: LOLP is defined as the probability of a loss-of-load event in
    which the system load is greater than available generating capacity
    during a given period.

[^ref40]: ELCC is the contribution (units of MW that can then be reported
    as a fraction of the installed capacity to represent CV) that an
    additional resource provides toward meeting the system’s load while
    maintaining a fixed system-wide reliability level.

[^ref41]: When running intertemporally, these values are calculated after
    each intertemporal solve. The model solves, recomputes these values,
    then solves again, and continues until convergence is reached.

[^ref42]: Residual LDC, or RLDC, is an equivalent term to NLDC and is used
    in the literature.

[^ref43]: We currently use only a single year of wind, solar, and load data
    to calculate capacity. Expansion of this method to use multiple
    years of data would increase the robustness of this calculation, and
    it is currently under development.

[^ref44]: We refer to “existing” CV as the reliable capacity contribution
    from resources that have already been deployed in the model before
    the buildout of additional “marginal” resources.

[^ref45]: To account for forecasting errors and uncertainty in future
    loads, this curve is shifted by one hour of storage duration. Thus,
    2-hour storage gets full capacity credit for meeting peaks that are
    1 hour in duration, 4-hour storage gets full capacity credit for
    peaks that are 3 hours or shorter, etc.

[^ref46]: It is worth noting that storage resources can provide resources
    to the electricity grid beyond peaking capacity and energy
    arbitrage. A capacity-expansion model like ReEDS has limited
    representation of these services, but to the extent that they are
    represented in the model these services are captured when assessing
    energy storage. See the ReEDS documentation {cite}`brownRegionalEnergyDeployment2020`
    for more information on operating reserve representation in ReEDS.

[^ref47]: The PV reserve requirement is only valid during daytime hours
    when the PV systems are operating. In addition, the requirement is a
    function of capacity rather than generation because reserves are
    especially important around sunrise and sunset when PV generation is
    low.

[^ref48]: “2017 Model Rule,” accessed April 26, 2018,
    <https://www.rggi.org/program-overview-and-design/program-review>.
    For more information, see:

    “About the Regional Greenhouse Gas Initiative (RGGI),” fact sheet
    updated August 2016,
    <https://www.rggi.org/docs/Documents/RGGI_Fact_Sheet.pdf>

    “The RGGI CO<sub>2</sub> Cap,”
    <https://www.rggi.org/design/overview/cap>

    “Regional Greenhouse Gas Initiative,” December 2013,
    <http://www.c2es.org/docUploads/rggi-brief-12-18-13-updated.pdf>.

[^ref49]: RGGI press release officially adding New Jersey to the set of
    RGGI states,
    <https://www.rggi.org/sites/default/files/Uploads/Press-Releases/2019_06_17_NJ_Announcement_Release.pdf>

[^ref50]: New Jersey State press release, specifying New Jersey’s RGGI
    budget, <https://nj.gov/governor/news/news/562019/approved/20190617a.shtml>

[^ref51]: See <https://www.deq.virginia.gov/Portals/0/DEQ/Air/Regulations/c140p7.pdf>.

[^ref52]: Note that the eligible cost basis for MACRS is reduced by
    one-half the value of the tax credit.

[^ref53]: CCS projects are eligible for a direct pay option for the first 5
    years of the 45Q credit or until 2032 (whichever comes first), with
    the credits returning to non-refundable status after that point. The
    lower monetization penalty is meant to approximate the benefit of
    the direct pay option.

[^ref54]: See Barbose {cite:year}`barboseStateRenewablesPortfolio2023` and
    <https://emp.lbl.gov/projects/renewables-portfolio>.

[^ref55]: See Database of State Incentives for Renewables & Efficiency
    (DSIRE) website at [dsireusa.org](http://www.dsireusa.org/) . If
    data are unavailable, ReEDS forces RPS target to be met by using a
    default alternative compliance payment and solar alternative
    compliance payments of \$200/MWh and \$400/MWh respectively.

[^ref56]: Not all electricity produced in a state is subject to the state
    law. For example, electricity co-ops or federal entities might not
    be required to comply with the CES, leading to an effective CES
    fraction that is smaller than the one stated in the law.

[^ref57]: For Massachusetts, we assume CCS technologies are also eligible,
    but we disallow hydropower because of the post-2010 commercial
    operation date requirement in the state policy {cite}`doerElectricitySectorRegulations2018`.

[^ref58]: The modeled CES for CO<sub>2</sub> is assumed to start in 2020
    and includes the clean energy commitments from the largest electric
    utility in the state (Xcel Energy), which were codified into law in
    1.    The modeled CES for Massachusetts begins at 16% in 2018 and
    increases to 80% by 2050.

[^ref59]: To provide ReEDS with foresight to know that the phaseout is
    coming in Virginia, we implement an increasing capital cost
    financing multiplier to plants that are being phased out. This
    multiplier shortens the cost recovery period of the plant. For
    example, when evaluating whether to build a Gas-CC unit in 2040 (5
    years before the scheduled phaseout), the financial multiplier for
    Gas-CC includes a 5-year cost recovery period.

[^ref60]: See <https://www.ncsl.org/environment-and-natural-resources/states-restrictions-on-new-nuclear-power-facility-construction>.

[^ref61]: Previous work has found that accounting for mortality results in
    the largest component of monetized benefits {cite:p}`epau.s.environmentalprotectionagencyBenefitsCostsClean1999, nrcnationalresearchcouncilHiddenCostsEnergy2010` that
    PM<sub>2.5</sub> exposure is the driver of 90%–95% of all
    mortalities related to air pollution {cite:p}`tessumInMAPModelAir2017, tschofenFineParticulateMatter2019`.
    
[^ref62]: Additional description of the models and the marginal damage
    estimates used in ReEDS can be found at
    <u>https://www.caces.us/data</u>.

[^ref63]: Minimum load is an example of one such parameter. The aggregate
    representation of minimum load in ReEDS at the technology-BA level
    does not effectively reflect unit-level operating constraints used
    in PLEXOS, so PLEXOS uses native assumptions for minimum load.

[^ref64]: The long-run marginal emission rate is a metric designed to help
    estimate the emissions induced (or avoided) by a persistent change
    in electricity consumption. Unlike the short-run marginal emission
    rate, the long-run marginal emission rate reflects the structural
    changes to the grid that can be induced by a persistent change in
    electricity consumption.

[^ref65]: A quad is a quadrillion Btu, or 10<sup>15</sup> Btu.

[^ref66]: The default value of $\epsilon$ is assumed to be 0.76 from values
    estimated by Ponce and Neuman {cite:year}`ponceElasticitiesSupplyUS2014a`

[^ref67]: Exceptions include state-level policies, which are specified at
    the state level, NOx emission trading groups, and transmission
    interface limits between system operator boundaries.

[^ref68]: Prescribed builds are builds that are forced into the model
    because they have already been built or are under construction, such
    as the Vogtle nuclear power plant. Prescribed retirements are power
    plant retirements that are forced into the model based on actual
    retirements or retirement announcements.

[^ref69]: Older versions of the ReEDS model (version 2022 and earlier)
    included the full spatial dataset, and then subset the model
    equations to only include equations for the region of interest.