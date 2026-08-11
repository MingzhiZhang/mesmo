TUM School of Engineering and Design

## Multi-Energy System Modeling and Optimization (MESMO)

### Development of a Software Tool for District-Scale Electric and Thermal Energy System Operation

##### Sebastian Troitzsch

Vollständiger Abdruck der von der TUM School of Engineering and Design der Technischen Universität München zur Erlangung des akademischen Grades eines

##### Doktors der Ingenieurwissenschaften (Dr.-Ing.)

genehmigten Dissertation.

##### Vorsitzender

Prof. Dr.-Ing. Harald Klein

##### Prüfer der Dissertation

1. Prof. Dr. rer. nat. Thomas Hamacher
2. Prof. Xu Yan, Ph.D. Die Dissertation wurde am 09.08.2021 bei der Technischen Universität München eingereicht und durch die TUM School of Engineering and Design am 19.04.2022 angenommen.

## Abstract

District-scale energy systems are progressively evolving from unidirectional, top-down struc- tures into bidirectional, distributed and multi-commodity systems. This transformation is driven by efforts to decarbonize the energy sector as well as the advancement of control systems for distributed energy systems (DERs). Furthermore, the increased coupling of electric, thermal and other energy systems in terms of multi-energy systems (MESs) enables additional flexibility across conventional system boundaries. To this end, market-based mech- anisms under the transactive energy paradigm are being studied, primarily in the electric grid, for the safe operation of the distribution system by harnessing operational flexibility of DERs.

To facilitate the study of transactive energy frameworks for MESs, this thesis develops the Multi-Energy System Modeling and Optimization (MESMO) framework. MESMO is a software tool for optimal operation problems of district-scale electric grids, thermal grids and DERs, such as flexible loads (FLs), electric vehicle (EV) chargers, distributed generators (DGs) and energy storage systems (ESSs). It implements convex models for each subsystem along with a set of optimization-focused interfaces. Essentially, MESMO addresses the need for a software framework to model, define and solve numerical optimization problems in the MES context. This avoids the non-trivial coupling of domain-specific models, while enabling the usage of custom, high-fidelity models for each subsystem. A formal software development procedure is employed in this thesis to identify stakeholders, use cases and requirements in order to devise the software architecture of MESMO.

MESMO is employed for two studies in this thesis. In the first study, the impact of EV charging is evaluated for a synthetic test case based in Singapore. The results point to the need for incentive frameworks for EV charging to mitigate grid upgrades. To this end, the second study focuses on deployment of distribution locational marginal prices (DLMPs) for combined thermal and electric grids. In electric grids, DLMPs have been demonstrated as effective incentive signals for the economic dispatch of DERs while maintaining operational grid constraints. This thesis derives a formulation for DLMPs for thermal grids and demonstrates their ability to represent various operational scenarios in MES.

i

## Zusammenfassung

Energiesysteme im Quartiersmaßstab entwickeln sich zunehmend von unidirektionalen Top-Down-Strukturen zu bidirektionalen, verteilten Multi-Commodity-Systemen. Diese Trans- formation wird durch die Bemühungen zur Dekarbonisierung des Energiesektors sowie durch die Weiterentwicklung von Steuerungssystemen für dezentrale Energiesysteme, d.h. Distributed Energy Resources (DERs), vorangetrieben. Darüber hinaus ermöglicht die zunehmende Kopplung von elektrischen, thermischen und anderen Energiesystemen im Sinne von Multi-Energie-Systemen (MES) zusätzliche Flexibilität über konventionelle Sys- temgrenzen hinweg. Zu diesem Zweck werden marktbasierte Mechanismen unter dem Paradigma von Transactive Energy vor allem im elektrischen Netz für den sicheren Betrieb des Verteilungssystems durch die Nutzung der betrieblichen Flexibilität von DERs untersucht.

Um die Untersuchung von Transactive Energy Mechanismen für MESs zu erleichtern, entwick- elt diese Arbeit das Multi-Energy System Modeling and Optimization (MESMO) Framework. MESMO ist ein Software-Tool für optimale Betriebsprobleme von elektrischen Netzen, ther- mischen Netzen und DERs, wie z.B. flexible Lasten, Ladeinfrastruktur für Elektrofahrzeuge, verteilte Generatoren und Energiespeichersysteme. Es implementiert konvexe Modelle für jedes Subsystem zusammen mit einer Reihe von optimierungsorientierten Schnittstellen. Im Wesentlichen adressiert MESMO den Bedarf an einem Software-Framework zur Model- lierung, Definition und Lösung numerischer Optimierungsprobleme im MES-Kontext. Dies vermeidet die nicht-triviale Kopplung von domänenspezifischen Modellen und ermöglicht gleichzeitig die Verwendung von benutzerdefinierten Modellen für jedes Subsystem. In dieser Arbeit wird ein formales Softwareentwicklungsverfahren eingesetzt, um Stakeholder, Anwendungsfälle und Anforderungen zu identifizieren, sowie um die Softwarearchitektur von MESMO zu entwerfen.

MESMO wird in dieser Arbeit für zwei Studien eingesetzt. In der ersten Studie werden die Auswirkungen des Ladens von Elektrofahrzeugen für einen synthetischen Testfall in Singapur evaluiert. Die Ergebnisse weisen auf die Notwendigkeit von Anreizsystemen für das Laden von Elektrofahrzeugen hin, um die Anforderungen an den Netzausbau zu verringern. Zu diesem Zweck konzentriert sich die zweite Studie auf den Einsatz von Distribution Locational Marginal Prices (DLMPs) für kombinierte thermische und elektrische Netze. In elektrischen Netzen haben sich DLMPs als wirksame Anreizsignale für den wirtschaftlichen Einsatz von DERs bei gleichzeitiger Aufrechterhaltung der betrieblichen Netzbeschränkungen erwiesen. In dieser Arbeit wird eine Formulierung für DLMPs für thermische Netze abgeleitet und ihre Fähigkeit zur Darstellung verschiedener Betriebsszenarien in MES demonstriert.

ii

## Acknowledgments

I would like to thank all my former and current mentors, colleagues, friends and family for the various types of support that have enabled my work on this thesis.

Particularly, I am deeply grateful to Prof. Thomas Hamacher for providing key guidance and advice on the direction of my work. I greatly enjoyed our discussions and also appreciated his effort in making many connections to potential collaborators and experts to complement my work.

To TUMCREATE and Tobias Massier, I am very thankful for providing me with the opportunity to conduct this dissertation. Thank you also to Prof. Xu Yan for co-examining this thesis and also for the effective collaboration on various research projects.

This thesis would certainly not have been possible without Sarmad Hanif and Kai Zhang, who have set me on track towards the development of MESMO. Our extensive discussions on methodologies for electric grid modeling and operation are the bedrock of this work.

Of the former ESTL team of TUMCREATE, I also would like to thank Alex Lamprecht, Andrej Trpovski, Marc Gallet, Nitin Shivaraman, Srikkanth Ramachandran and all other colleagues for the great companionship throughout the past years.

Through student internships and thesis projects, this work was significantly supported by the fantastic work of Angelica Gonzales, Anthony Vautrin, Aurelie Moine, Christian Utama, Thanh Huynh, Tommaso Miori, Mischa Grussmann, Sherif Hashem, Sophia Spitzer and Wesley Poh.

The development of MESMO has also been spurred through a number of research projects and collaborations. To this end, I would like to thank the project teams of SITEM, PRIMO and CONCEPT. I was particularly delighted by the fruitful exchanges with Tom Schelo, Thomas Licklederer and Desmond Cai.

Last but not least, I am extremely thankful to my wife Xin Ling, for putting up with me during the challenging periods of thesis writing and for being a great partner throughout. Likewise, heartfelt thanks to my mother for always pushing me to do my best and to my whole family for their unconditional support.

iii

## Contents

**Abstract i**

**Acknowledgmentsiii**

**Contents iv**

**Notation ix**

**List of acronymsxi**

**List of symbolsxiii**

**List of algorithmsxviii**

**List of figuresxix**

**List of tablesxxi**

**1 Introduction1**

1.1 Motivation..................................... 1

1.2 Objectives.	3
1.3 Outline.. 4
1.4 Contributions.	5
1.5 Publications.. 7

1.2 Objectives.................................... 3
.

**I Background9**

**2 Fundamentals of district-scale energy systems10**

2.1 Electric grids.................................. 10
2.1.1 Overview................................ 10
2.1.2 Transmission systems.......................... 11
2.1.3 Distribution systems.......................... 12
2.1.4 Mathematical modeling......................... 13
2.2 Thermal grids.................................. 16
iv

<u>Contents</u>

2.3
**3**

3.1
3.2
3.3
3.4
**4**

4.1
4.2
4.3
2.2.1 Overview................................
2.2.2 District heating systems......................... 17
2.2.3 District cooling systems........................ 18
2.2.4 Bidirectional low-temperature networks................ 19
2.2.5 Distribution piping system....................... 19
2.2.6 Mathematical modeling......................... 20
Distributed energy resources........................... 21

2.3.1 Typology................................. 21
2.3.2 Distributed generators......................... 22
2.3.3 Loads.................................. 23
2.3.4 Storage systems............................ 25
2.3.5 Mixed DERs.............................. 26
Definition and concepts.............................. 27
Scope and problem types........................... 28
Modeling dimensions.............................. 29
Existing software frameworks......................... 30

Software development life cycle......................... 37

4.1.1 Life cycle stages............................. 37
4.1.2 Life cycle models............................ 38
Software requirements............................. 39

4.2.1 Requirements development...................... 39
4.2.2 Functional requirements........................ 40
4.2.3 Quality attributes............................. 41
Software architecture.............................. 42

4.3.1 Scope and outcomes.......................... 42
4.3.2 Design process............................. 42
4.3.3 Documentation............................. 43
**II**

**5**

5.1
5.2
Prerequisites................................... 47

5.1.1 Scope................................... 47
5.1.2 Use case modeling........................... 48
5.1.3 Functional requirements........................ 50
5.1.4 Quality attributes............................ 52
Software architecture.............................. 55

5.2.1 Overview................................ 55
5.2.2 Module structures........................... 55
v

##### Multi-energy system modeling and optimization27

##### Fundamentals of software development37

##### Methodology46

##### Software architecture of MESMO47

<u>Contents</u>

5.2.3 Workflow structures...........................
5.2.4 Allocation structures.......................... 70
##### 6 Electric grid modeling76

6.1 Fundamental electric grid model......................... 77
6.1.1 Scope and assumptions......................... 77
6.1.2 Single-phase power flow......................... 77
6.1.3 Three-phase power flow........................ 80
6.1.4 Multi-phase power flow.......................... 84
6.1.5 Line admittance model......................... 86
6.1.6 Transformer admittance model...................... 87
6.1.7 DER connection............................ 88
6.1.8 Source connection........................... 89
6.1.9 Source and no-source notation.................... 89
6.2 Non-linear power flow solution......................... 90
6.2.1 Outline................................. 90
6.2.2 Fixed-point method............................ 91
6.3 Linear approximate model........................... 92
6.3.1 Fundamental linear model....................... 92
6.3.2 Global approximation........................... 94
##### 7 Thermal grid modeling97

7.1 Fundamental thermal grid model........................ 98
7.1.1 Scope and assumptions........................ 98
7.1.2 Thermal power flow........................... 99
7.1.3 Pipe pressure loss model....................... 102
7.1.4 DER connection............................ 103
7.1.5 Source connection............................ 104
7.1.6 Source and no-source notation..................... 104
7.2 Non-linear power flow solution......................... 105
7.2.1 Outline................................. 105
7.2.2 Explicit method for radial networks.................. 106

|7.2.2|Explicit method for radial networks.||...|......|.....|... 106|
|---|---|---|---|---|---|---|
|Linear approximate model.||......|......|......|.....|.... 107|
|7.3.1|Fundamental linear model.|..|......|......|.....|.... 107|
|7.3.2|Global approximation for radial networks.|||......|.....|... 108|
|Fundamental DER model.||......|......|......|.....|.... 111|
|8.1.1|Scope and assumptions.|...|......|......|.....|.... 111|
|8.1.2|Fixed DER model.|......|......|......|.....|.... 111|
|8.1.3|Flexible DER model.|.....|......|......|.....|... 112|
|Fixed DERs.||......|......|......|.....|.... 114|
|8.2.1|Fixed loads.|......|......|......|.....|.... 114|
|8.2.2|Fixed EV chargers.|......|......|......|.....|.... 114|

7.3
##### 8 Distributed energy resource modeling110

8.1.
.

8.2........
....

vi

<u>Contents</u>

8.2.3 Fixed generators............................. 114
8.3 Flexible DERs................................... 114
8.3.1 Flexible loads............................... 114
8.3.2 Flexible generators........................... 116
8.3.3 Flexible EV chargers........................... 117
8.3.4 Flexible buildings............................. 121
8.3.5 Storage systems............................ 129
8.3.6 Cooling plants.............................. 131
8.3.7 Heating plants............................. 133
##### 9 Multi-energy system operation problem formulations135

9.1 Fundamental problem types.......................... 135
9.2 Nominal operation problem........................... 136
9.2.1 Outline................................. 136
9.2.2 Solution algorithm............................ 137
9.3 Optimal operation problem........................... 138
9.3.1 Outline................................. 138
9.3.2 Optimization problem.......................... 139
9.3.3 Distribution locational marginal prices................. 140
9.3.4 Solution algorithm............................ 147
##### IIIResults and discussion149

##### 10 Study of electric vehicle charging in Singapore150

10.1 Test case.................................... 150
10.1.1Overview................................ 150
10.1.2Electric grid................................ 151
10.1.3EV chargers.............................. 152
10.1.4Scenarios................................ 156
10.2 Results...................................... 157
10.2.1Uncontrolled charging.......................... 157
10.2.2Smart charging............................. 159
10.2.3Peak-shaving.............................. 159
10.2.4Price-based charging.......................... 159
10.3 Discussion.................................... 163
##### 11 Study of combined thermal and electric grid operation165

11.1 Test case.................................... 166
11.1.1Overview................................ 166
11.1.2Electric grid................................ 167
11.1.3Thermal grid.............................. 168
11.1.4Flexible buildings............................ 168
11.1.5Scenarios................................ 169
vii

<u>Contents</u>

11.2 Results.....................................
11.2.1Baseline................................. 170
11.2.2Constrained branch flow in the thermal grid.............. 172

|11.2.2|Constrained branch flow in the thermal grid.||||..|.....|....|.. 172|
|---|---|---|---|---|---|---|---|---|
|11.2.3|Constrained node head in the thermal grid.||||..|.....|....|... 174|
|11.2.4|Constrained branch power in the electric grid.||||.|.....|....|.. 176|
|11.2.5|Constrained node voltage in the electric grid.||||.|.....|....|... 177|
|11.2.6|High-cost cooling plant in the thermal grid.||||..|.....|....|.. 179|
|11.2.7|Low-cost cooling plant in the thermal grid.||||...|.....|....|.. 179|
|11.2.8|Low-cost generator in the electric grid.||||.....|.....|....|.. 180|
|11.3 Discussion.|.|......|.....|.....|......|.....|....|.. 182|

.

##### 12 Summary and conclusions184

12.1 Summary..................................... 184
12.2 Conclusions................................... 185
##### Bibliography187

viii

## Notation

#### Domains and sets

Domains are denoted by uppercase blackboard bold letters R*,*C, where R and C are the domains of real numbers and complex numbers. Sets are denoted by uppercase calligraphic letters as *S*, where individual elements of the set are denoted by lowercase italic letters as *s ∈S*. The symbol *N* *S* denotes the number of elements contained in set *S*.

#### Scalars, vectors and matrices

Non-bold letters *x*, *X* denote scalars R¹ *×*1 / C¹ *×*1, bold lowercase letters *x* denote vectors R *n×*1 / C *n×*1 and bold uppercase letters *X* denote matrices R *n×m* / C *n×m*. The expression

|[x] denotes the column vector of scalar values x||for all rows r ∈R and [x|]|
|---|---|---|---|
|r r∈R||r|r,c (r,c)∈R×C|
||r,c|||

denotes the matrix of scalar values *x* for all rows and columns (*r,c*) *∈R×C*.

The real and imaginary parts of a complex number *√* <u>x</u> *∈* C are denoted as Re(*x*) and Im(*x*). The symbol *j* denotes the imaginary number *j* = *−*1. The symbols 0 and 1 denote vectors or matrices of zeros and ones of appropriate size. The symbol *I* is the identity matrix of appropriate size.

#### Mathematical operations

The partial derivative of *x* with regards to *y* is denoted by <u>δx</u> *δy*, whereas the total derivative is denoted by *dx* *dy*. The time derivatives *dx* *dt* and *ddtx* are denoted by *x*˙ and *x*˙. The p-norm of a vector is denoted by *||x||p*. The transpose of a vector or matrix is denoted by () ⊺. The matrix diag(*x*) denotes the diagonal matrix of diagonal entries *x*. Note that diag(*x*)*y* is equivalent to the Hadamard product *x ⊙ y*, i.e. the element-wise multiplication of vectors *x* and *y*. Similarly, the inverse diag(*x*) *−*1 is equivalent to the diagonal matrix of the element-wise inverse of vector *x*. These equivalences may be utilized in source code implementations for more efficient operations.

ix

<u>Notation</u>

#### Physical properties and units

Symbols for physical properties are aligned with ISO 80000 and their units are based on the international system of units (SI). Prices and costs are in Singapore Dollar (SGD) which is denoted by S$.

#### Date-time, time-period and time-delta formats

Time steps *t* can be defined in date-time format *t ∈* T or time-period format *t ∈* P, whereas time intervals ∆*t* can be defined in time-delta format ∆*t ∈* D. The date-time format denoted by T is described by ISO 8601, i.e. yyyy-mm-ddTHH:MM:SS, where yyyy denotes the year, mm denotes the month, dd denotes the day, HH denotes the hour, MM denotes the minute and SS denotes the second, e.g. 2021-07-31T23:59:59.

The time-period format denoted by P refers to day and time in a week, which is based on a variation of ISO 8601 as ddTHH:MM:SS, where dd denotes the weekday (01 for Monday, 07 for Sunday), HH denotes the hour, MM denotes the minute and SS denotes the second, e.g. 06T13:00:00 for 1pm on Saturday. The time-delta format denoted by D refers to the interval between time steps and is described based on a variation of ISO 8601 as HH:MM:SS, where HH denotes the hour, MM denotes the minute and SS denotes the second, e.g. 00:30:00 for a time interval of 30 min.

x

## List of acronyms

##### AcronymDescription

ACAlternating Current

ADMMAlternating Direction Method of Multipliers

ADMSAdvanced Distribution System Management System

ASRArchitecturally Significant Requirement

APIApplication Programming Interface

BESSBattery Energy Storage System

BLTNBidirectional Low-Temperature Network

CHPCombined Heat and Power

COPCoefficient of Performance

CoBMoControl-oriented Building Model

CSVComma-separated Values

DCDirect Current

DCPDistrict Cooling Plant

DCSDistrict Cooling System

DERDistributed Energy Resource

DERMSDistributed Energy Resource Management System

DGDistributed Generator

DHPDistrict Heating Plant

DHSDistrict Heating System

DLMPDistribution Locational Marginal Price

DSFDemand Side Flexibility

EMCEnergy Market Company

EMAEnergy Market Authority

EVElectric Vehicle

xi

<u>List of acronyms</u>

ESSEnergy Storage System

ETSEnergy Transfer Station

FLFlexible Load

GUIGraphical User Interface

HPHeat Pump

HVACHeating, Ventilation and Air-Conditioning

ISOIndependent system operator

KKTKarush–Kuhn–Tucker

LMPLocational Marginal Price

MESMulti-Energy System

MESMOMulti-Energy System Modeling and Optimization

NEMSNational Electricity Market of Singapore

OPFOptimal Power Flow

PSOPower System Operator

PVPhotovoltaic

QCQPQuadratically Constrained Quadratic Program

SDLCSoftware Development Lifecycle

SDPSemi-definite Program

SOCPSecond-Order-Conic Program

SPSingapore Power

TESSThermal Energy Storage System

TSOTransmission System Operator

UMLUnified Modeling Language

V2GVehicle-to-grid

VPPVirtual Power Plant

xii

## List of symbols

#### Electric grid modeling

|SymbolDescription||Unit|
|---|---|---|
|, N|Set of all electric grid nodes n ∈N|–|
|, B|Set of all electric grid branches b ∈B Set of all DERs in the electric grid d ∈D|– –|
||Nodal current injection|A|
|, i|Nodal wye current injection|A|
|, i|Nodal delta current injection|A|
|, s|Nodal wye power injection|VA|
|, s|Nodal delta power injection|VA|
||Nodal voltage|V|
|, u|Source node voltage|V|
|, u|Nodal no-load voltage|V|
|, i|Complex branch current flow in “from” direction|A|
|, s|Complex branch power flow in “from” direction|VA|
|, i|Complex branch current flow in “to” direction|A|
|, s|Complex branch power flow in “to” direction|VA|
||Total complex power loss DER complex power, where s = p + jq|VA VA|
||DER active power|W|
||DER reactive power|VAr|
|, Y|Element series admittance||
|, Y|Element shunt admittance||

*el el el* *N* *el el el* *B* *el el* *D*

*i*, *i* *Y Y* *i* ∆ ∆ *i* *Y Y* *s* ∆ ∆ *s*

*u*, *u* *sr sr* *u* *nl nl* *u* *f f* *i* *f f* *s* *t t* *i* *t t* *s* *ls* *s*

*s*, *s*

*p*, *p*

*q*, *q* *se se* *y* Ω *sh sh* *y* Ω

##### r, R Element resistance Ω

xiii

##### <u>List of symbols</u>

##### x, x Element inductive reactance Ω

##### c, C Element capacitance F

*Y* Nodal admittance matrix Ω *f/t* *Y* Branch admittance matrix in “from” / “to” direction Ω *f/t* *A* Branch incidence matrix in “from” / “to” direction *Y* *A* DER wye mapping matrix ∆ *A* DER delta mapping matrix

##### Γ Delta phase mapping matrix

*H* Aggregated delta phase mapping matrix *sr* *A* Source mapping matrix *ns* *A* No-source mapping matrix *|u|,p* *M* Sensitivity of the voltage magnitude with respect to active power V/W *|u|,q* *M* Sensitivity of the voltage magnitude with respect to reactive power V/VAr *|sf/t|,p* *M* Sensitivity of the branch power flow magnitude in “from” / “to” direction VA/W with respect to active power *|sf/t|,q* *M* Sensitivity of the branch power flow magnitude in “from” / “to” direction VA/VAr with respect to reactive power *pls,p* *M* Sensitivity of the active loss with respect to active power W/W *pls,q* *M* Sensitivity of the active loss with respect to reactive power W/VAr *qls,p* *M* Sensitivity of the reactive loss with respect to active power W/W *qls,q* *M* Sensitivity of the reactive loss with respect to reactive power W/VAr

#### Thermal grid modeling

|SymbolDescription||Unit|
|---|---|---|
||Set of all thermal grid nodes n ∈N Set of all thermal grid branches b ∈B Set of all DERs in the thermal grid d ∈D|– – –|
|, q|Nodal volume flow injection|m³/s|
|, q|Nodal thermal power injection|W|
|, p|Nodal static pressure Nodal pressure head Source node pressure head No-load pressure head|Pa m m m|

*th th* *N* *th th* *B* *th th* *D* *th,n th,n* *q* *th,n th,n* *q* *st st* *p*

*h*, *h* *sr* *h* *nl* *h*

xiv

##### <u>List of symbols</u>

*th,f th,b* *q*

|, q|Branch volume flow in “from” direction|m³/s|
|---|---|---|
|, q|Branch volume flow in “to” direction|m³/s|
|, q|Branch volume flow, where q|m³/s|
|, v|Branch average fluid velocity in “from” direction|m/s|
|, v|Branch average fluid velocity in “to” direction|m/s|
|, v|Branch average fluid velocity, where v|m/s|
||Total pump power demand|W|
|, p|DER thermal power Enthalpy difference between primary and secondary side of the ther- mal grid|W J/m³|
|, d, r|Branch pipe diameter Branch loss coefficient|m|
||Pump efficiency Hydraulic head loss across the ETS Total head loss across the branch Friction head loss across the branch|W m m m|
||Friction loss factor Minor head loss across the branch|m|

*th,b th,b* *q* *th,b*

|th,b th,b|th,f|th,t||
|---|---|---|---|
|f f||||
|t t||||
|b b pm th th th|b|f|t|

*q* = *q* = *−q*

*v*

*v*

##### v = v = −v

*p* th *p*

∆*h*

*th th* *d* *th th* *r* *th,pm* *η* *ets* ∆*h* *th* ∆*h* *fr* ∆*h* *fr* ∆*f* *mn* ∆*h* *mn* ∆*f* Minor loss factor

*Re* Reynolds number *th,f/t* *A* Branch incidence matrix in “from” / “to” direction *th,b th,b th,f th,t* Branch incidence matrix, where *A*

|A|= A|− A|||
|---|---|---|---|---|
|th,b th,d sr ns|th,b|th,f|th,t||
|h,p||||th|
|q ,p||||th|
|p ,p||||th|

*A* Branch incidence matrix, where *A* = *A − A*

##### A DER mapping matrix

##### A Source mapping matrix

*A* No-source mapping matrix *th* *M* Sensitivity of the pressure head with respect to thermal power m/W *th,b th*3 *M* Sensitivity of the volume flow with respect to thermal power m /s/W *pm th* *M* Sensitivity of the pump loss with respect to thermal power W/W

xv

##### <u>List of symbols</u>

#### DER modeling

##### SymbolDescription

|||Unit|
|---|---|---|
|Set of all DERs, where D = D||–|
|State vector|multiple||
|Initial state vector|multiple||
|Control vector|multiple||
|Output vector|multiple||
|Active power||W|
|Nominal active power||W|
|Reactive power||VA|
|Nominal reactive power||VA|
|Thermal power||W|
|Nominal thermal power||W|
|Input power value|multiple||
|Electric grid connection indicator, where a|||
|Thermal grid connection indicator, where a|||
|State matrix|multiple||
|Control matrix|multiple||
|Disturbance matrix|multiple||
|State output matrix|multiple||
|Control output matrix|multiple||
|Disturbance output matrix|multiple||
|Active power output mapping matrix|multiple||
|Reactive power output mapping matrix|multiple||
|Thermal power output mapping matrix|multiple||

*el th* *D ∪D*

*x*

*x⁰*

*c*

*y*

*p* *nm* *p*

*q* *nm* *q* *th* th *p* *th,nm* th *p* *in* *p* *el el* *a ∈{*0*,*1*}* *d* *th th* *a ∈{*0*,*1*}* *d* *A* *c* *B* *d* *B*

*C* *c* *D* *d* *D* *p,y* *M* *q,y* *M* *pth,y* *M*

#### MES operation problem formulations

##### SymbolDescription Unit

*rf,el* *c* Marginal cost of electric power at the source node of the electric grid S$/W *rf,th* th *c* Marginal cost of thermal power at the source node of the thermal grid S$/W *sr* *p* Active power injection at the source node W *sr* *q* Reactive power injection at the source node VA

xvi

##### <u>List of symbols</u>

*th,sr* th *p* Thermal power injection at the source node W

*µ*, *µ* Dual variable / Lagrange multiplier associated with inequality con-multiple straints *λ*, *λ* Dual variable / Lagrange multiplier associated with equality constraints multiple

*L* Lagrangian function S$ *p* *π* Active power DLMP S$/W *p,e* *π* DLMP electric energy component for the electric grid S$/W *p,u* *π* DLMP voltage support component for the electric grid S$/W *p,s* *π* DLMP branch congestion component for the electric grid S$/W *p,ls* *π* DLMP loss component for the electric grid S$/W *pth*th *π* Thermal power DLMP S$/W *pth,e* th *π* DLMP thermal energy component for the thermal grid S$/W *pth,u* th *π* DLMP pressure head support component for the thermal grid S$/W *pth,s* th *π* DLMP branch congestion component for the thermal grid S$/W *pth,ls* th *π* DLMP pump loss component for the thermal grid S$/W

xvii

## List of algorithms

|1 Electric power flow solution based on fixed-point method.|...|....|.. .93|
|---|---|---|---|
|2 Thermal power flow solution based on the explicit method for radial networks107||||
|3 Solution algorithm for the nominal operation problem.|......|....|.. .137|
|4 Solution algorithm for the optimal operation problem.|......|....|.. .148|

xviii

## List of figures

4.1 Exemplary use case diagram..........................40
4.2 Exemplary component diagram..........................44
4.3 Exemplary code diagram............................45
5.1 Use case diagram for MESMO.........................48
5.2 Context view of MESMO............................56
5.3 Component view of MESMO...........................57
5.4 Code view of the configuration module.....................58
5.5 Code view of the utility module.........................59
5.6 Code view of the data interface module.....................61

|5.6|Code view of the data interface module..||....|......|.....|... .61|
|---|---|---|---|---|---|---|
|5.7|Code view of the electric grid models module..||.|......|.....|.. .62|
|5.8|Code view of the thermal grid models module..||.|......|.....|... .64|
|5.9|Code view of the DER models module..||.....|......|.....|.. .65|
|5.10|Code view of the problems module..|.|......|......|.....|.. .66|
|5.11|Workflow diagram of the nominal operation problems..|||...|.....|... .67|
|5.12 5.13|Workflow diagram of the optimal operation problems.. Container view of MESMO, highlighting the external software dependencies.71|||...|.....|.. .69|
|5.14|Repository structure of MESMO..|..|......|......|.....|.. .73|
|6.1|Single-phase power flow between two nodes of the electric grid..||||..|.. .78|
|6.2|Three-phase power flow between two nodes of the electric grid..||||..|... .81|
|6.3|Three-phase wye and delta connection of DER injections..||||.....|.. .83|
|6.4|Multi-phase power flow between two nodes of the electric grid..||||...|... .84|
|7.1|Thermal power flow between two nodes of the thermal grid..||||....|.. .99|
|10.1|Synthetic grid layout for the Geylang district in Singapore..||||.....|.. .152|
|10.2|Workflow for EV charger demand modeling..||..|......|.....|.. .152|
|10.3|EV carpark simulation..|.....|......|......|.....|.. .155|
|10.4|Substation transformer utilization for uncontrolled charging..||||.....|.. .158|
|10.5|Line utilization for uncontrolled charging..||....|......|.....|.. .158|
|10.6 10.7|Node voltage drop for uncontrolled charging.. Aggregated active power demand schedule for uncontrolled charging..||..|......|.....|.. .160. .160|
|10.8|Substation transformer utilization for smart charging..|||...|.....|... .161|
|10.9|Aggregated active power demand schedule for peak-shaving..||||...|.. .162|

...

xix

##### <u>List of figures</u>

10.10 Substation transformer utilization for peak-shaving..............162
10.11 Aggregated active power demand schedule for price-based charging....163
10.12 Substation transformer utilization for price-based charging..........163
11.1 Test case area at the Tanjong Pagar Port Terminal. Figure taken from [39].166
11.2 Test case layout with thermal grid, electric grid and flexible buildings.....167
11.3 Street layout at the test case site........................168
11.4 Test case layout with nodes of interest “A”, “B” and “C” highlighted......169
11.5 DLMPs and dispatch schedules at DER 22 for scenario 1 (Baseline).....171
11.6 Thermal grid DLMPs at 12:00 for scenario 1 (Baseline)............172
11.7 Electric grid DLMPs at 12:00 for scenario 1 (Baseline)............173
11.8 DLMPs and dispatch schedules at DER 22 for scenario 2 (Constrained
branch flow in the thermal grid).........................173

11.9 Thermal grid DLMPs at 12:00 for scenario 2 (Constrained branch flow in the
thermal grid)....................................174

11.10 DLMPs and dispatch schedules at DER 22 for scenario 3 (Constrained node
head in the thermal grid)............................175

11.11 Thermal grid DLMPs at 12:00 for scenario 3 (Constrained node head in the
thermal grid)...................................175

11.12 DLMPs and dispatch schedules at DER 22 for scenario 4 (Constrained
branch power in the electric grid)........................176

11.13 Electric grid DLMPs at 12:00 for scenario 4 (Constrained branch power in
the electric grid)..................................177

11.14 DLMPs and dispatch schedules at DER 22 for scenario 5 (Constrained node
voltage in the electric grid)...........................178

11.15 Electric grid DLMPs at 12:00 for scenario 5 (Constrained node voltage in the
electric grid)...................................178

11.16 DLMPs and dispatch schedules at DER 23 for scenario 6 (High-cost cooling
plant in the thermal grid)............................179

11.17 DLMPs and dispatch schedules at DER 22 for scenario 7 (Low-cost cooling
plant in the thermal grid)............................180

11.18 Thermal grid DLMPs at 12:00 for scenario 7 (Low-cost cooling plant in the
thermal grid)....................................181

11.19 DLMPs and dispatch schedules at DER 24 for scenario 8 (Low-cost generator
in the electric grid)................................181

11.20 Electric grid DLMPs at 12:00 for scenario 8 (Low-cost generator in the electric
grid).......................................182

xx

## List of tables

2.1 Representative state and control variables of the electric grid..........14
2.2 Representative state and control variables of the thermal grid.........20
3.1 Software tools for district-scale energy system simulation and optimization...31
10.1 EV charging demand input data.........................153
10.2 EV and charger parameters...........................153
10.3 EV penetration scenarios.............................154
10.4 Scenarios for the study of EV charging in Singapore..............156
11.1 Scenarios for the study of combined thermal and electric grid operation...170
xxi

## 1 Introduction

#### 1.1 Motivation

District-scale energy systems, such as electric distribution systems, district heating systems (DHSs) and district cooling systems (DCSs), have traditionally been operated top-down, with energy being distributed unidirectionally from a centralized source towards distributed consumers. In the electric distribution system, the prevailing paradigm has been termed “fit-and-forget” [1], i.e. the system is designed to sustain the rated peak demand of the consumers but is not actively operated. In the face of efforts to decarbonize the energy 1 sector and due to advancements in control systems, distributed energy resources (DERs) such as distributed generators (DGs), flexible loads (FLs) and energy storage systems (ESSs) are progressively being deployed in district-scale energy systems. At the same time, the increasing coupling of electric, thermal and other energy systems facilitates a transition towards multi-energy systems (MESs), thereby unlocking operational synergies across conventional system boundaries.

There is a paradigm shift towards smart grids or active distribution networks [3] in the electric energy sector as well as bidirectional low-temperature networks (BLTNs) [4] or 5th generation district heating and cooling [5] in the thermal energy sector. These system architectures aim to harness operational flexibility from controllable DERs, e.g. FLs and ESSs, to ensure the safe operation of electric distribution systems, DHSs and DCSs. However, if not controlled appropriately, DERs can pose challenges to the local energy system by introducing high volatility, e.g. from renewable DGs, or excessive peak demand, e.g. from uncontrolled electric vehicle (EV) charging. To this end, both direct and indirect control schemes have been proposed [6]. In the case of direct control, advanced distribution system management systems (ADMSs) [7] or DER management systems (DERMSs) [8] facilitate the operational optimization of the entire district-scale energy system, including DERs. However, such an arrangement may be unsuitable if different stakeholders manage DERs and distribution systems. To this end, other research works [9], [10] have proposed the establishment of district-scale energy markets under the transactive energy paradigm, where the district energy system operator exercises indirect control of DERs through price signals.

At present, district-scale energy market frameworks are discussed primarily for the electric energy sector. For example, distribution locational marginal prices (DLMPs) [11] have been 1 This work defines DERs according to IEC 61850-7-420 [2, Section 3.2.9], as discussed in section2.3.1.

<u>1. Introduction 1.1. Motivation</u> studied extensively for the electric distribution system. DLMPs refer to nodal electricity prices, which express the marginal cost of supplying load at a particular grid node. Specifically, DLMPs incorporate information on losses and congestion in addition to the marginal genera- tion costs. For example, DLMPs will increase at nodes that are served through a congested line, therefore serving as an incentive to reduce the load at these nodes to alleviate the congestion. Hence, DLMPs can be integrated into district-scale energy market-clearing mech- anisms to add consideration for the distribution system operation limits [12], [13]. In principle, the DLMP framework can be readily employed to enable economic and safe operation of MESs as well. For DHSs and DCSs, the distribution piping system can be modeled in an equivalent fashion as the electric distribution system, which naturally leads to an extension of DLMPs for the complete MES [14]. However, the modeling of MESs requires the non-trivial coupling of domain-specific models for each commodity. Additionally, the formulations of energy market frameworks as well as direct control frame- works in recent research are typically based on numerical optimization [15]. For example, the market-clearing problem can be expressed as an optimization problem for maximizing overall social welfare [11, p. 99, Section 5.3.1]. Similarly, the operation problem of ADMSs or DERMSs can be posed as an optimal control problem for the minimization of operation costs. To this end, the study of these frameworks increasingly requires the interfacing of dedicated numerical optimization solvers. Furthermore, applications such as DLMPs rely on convex model formulations for the underlying energy systems. Since these models may not be readily available from conventional power system analysis software, the research community has relied on the manual implementation of mathematical models through suitable solver interfaces, e.g. YALMIP [16], Pyomo [17], CVXPY [18], JuMP [19]. However, the scalability of such implementations is limited beyond research-scale test cases. Nevertheless, a complete software package that enables the expression of MES optimization problems for transactive energy applications is not readily available. The above-outlined challenges can be synthesized into the fundamental requirements for a software system to holistically support the modeling, definition and solution of convex opti- mization problems of district-scale MESs to facilitate the study of DER integration frameworks across conventional system boundaries. The fundamental needs can be summarized as follows:
- The modeling of all relevant subsystems of MES in a coupled manner, e.g. district-scale grids in conjunction with DERs.
- Mathematical models can be obtained in a convex fashion and are directly compatible with numerical optimization solver interfaces.
- Both direct control frameworks, i.e. centralized optimization problems, and indirect control frameworks, i.e. market-based decentralized optimization problems can be expressed.
- Implemented problem formulations must be scalable, i.e. suited both for research-scale and application-scale studies.
2

<u>1. Introduction 1.2. Objectives</u> Software tools for energy system analysis have traditionally focused on simulation appli- cations. In power system analysis, this includes for example OpenDSS [20], DIgSILENT PowerFactory [21] and MATPOWER [22], which implement solution algorithms for the non- linear power flow in the electric grid. With the advancement of numerical optimization in energy system research, some tools have been extended with modules for optimal power flow (OPF) studies, e.g. MATPOWER and DIgSILENT PowerFactory. At the same time, dedicated optimization-focused tools have been developed with a focus on MES planning problems, such as Homer [23], Calliope [24], urbs [25] and the City Energy Analyst (CEA) [26]. On the other hand, few tools such as PowerModels.jl [27] have focused on high-fidelity modeling of a single subsystem for optimal operation problems. At the same time, a class of software tools for the study of DER integration has evolved, e.g. with GridLAB-D [28] and the Open Platform for Energy Networks (OPEN) [29]. However, none of these tools addresses all of the above key needs at the same time.
#### 1.2 Objectives

To address the identified challenges in MES operation, the key objectives of this work are captured as follows:

1. To develop an open-source software framework for the modeling, simulation and optimization of district-scale MESs.
2. To derive DLMPs for district-scale thermal grids², i.e. DHSs and DCSs, in conjunction with formulating a convex modeling framework for the thermal grid. This is intended to complement the readily available methodologies for the electric grid, such that thermal and electric grids can be operated in the same fashion.
3. To study the characteristics of DLMPs in the MES context and to analyze their suitability as incentive mechanism in the operation of combined electric and thermal energy systems.
The development of the Multi-Energy System Modeling and Optimization (MESMO) frame- work is the core contribution of this work, with the majority of this thesis structured around its software development and mathematical modeling fundamentals. MESMO is intended as a software tool for operation problems of electric grids, thermal grids and DERs, such as flexible building loads, EV chargers, distributed generators (DGs) and energy storage systems (ESS). It implements convex modeling techniques for electric grids, thermal grids and DERs, along with a set of optimization-focused utilities. Essentially, MESMO is a software framework for defining and solving numerical optimization problems in the electric / thermal grid context, such as OPF, market-clearing with network constraints, strategic offering or MES dispatch problems. The tool also includes classical steady-state non-linear power flow models for electric and thermal grids. 2 “Thermal grid” will be used as a synonym for DHSs and DCSs in the remainder of this work.

<u>1. Introduction 1.3. Outline</u> Based on modularized electric grid models, thermal grid models and DER models, MESMO is intended to support constructing custom problem formulations for MESs in a plug-and-play fashion. Initially, to address the most common needs, nominal operation problems and optimal operation problems will be directly provided in MESMO. The nominal operation problem describes a traditional simulation problem for the MES, i.e. based on a-priori projections for the DER dispatch schedules. The optimal operation problem describes a numerical optimization problem for the optimal dispatch of DERs with regards to the operational constraints of the electric grid, thermal grid and DERs, where the objective function defaults to the maximization of social welfare based on predefined wholesale energy prices and DER production costs and utility functions. As part of the formulation of the optimal operation problem definition for MESs, this thesis also derives a fundamental model of DLMPs for combined thermal and electric grids. A linear approximate modeling technique is applied to obtain a convex model for the power flow in the thermal grid. Such models are readily available for electric grids but have not yet been widely studied for thermal grids. The DLMPs are derived from the dual problem of the MES optimal operation problem, where the importance of this contribution is twofold. First, a case study in the final portion of this thesis demonstrates the ability of DLMPs to act as incentive signals for flexible DERs. Second, this demonstrates the possibility of re-applying many existing transactive energy system techniques from the electric energy sector to the thermal energy sectors or other commodity networks in MESs. The thesis concludes with two case studies based on MESMO. In the first study, the impact of EV charging is evaluated for a synthetic test case based in Singapore. The results point to the need for incentive frameworks for EV charging to mitigate grid upgrades. To this end, the second study focuses on the deployment of distribution locational marginal prices (DLMPs) for combined thermal and electric grids. In electric grids, DLMPs have been demonstrated as effective incentive signals for the economic dispatch of DERs while maintaining operational grid constraints. This thesis derives a formulation for DLMPs for thermal grids and demonstrates their ability to represent various operational scenarios of MESs.
#### 1.3 Outline

The thesis is structured around developing the Multi-Energy System Modeling and Optimiza- tion (MESMO) framework and is intended to serve as documentation for the tool. The main body of the work is divided into the background (partI), methodology (partII) and results (partIII).

PartIbegins with establishing the required fundamentals of district-scale energy systems in chapter2. This is followed by reviewing the state of the art in MES modeling and optimization in chapter3. Finally, chapter4establishes the fundamentals of software development, which are immediately utilized in chapter5at the beginning of partIIto establish the software architecture for MESMO.

<u>1. Introduction 1.4. Contributions</u> Based on the fundamental module structure of MESMO from chapter5, the mathematical models for each of the MES subsystems, i.e. electric grids, thermal grids and DERs, are developed in chapters6to8. Chapter9then defines the mathematical formulation of optimal operation problems for MESs and derives the definitions for DLMPs in this context. The mathematical model and problem definitions in partIIform the core of the MESMO software implementation. MESMO is then applied for two studies in partIII: 1) Study of electric vehicle charging in Singapore in chapter10and 2) Study of combined thermal and electric grid operation in chapter11. For each study, the data inputs and pre-processing steps to develop the test case are presented along with the results and discussion. Eventually, the thesis concludes with summary and outlook in chapter12.
#### 1.4 Contributions

The contributions of this thesis rely and build upon previous research works, particularly with regards to electric grid modeling and test case development. The content of this thesis is structured to present each topic coherently, thereby mixing original contributions with adaptations of previous works. For the sake of clarity, the following distinguishes the contributions of this thesis from the derivatives of other works:

- **Background** (chapters2to4): **–** This part of the thesis constitutes a review of fundamentals and existing research works regarding electric grids, thermal grids, DERs, MESs and software develop- ment. The contribution lies solely in the arrangement, presentation and discussion of the content.
- **Software architecture of MESMO** (chapter5): **–** This chapter constitutes the core contribution of the thesis. The author entirely derived the definitions of stakeholders, use cases, requirements and software architecture. This forms the foundation for the software implementation of MESMO. A precursor of this work has been published by the author in [30]. Note that the author has also been the core developer and maintainer of the MESMO software repository.
- **Electric grid modeling** (chapter6): **–** The fundamental modeling methodologies presented in this chapter are derived from [11], [31]–[33]. However, the model formulation has been redeveloped for this thesis for a more consistent presentation than previous works. **–** The non-linear power flow solution and the linear approximate modeling are based on the works [11], [34] and have only been restated and corrected in this thesis.
- **Thermal grid modeling** (chapter7):
5

<u>1. Introduction 1.4. Contributions</u> **–** The fundamental thermal grid model and non-linear thermal power flow solution
have been redeveloped for this thesis but are essentially adapted from the estab- lished fundamentals for water distribution systems, DCSs and DHSs in [35]–[38]. This portion of the work was supported through the master theses [39], [40], which the author supervised. **–** An entirely original contribution of this thesis is the linear approximate thermal grid model in this chapter, which serves as the basis for formulating the thermal grid DLMPs in chapter9. This work was previously published by the author in [14], [41].

- **Distributed energy resource modeling** (chapter8): **–** The fundamental fixed and flexible DER model representations in this chapter have been chosen to suit the modeling framework of MESMO. However, these rep- resentations do not differ significantly from the prevailing formulation in previous works. Nevertheless, note the important choice for keeping flexible DER models in state-space form for notational coherence across all DER types, inspired by works in the building modeling domain [42], [43]. **–** As minor original contributions, the models for fixed loads, fixed EV chargers, fixed generators, flexible loads, flexible EV chargers and flexible generators have been developed as part of this thesis. **–** The flexible building model is an original work of the author but has primarily been developed as part of the author’s master thesis in [44]. As part of this Ph.D. thesis, the model was implemented and published in the Control-oriented Building Model (CoBMo) toolbox in [45], which includes contributions from supervised master students in [46]–[49]. **–** The storage system, cooling plant and heating plant models are original but minor contributions of this thesis, whose development was supported through two supervised master theses [39], [40].
- **Multi-energy system operation problem formulations** (chapter9): **–** The fundamental MES problem representations have been significantly redevel- oped to coherently present their implementation in MESMO, although the problem types themselves are well established. **–** A core contribution of the thesis in this chapter is the derivation of DLMPs for thermal grids. Combined with the derivation of DLMPs for electric grids based on [11], [34], this is utilized to form the complete set of DLMPs for the MES. This work was previously published by the author in [14], [41].
- **Study of electric vehicle charging in Singapore** (chapter10): **–** The test case for this study relies on 1) a synthetic electric grid test case for Singapore, which was developed in [50], [51], and 2) the synthetic EV charging demand, which was developed as an original contribution of this thesis. **–** The execution of the study via MESMO and interpretation of the results was conducted independently by the author.
6

<u>1. Introduction 1.5. Publications</u>
- **Study of combined thermal and electric grid operation** (chapter11): **–** The test case for this study was first developed as part of the Connecting District Energy and Power Systems in Future Singaporean New Towns (CONCEPT) project with contributions of the author and relies on previous works published in [26], [52]. The author adapted the test case to derive the thermal grid definition and developed the operational scenarios. A version of this test case was also utilized for the master theses [39], [40], which were supervised by the author. **–** The execution of the study via MESMO and interpretation of the results was conducted independently by the author.
#### 1.5 Publications

In addition to the thesis at hand, the following software releases and publications have been contributed as part of the Ph.D. dissertation. With regards to the software releases, both tools were entirely developed from the ground up and initially released in the course of this dissertation.

##### Publications, 1st-author

1. **S. Troitzsch**, K. Zhang, T. Massier, and T. Hamacher, “Coordinated market-clearing for Combined Thermal and Electric Distribution Grid Operation,” presented at the IEEE Power & Energy Society General Meeting (PESGM), Jul. 2021. doi: 10.36227/techr xiv.13247246.
2. **S. Troitzsch**, M. Grussmann, K. Zhang, and T. Hamacher, “Distribution Locational Marginal Pricing for Combined Thermal and Electric Grid Operation,” 2020. doi: 10.1 109/ISGT-Europe47291.2020.9248832.
3. **S. Troitzsch**, B. K. Sreepathi, T. P. Huynh, A. Moine, S. Hanif, J. Fonseca, and T. Hamacher, “Optimal electric-distribution-grid planning considering the demand-side flexibility of thermal building systems for a test case in Singapore,” Applied Energy, vol. 273, p. 114917, Sep. 2020, doi: 10.1016/j.apenergy.2020.114917.
4. **S. Troitzsch** and T. Hamacher, “Control-oriented Thermal Building Modelling,” Aug.
2020. doi: 10.1109/PESGM41954.2020.9281503.
5. **S. Troitzsch**, S. Hanif, K. Zhang, A. Trpovski, and T. Hamacher, “Flexible Distribution Grid Demonstrator (FLEDGE): Requirements and Software Architecture,” presented at the IEEE Power & Energy Society General Meeting (PESGM), Atlanta, GA, USA, Aug.
2019. doi: 10.1109/PESGM40551.2019.8973567.
6. **S. Troitzsch**, S. Hanif, and T. Hamacher, “Distributed Robust Reserve Scheduling in Congested Distribution Systems,” presented at the IEEE Power & Energy Society General Meeting (PESGM), Portland, OR, Aug. 2018. doi: 10.1109/PESGM.2018.858
6650.
7

<u>1. Introduction 1.5. Publications</u>
##### Publications, co-author

7. K. Zhang, **S. Troitzsch**, S.-Y. Zhang, E. S. P. Teh, L. Subramanian, and T. Massier, “Transactive Energy in an Urban Environment: A Case Study of Local Generation and Flexibility Potentials in a Singaporean Urban District,” Front. Energy Res., vol. 9, 2021, doi: 10.3389/fenrg.2021.632992.
8. K. Zhang and **S. Troitzsch**, “Robust Scheduling for Networked Microgrids Under Uncertainty,” Front. Energy Res., vol. 9, p. 632852, May 2021, doi: 10.3389/fenrg.
2021.632852.
9. C. Utama, **S. Troitzsch**, and J. Thakur, “Demand-side flexibility and demand-side bidding for flexible loads in air-conditioned buildings,” Applied Energy, vol. 285, p. 116418, Mar. 2021, doi: 10.1016/j.apenergy.2020.116418.
10. K. Zhang, **S. Troitzsch**, T. Massier, R. Migne, E. S. Pheng Teh, V. K. Advani, M. Cassat,
Y. Xu, and K. J. Tseng, “Towards City-integrated Distributed Generation: Platform for Interconnected Micro-grid Operation (PRIMO),” in IECON 2020 The 46th Annual Conference of the IEEE Industrial Electronics Society, Singapore, Singapore, Oct. 2020, pp. 3791–3796. doi: 10.1109/IECON43393.2020.9255134.
11. K. Zhang, **S. Troitzsch**, S. Hanif, and T. Hamacher, “Coordinated Market Design for Peer-to-Peer Energy Trade and Ancillary Services in Distribution Grids,” IEEE Trans. Smart Grid, 2020, doi: 10.1109/TSG.2020.2966216.
12. K. Zhang, S. Hanif, **S. Troitzsch**, and T. Hamacher, “Day-ahead Energy Trade Schedul- ing for Multiple Microgrids with Network Constraints,” in 2019 IEEE Power & Energy Society General Meeting (PESGM), Atlanta, GA, USA, Aug. 2019, pp. 1–5. doi:
10.1109/PESGM40551.2019.8973609.
13. A. Vautrin, **S. Troitzsch**, S. Ramachandran, and T. Hamacher, “Demand Controlled Ventilation for Electric Demand Side Flexibility,” 2019. doi: 10.26868/25222708.2019
.210968.
14. D. Recalde, A. Trpovski, **S. Troitzsch**, K. Zhang, S. Hanif, and T. Hamacher, “A Review of Operation Methods and Simulation Requirements for Future Smart Distribution Grids,” 2018. doi: 10.1109/ISGT-Asia.2018.8467850.
##### Software releases

15. **S. Troitzsch**, T. Schelo, V. Kleinschmidt, K. Zhang, and A. Ahmed, MESMO-Multi- Energy System Modeling and Optimization, Zenodo, 2021. doi: 10.5281/zenodo.352
3568. Available open-source:[https://purl.org/mesmo/repository](https://purl.org/mesmo/repository)
16. **S. Troitzsch**, T. Miori, and A. Vautrin, CoBMo-Control-oriented Building Model. Zenodo, 2021. doi: 10.5281/zenodo.3523539. Available open-source:https: //purl.org/cobmo/repository
8

## Part I

# Background

## 2 Fundamentals of district-scale energy systems

#### Contents

2.1 Electric grids.................................. 10
2.1.1 Overview................................ 10
2.1.2 Transmission systems.......................... 11
2.1.3 Distribution systems.......................... 12
2.1.4 Mathematical modeling......................... 13
2.2 Thermal grids.................................. 16
2.2.1 Overview................................ 16
2.2.2 District heating systems......................... 17
2.2.3 District cooling systems........................ 18
2.2.4 Bidirectional low-temperature networks................ 19
2.2.5 Distribution piping system....................... 19
2.2.6 Mathematical modeling......................... 20
2.3 Distributed energy resources........................... 21
2.3.1 Typology................................. 21
2.3.2 Distributed generators......................... 22
2.3.3 Loads.................................. 23
2.3.4 Storage systems............................ 25
2.3.5 Mixed DERs.............................. 26
**2.1 Electric grids**
**2.1.1 Overview** The electric grid, i.e. the power system, is generally organized into transmission and distribu- tion systems, which are characterized by different spatial scales, current-carrying capacities and voltage levels. The transmission system links large-scale generators with regional load centers or distribution systems. The distribution system takes care of interconnecting regional and district-scale loads, generators and ESSs, i.e. DERs, with the transmission system.
10

<u>2. Fundamentals of district-scale energy systems 2.1. Electric grids</u> Historically, electric power was only injected to the electric grid by large-scale generators and unidirectionally transferred through the transmission system to the distribution system and further to local electric consumers. In recent years, this paradigm is shifting due to the increasing deployment of renewable generation and ESSs within the distribution system. Still, the different nature of transmission and distribution systems has led to different paradigms for their modeling and operation, which are discussed in the following in sections2.1.2and2.1.3. In the following, electric grids are represented as sets of nodes *N*
*el* and branches *B* *el*, where nodes *n ∈N* *el* are interconnection points and branches *b ∈B* *el* are electric lines or transformers. In graph-theoretical terms, nodes correspond to vertices and branches correspond to edges. Nodes serve as interconnections between different branches as well *NelBel* as DERs. The total numbers of nodes and branches are denoted by *N* and *N*.

##### 2.1.2 Transmission systems

Transmission systems are high-voltage three-phase alternating-current (AC) systems, where the higher voltage is preferred to reduce line currents and losses for long-distance transmis- sion. Although the voltage levels vary for different regions, transmission systems typically operate at or above approx. 100 kV, which may be augmented by sub-transmission sys- tems operating between approx. 30 kV and 100 kV. In Singapore, the voltage levels 400 kV, 230 kV and 66 kV are considered part of the transmission system [53, p. 26, Section 6.5.1]. Historically, the grid is operated as AC system, although direct-current (DC) transmission systems are increasingly being utilized for long-distance transmission with high-voltage DC lines.

Modeling assumptions for the transmission system include the following considerations:

- Branches of the transmission system are arranged in looped or meshed structures, i.e. *NelBel* *N ≤ N*, which increases the resilience for failures of individual branches.
- The transmission system has a low resistance-to-reactance-ratio, compared to distri- bution systems. This is associated with relatively low losses and high linearity of the power flow in the transmission system [11, p. 39, Section 3.9].
- The three phases of the transmission systems are generally operated in a balanced manner. Based on this property, the transmission system can be equivalently modeled as a single-phase system.
Transmission systems are operated by transmission system operators (TSOs) or independent system operators (ISOs), where the nomenclature and scope of responsibilities vary for different regions. Historically, regional utility companies were often vertically integrated and operated power generation plants, transmission systems and distribution systems in conjunction with direct retail consumer services. Over time, energy market liberalization initiatives in many regions have required the disintegration of power generation, transmission, distribution and retail services and introduced wholesale energy markets for the coordination between these services.

<u>2. Fundamentals of district-scale energy systems 2.1. Electric grids</u> In Singapore, the power system liberalization process began in 1995, when the electricity undertakings of the governmental Public Utilities Board (PUB) were corporatized with the creation of Singapore Power (SP). Further, in 1998 the Singapore Electricity Pool was created as day-ahead wholesale electricity market, initially under the SP PowerGrid, i.e. the TSO. Through further regulatory adjustments from 2000 to 2004, the Singapore Electricity Pool eventually became the National Electricity Market of Singapore (NEMS), being operated by the Energy Market Company (EMC). At the same time, the Energy Market Authority (EMA) was created in 2001 as regulatory body and power system operator (PSO), which also holds a 51 % share of the EMC. SP PowerAssets as transmission licensee and SP PowerGrid as subcontractor of SP PowerAssets are responsible for the physical operation of the transmission system. In the meantime, all power generation facilities are operated by wholly independent privatized companies since 2008 after the divestment of the government- owned Temasek holdings from these corporations [54, p. 3-1 to 3-2]. To ensure safe operation, the transmission system capacity limits are included through different mechanisms in the wholesale energy market-clearing process. For example, the market-clearing problem can be formulated as a numerical optimization problem for social welfare maximization, subject to the bids of generators / retailers and the capacity constraints of the transmission system. If congestion occurs, i.e. any branch of the transmission system reaches its capacity limit, locational marginal prices (LMPs) can be utilized to translate the operational constraint into price signals for generators and retailers. That is, the congested portion of the transmission system, i.e. downstream of the congested branch, will see an increased price level, thereby incentivizing the dispatch of additional generation capacities or reduction of demand within this part of the grid.
##### 2.1.3 Distribution systems

The distribution system typically operates as AC system at or below approx. 30 kV, i.e. medium voltage (MV), with the final feeders to customers being operated at or below 400 V,

i.e. low-voltage (LV). In Singapore, the voltage levels 22 kV, 6.6 kV, 400 kV and 230 kV are considered part of the distribution system [53, p. 26, Section 6.5.1]. Modeling assumptions for the distribution system include the following considerations:
- Branches of distribution system usually represent a radial network, which corresponds
*NelBel* to a graph-theoretical tree structure, i.e. *N* = *N* +1. This allows for simplifications in the electric power flow formulation, particularly since branch power flows, excluding losses, follow directly from the nodal energy balances. However, parts of the distribution systems may also include meshed structures to increase reliability. For example, the Singaporean distribution system comprises loops at the 6.6 kV and 22 kV levels [53, p. 40, Section 8.3.1-b].

- The distribution system has a high resistance-to-reactance-ratio, which is associated with relatively high losses and higher non-linearity of the power flow than in the trans- mission system [11, p. 39, Section 3.9].
12

<u>2. Fundamentals of district-scale energy systems 2.1. Electric grids</u>
- The distribution system is usually operated as a three-phase system but may also con- tain two-phase or single-phase sections, i.e. multi-phase configurations. Additionally, the heterogeneity of DERs at the district level may cause highly unbalanced phase loading in the distribution grid. To this end, the modeling of individual phases is more important for the distribution system as compared to the transmission system.
Distribution system operators are typically local or regional utility companies, which operate independently from upstream transmission systems and local generation facilities following the liberalization of the power system as described in section2.1.2. In Singapore, this role is also undertaken by the transmission licensee [53, p. 25, Section 6.1.1], which is owed to the relatively small overall size of Singapore’s power system. Unlike the transmission system, the distribution system is not directly considered in the energy market-clearing process. Rather, distribution systems in the past have been designed in a “fit-and-forget” fashion [1], i.e. its capacity is planned to accommodate projected peak load conditions but there is no active monitoring or control of the system. This paradigm is shifting due to the deployment of more diverse DER types and increasing peak demand. To this end, much research has been devoted to the study of DSO-operated energy markets at the distribution system similar to the wholesale market at the transmission system [13], [55]. In line with this, LMPs have been proposed as distribution LMPs (DLMPs) for the distribution system to incentivize DERs for the resolution of localized congestion [11], [56].

##### 2.1.4 Mathematical modeling

##### Scope and requirements

Mathematical modeling techniques for the electric grid differ for AC transmission and distribu- tion systems and depending on the subject of analysis. Generally, power system analysis can be subdivided into steady-state, short-circuit and transient studies. Steady-state analysis consists of the study of the electric power flow under normal operating conditions, whereas short-circuit analysis focuses on fault conditions and transient analysis refers to the study of machine start-up / shut-down events or harmonics to due to power electronics. To this end, the steady-state analysis typically informs operational dispatch decisions, whereas short-circuit and transient studies are usually performed during the planning stage. In the context of this work, the following will focus on the steady-state power flow modeling of AC electric grids.

Steady-state power flow analysis seeks to determine a set of state variables for the electric grid depending on a set of control variables according to table2.1, based on [57, p. 6, Table 1]. Typical state variables are nodal voltages, branch flows and system losses. Control variables can include substation reference voltage, transformer or voltage regulator settings and nodal power injections. The power flow model is then derived based on the electrical properties of lines, transformers, regulators, generators and loads. Since electric state and control variables of three-phase AC systems are typically expressed as complex phasors, the electrical properties are expressed in terms of complex series and shunt admittance quantities [31].

2. Fundamentals of district-scale energy systems 2.1. Electric grids

||Table 2.1: Representative state and control variables of the electric grid.||
|---|---|---|
|Symbol|Variable description|Type|
|u ∈ C n|Voltage at node n|State variable|
|i ∈ C b|Current flow at branch b|State variable|
|ls s ∈ C|Total complex power losses|State variable|
|sr u ∈ C|Regulated voltage at the source node, e.g. transmission substation|Control variable|
|trf n ∈ R b|Turns ratio, which is representative of the tap setting at transformer b|Control variable|
|s ∈ C n|Complex power injection or load at node n|Control variable|

Additionally, the power flow model formulation is governed by the application type, which can be subdivided into 1) power flow simulation and 2) optimal power flow (OPF). Power flow simulation assumes a-priori knowledge of the control variable settings or expresses their values with controller models. In contrast, OPF seeks to determine optimal values for the control variables based on some objective function and subject to operational constraints of the electric grid. The exact power flow equations are non-convex, which is tolerable for power flow simulations, where iterative techniques can be applied to obtain solutions within reasonable computation time. For OPF, the problem is expressed in terms of a numerical optimization problem, where the exact power flow equations yield a quadratically constrained quadratic program (QCQP), which is NP-hard [58, p. 4]. To address this, the OPF problem can be transformed into a convex form through relaxations [58] or approximation [34], where the convex optimization problem can be efficiently solved with existing solvers [15].

##### Power flow

The steady-state power flow equations are essentially derived based on Kirchhoff’s circuit laws, assuming that the electric grid is represented in terms of nodes and branches. First, Kirchhoff’s current law states that at each node of the grid, the sum of currents equates to zero, which corresponds to the conservation of energy. Second, Kirchhoff’s voltage law states that for closed loops of branches, the sum of potential differences, i.e. voltages, equates to zero. Additionally, current and voltages across branches are related through branch models,

i.e. line, transformer and voltage regulator models, e.g. from [31, Chapters 4 to 7]. Nodal injections or loads are described in terms of bus types or node models, which define relations for the voltage *un*and power injection / load *sn*at each node. The main bus types based on [58, p. 6, Remark 1] are 1) slack bus, 2) generator bus and 3) load bus. The slack bus describes a voltage-regulated node, where *un*is given and *sn*is unknown. At the generator bus, i.e. PV-bus, the active power *pn*= *Re*(*sn*) and voltage magnitude *|un|* are given, whereas reactive power *qn*= *Im*(*sn*) and voltage angle are unknown. The load bus, i.e. PQ-bus, refers to a bus with given complex power injection / load *sn*and unknown voltage *un*. The complete power flow model is eventually derived as a set of generally non-convex
14

<u>2. Fundamentals of district-scale energy systems 2.1. Electric grids</u> quadratic equations. According to [58], the power flow equations can be further distinguished into the bus-injection model and branch-flow model, where the bus-injection model directly expresses nodal injection / load *sn*as a function of the nodal voltage *un*[58, p. 6, eq. 1], whereas the branch-flow model instead formulates the nodal power balance as a function of the branch power flow *sb*and current *ib*augmented by expressions for ohm’s law and branch power [58, p. 7, eq. 2]. Since both model forms are equivalent [58], the choice serves merely as convenience for certain relaxations or approximations. For MESMO, the power flow model is in fact formulated as a superposition of bus-injection model and branch-flow model, which is elaborated in sections6.1.2to6.1.4. The power flow problem itself is stated as the problem for obtaining as solution of the state variables of the electric grid based on the control variables and electrical parameters. Although the power flow equations are non-convex and cannot be explicitly solved, there exist various implicit, i.e. iterative, solution techniques such as Newton-Raphson method, forward- backward sweep and Gauss-Seidel method, which in turn have served as the basis for various software implementations such as OpenDSS [20], MATPOWER [22], PSS-SINCAL [59]. More recently, the implicit Z-bus method [60], [61] and the fixed-point method [33], [62]–[64] have been proposed for the power flow solution. The advantage of these techniques is the ability to formulate conditions for the uniqueness and existence of solutions. In MESMO, the power flow solution is based on the fixed-point method as elaborated in section6.2.
##### Optimal power flow

Optimal power flow (OPF) is an extension to the power flow problem, where the power flow equations are considered as constraints and are augmented with some objective function, for example the maximization of the social welfare in the wholesale market-clearing problem. To this end, the control variables from table2.1become decision variables in the OPF problem, i.e. their values are obtained as the solution of the numerical optimization. The key challenge in formulating the OPF problem lies in the non-convexity of the power flow equations yielding a QCQP, which is NP-hard [58, p. 4]. However, for operational applications,

e.g. wholesale market-clearing or micro-grid operation, obtaining a global solution within reasonable computational effort is key. To this end, various relaxations and approximations for the power flow constraints have been proposed, which allow turning the OPF problem into a convex optimization problem that can be efficiently solved with existing solvers [15]. Relaxations describe the loosening of the power flow constraints in the OPF problem, thereby yielding a convex solution set. To this end, relaxations describe a superset of the original solution set and provide a lower bound for the non-convex OPF problem [58], [65]. Based on [58], relaxation techniques can be distinguished into semi-definite relaxations, chordal relaxations and second-order-conic relaxations. Note that semi-definite programming (SDP) and second-order-conic programming (SOCP) are problem classes of convex optimization, where SDP is a generalization that includes SOCP, i.e. an SOCP problem is also an SDP problem [15]. Chordal relaxation describes SDP relaxations that exploit chordal graph properties for the reformulation of the power flow equations. In terms of solution tightness,
i.e. degree of equivalence between the relaxed solution set and the original solution set,
15

<u>2. Fundamentals of district-scale energy systems 2.2. Thermal grids</u> the SDP describes the most tight and the SOCP describes the least tight relaxation. The theoretical disadvantage of these relaxations is the risk of obtaining an optimal solution from the relaxed problem which does not lie within the original solution set. To this end, conditions of exactness have been formulated in [65], [66], which guarantee that the relaxed solution is equivalent to the solution of the original problem. Approximations introduce additional constraints or assumptions to the OPF problem such that the solution set becomes convex. To this end, approximations describe a subset of the original solution set and serve as an upper bound to the original problem [58]. A historically popular approximation technique is the DC OPF formulation, where the three-phase AC power flow is approximated as single-phase DC power flow [67], [68]. In its classical form [67], this approximation assumes that the system loss, the voltage angle differences as well as voltage magnitude differences are relatively small. Although these approximations are sufficiently accurate for transmission systems [69], distribution system models typically do not fulfill these assumptions as highlighted in section2.1.3. Therefore, [11], [33], [34], [70], [71] have proposed linear approximations for the three-phase AC power flow equations by finding on local tangent panes or global secant panes for the power manifold, thereby yielding linear equation systems. These approximations can further be distinguished into implicit and explicit formulations [55, p. 18, Section 2.2.2], where explicit formulations directly express equations for the state variables in terms of the control variables in the form *x* = *f* (*c*), e.g. in [33], [34], [55], whereas implicit formulations omit the classification of state / control variables in favor of the form *f* (*x,c*) = 0, e.g. in [70]. A clear disadvantage of local / global linear approximations is that their accuracy relies on the choice of the linearization point. To this end, [34] has proposed a trust-region algorithm to continuously update the approximation along with the solution of the OPF problem. In the context of MESMO, the local / global linear approximation of the electric grid model is described in section6.3.
#### 2.2 Thermal grids

##### 2.2.1 Overview

Thermal grids, i.e. DHSs or DCSs, are district-scale systems for the delivery of thermal power,

i.e. heat or cold, to thermal consumers. Thermal grids interconnect district heating plants (DHPs) or district cooling plants (DCPs) with thermal DERs, i.e. loads, generators and ESSs. Therefore, DHS and DCS correspond in scale to the electric distribution system, although there exists no equivalent to the electric transmission system, since thermal grids are usually not inter-regionally interconnected and are served by local DHPs and DCPs. Based on [37], [38], the main subsystems of the thermal grid are the central DHP or DCP, the distribution piping system and the energy transfer stations (ETSs). DHPs and DCPs take a similar role as substations in the electric distribution system, whereas the ETSs serve as coupling points between the grid and thermal DERs. Traditionally, DHSs and DCSs are separate systems, i.e. a thermal grid would serve either heat or cold, and the distribution of thermal power is unidirectional from central plants to thermal consumers. However, recent research envisions a transition towards bidirectional
16

<u>2. Fundamentals of district-scale energy systems 2.2. Thermal grids</u> power flows driven by the deployment of distributed heat pumps (HPs), chillers and combined heat and power (CHP) plants that can turn thermal loads into prosumers [4], [72]–[74]. This paradigm shift is augmented by research into combined district heating and cooling systems, particularly in the form of BLTNs [4], [5], [75]–[77]. As a further dimension in the paradigm shift, buildings equipped with heating, ventilation and air-conditioning (HVAC) systems have already been proposed as FLs for the electric grid [46], [52], [78] and can be operated in a similar fashion to introduce demand side flexibility in the thermal grid. The different characteristics and modeling considerations for DHSs, DCSs and BLTNs are individually addressed in sections2.2.2to2.2.4.
*th th* In the following, thermal grids are represented as sets of nodes *N* and branches *B*, which *th* is equivalent to the notation introduced for electric grids in section2.1. Nodes *n ∈N* are *th* interconnection points and branches *b ∈B* are pipes or other fluid delivery elements. In graph-theoretical terms, nodes correspond to vertices and branches correspond to edges. Nodes serve as interconnections between different branches as well as DERs. Furthermore, *NthBth* the total numbers of nodes and branches are denoted by *N* and *N*.

##### 2.2.2 District heating systems

In DHSs, thermal power is delivered in the form of steam or hot water, where water is the preferred thermal transport fluid due to its relatively low cost. The operating temperature and pressure vary depending on use case and generation of the DHS. Based on [37, p. 3.4], use cases for steam include hospitals and industrial consumers, whereas hot water is preferred for commercial or residential heat supply. The generation of DHSs is classified into 1st generation through 4th generation DHSs, where operating temperature and pressure are continually reduced from 1st to 4th generation. 1st generation systems utilized pressurized steam at supply temperatures of up to 200 °C, whereas 2nd generation systems utilized pressurized hot water at supply temperatures above 100 °C. 3rd generation systems reduced hot water supply temperatures to below 100 °C, thereby also reducing the minimum operating pressure to atmospheric levels. The 4th generation further reduces supply temperatures to below 70 °C, specifically to allow decentralized injections from heat pumps, thereby transforming the DHSs to a bidirectional system. Note that 5th generation DHSs as proposed in [76] are addressed as BLTNs in section2.2.4. The following will only consider DHSs with hot water as thermal transport fluid, i.e. systems of 2nd generation or newer.

DHPs can be classified based on their fuel source and technology according to [37], [79] into the following types:

- Heat-only fuel-fired systems, such as conventional boilers powered by fossil fuels, biomass or refuse-derived fuels.
- CHP plants, which may be based on a steam turbine, combustion turbine or combustion engine and driven by fossil fuels, biomass or refuse-derived fuels.
17

<u>2. Fundamentals of district-scale energy systems 2.2. Thermal grids</u>
- Electric-driven heat pumps are heat-only systems, where the heat is produced with a vapor-compression cycle based an external heat reservoir, such as sewage, seawater, solar-thermal resources, geothermal resources or industrial waste heat.
- Geothermal direct-use heat-only plants, which utilize geothermal hot water or steam directly without an additional vapor-compression cycle.
While the historically most common DHPs are heat-only fuel-fired systems and fossil-fuel- driven CHP plants, future DHSs are envisioned to rely on electric-driven systems in the context of smart energy systems [80]. To this end, DHPs are becoming an interconnection point between the electric and the thermal grid, which will be explored further in the context of MESs in chapter3.

The distribution piping system of DHS usually consists supply side and return side. Assuming a traditional setup with thermal power only being injected centrally at the DHP, hot water at supply conditions is distributed through the supply side to thermal consumers. At each consumer, the water passes from the supply side through the ETS to the return side, where the water temperature falls to return conditions as thermal power is extracted. The return water temperatures in DHSs depend on the generation of the plant, e.g. up to 80 °C for 1st generation plants and down to 25 °C for 4th generation plants. Note that in 4th genera- tion DHSs, where bidirectionality is introduced in the form of decentralized thermal power injections, e.g. from heat pumps, the supply and return side are instead referred to as warm and cold side. Further characteristics of the distribution piping system are discussed in section2.2.5.

##### 2.2.3 District cooling systems

In DCSs, chilled water serves as thermal transport fluid, where water is preferred due to its relatively low cost, similar to DHSs. Chilled water at approx. 4 °C is used for commercial or residential space cooling supply [38, p. 3.3]. Temperatures below 4 °C are usually avoided due to the risk of freezing. In principle, glycol can be added to allow for lower temperatures but is typically avoided due to the additional cost.

DCPs are distinguished based on [38] according to their technology and energy source into:

- Electric-driven compression chillers, where heat is removed from the thermal transport fluid through a vapor-compression cycle.
- Mechanically-driven compression chillers, where the mechanical input is provided by a fuel-driven steam turbine, combustion turbine or combustion engine.
- Absorption refrigeration machines, where chilled water is produced through a chemical absorption cycle based on an external heat reservoir, such as geothermal resources or industrial waste heat.
DCPs, unlike DHPs, are already commonly operated as electric-driven systems. However, the operational flexibility of such systems, especially when equipped with TESS, is usually not

<u>2. Fundamentals of district-scale energy systems 2.2. Thermal grids</u> utilized to participate as a flexibility resource in the electric grid. This is, however, envisioned in the context of smart energy systems [80] and will become increasingly important due to the expected global increase in cooling demand [81]. The distribution piping system of DCSs typically comprises supply side and return side similar to DHSs. The supply side distributes chilled water at supply conditions to the thermal consumers, assuming that chilled water is only produced centrally at the DCS. Within the ETS at each consumer, water is passed from the supply to the return side, while the water temperature increases to return conditions, i.e. typically approx. 13 °C. Further considerations for the distribution piping system are presented in section2.2.5.
##### 2.2.4 Bidirectional low-temperature networks

BLTNs, proposed as 5th generation DHSs in [76] or 5th generation district heating and cooling in [5], describe thermal grids which combine capabilities of DHSs and DCSs. To this end, these systems divide the distribution piping system into warm side and cold side, where [76] assumes that water temperatures on both side are close to ambient temperatures between 5 °C to 30 °C and the temperature difference between warm and cold side would lie between 5 K to 10 K. Unlike traditional DHSs or DCSs, the supplied water would not directly serve thermal demand but would instead serve as heat or cold reservoir for heat pumps or chillers at the ETSs. To this end, heat pumps would serve thermal heating demand by utilizing water from the warm side as heat reservoir for their evaporator and discharging the cooled water to the cold side. Inversely, chillers would operate with water from the cold side as cold reservoir for the condenser and eject heated water to the warm side. In principle, all DHP and DCP plant types introduced in sections2.2.2and2.2.3can also serve as thermal producers in BLTNs but the system does not follow the paradigm of centralized production as traditional DHSs and DCSs.

##### 2.2.5 Distribution piping system

The distribution piping system of thermal grids consists of insulated pipes and fittings as branches and ETSs as nodes. For traditional DHSs and DCSs, as outlined in sections2.2.2 and2.2.3, the piping system comprises supply side and return side. Usually, the layout of supply and return side is congruent, i.e. the arrangement of the return side piping mirrors the supply side setup. At ETSs of thermal DERs, the water is either passing through a heat exchanger or directly through the consumer systems, where the former variant with separate fluid cycles is typically preferred for maintenance reasons. The layout of piping systems can be distinguished similarly to electric grids into radial, looped and meshed system according to [79, p. 37, Figure 4.1]. Radial grid layouts correspond to a graph-theoretical tree structure, *NthBth*

i.e. *N* = *N* + 1 and are preferred for medium-sized grids to reduce the overall pipe
*NthBth* length and associated costs [40, p. 40]. Looped and meshed layouts, i.e. *N ≤ N*, are pursued where the increased reliability justifies the additional cost or where system expansion necessitates the integration of multiple plants. At the same time, proposals for

2. Fundamentals of district-scale energy systems 2.2. Thermal grids 4th-generation and 5th-generation DHSs often assume meshed layouts for the increased operational flexibility [82]. A key concern at the return side is to ensure a high temperature difference across the ETSs, such that a high plant efficiency can be maintained at the DHP or DCP [37], [38]. This is often enforced through penalties for consumers which do not achieve a contractually mandated temperature difference. At DCSs operated by SP Group in Singapore, a penalty term is included in the billing arrangements to incentivize thermal consumers to ensure return temperature at or above 14 °C as per supply conditions [83, Section 6.5].
##### 2.2.6 Mathematical modeling

##### Scope and requirements

Mathematical models of thermal grids describe the hydraulic and thermodynamic properties of the supply and return water flow. Such models are utilized for both planning-stage and operational decision support and are akin to steady-state power flow models for the electric grid as in section2.1.4, although no equivalent exists for short-circuit and transient analysis. In the context of this work, the following will focus primarily on the modeling of DHSs and DCSs with congruent supply and return sides.

Table 2.2: Representative state and control variables of the thermal grid.

|Variable description|Type|
|---|---|
|Pressure head at node n|State variable|
|Supply and return side temperature at node n|State variable|
|Volume flow rate at branch b|State variable|
|Total pump power demand|State variable|
|Regulated pressure head at the source node, i.e. DHP or DCP|Control variable|
|Regulated supply temperature at the source node, i.e. DHP or DCP|Control variable|
|Thermal power injection or load at node n|Control variable|

##### Symbol

*hn∈* R *sup* *Tn,Tnret∈* R *qb∈* R *pm* *p ∈* R *sr* *h ∈* R

*sup,sr* *T ∈* R *th* *pn∈* R

The hydraulic and thermodynamic fluid modeling characterizes the relationship between the state variables and control variables of the thermal grid according to table2.2. Typical state variables are nodal pressure heads, nodal supply / return temperatures, branch volume flow rates and pump power demand. Control variables can be the regulated pressure head at the source node, the regulated supply temperature at the source node and the nodal thermal power injection or load. Model parameters are the hydraulic and thermodynamic properties of the distribution piping system, pump parameters and ambient temperature conditions. Two common assumptions for hydraulic and thermodynamic flow modeling are 1) incompressibility of water and 2) constant specific heat capacity of water, which are accordingly assumed in the following.

<u>2. Fundamentals of district-scale energy systems 2.3. Distributed energy resources</u>
##### Hydraulic and thermodynamic flow modeling

The hydraulic flow modeling in thermal grids is governed by 1) the law of mass conservation and 2) the law of energy conservation and 3) the hydraulic resistance of branches [39, p. 61, Section 2.5.3]. The law of mass conservation is akin to Kirchhoff’s current law and states that the sum of volume flows at each node equates to zero. Similarly, the law of energy conservation, i.e. the extended Bernoulli equation, is equivalent to Kirchhoff’s voltage law and states that for closed loops of branches, the sum of potential differences, i.e. hydraulic pressure heads, equates to zero. Additionally, the hydraulic resistance of pipes and fittings is described with models for friction losses and minor losses. Friction losses occur due to shear stresses between the viscous fluid flow and the pipe wall, whereas minor losses occur at flow deviations [39]. The equation system resulting from the law of mass conservation and the law of energy conservation is often represented in graph-theoretical notation, e.g. [84, eqs. 5-10] and [72, Section 3.1].

The thermodynamic flow modeling describes the change of the fluid temperature due to 1) thermal losses and 2) thermal power injections and loads. Thermal losses are fundamentally captured by the differential equation for the fluid temperature along each pipe, depending on the specific thermal resistance and the ambient temperature. This equation can be reformulated to into an expression of the fluid volume flow rate according to [72, p. 5]. The change of the fluid temperature due to thermal power injections and loads is often neglected in DCS models [40] but can be considered with models of the heat exchanger dynamics at ETSs, e.g. based on [72, p. 6].

#### 2.3 Distributed energy resources

##### 2.3.1 Typology

DERs represent all energy systems connected to the district-scale electric or thermal grid,

i.e. loads, generators and ESSs. This is based on the definition of “DER” according to IEC 61850-7-420 [2, Section 3.2.9]: [...] generation, storage, and controllable load connected at the low or medium voltage distribution level. DER may include associated protection, control, and monitoring capabilities, and may consist of aggregated DER units. DER may interact with the area and/or local electric power systems (EPS) by providing energy through the EPSs, by adapting their behavior based on EPS conditions, and/or by providing other EPS-related services for regulatory, contractual, or market reasons. Although this definition aligns with ISO 15118-1 [85, Section 3.1.20], it is contradicted by IEEE Std 1547-2018 [86, Section 3.1], IEC 60050 [87, Section 617-04-20] and [88, Section
1.3.2], which only consider generators or energy storage as DERs and specifically exclude controllable loads without generation capabilities. Nevertheless, the broader definition from
21

<u>2. Fundamentals of district-scale energy systems 2.3. Distributed energy resources</u> IEC 61850-7-420 [2] is adapted in the following because it avoids ambiguous distinctions between generators and loads in MESs, e.g. for district heating and cooling plants, which act as generators in the thermal grid and loads in the electric grid. DERs are generally distinguished into 1) generators, 2) storage systems and 3) loads, e.g. based on IEC 61850-7-420 [2, Figure 11], where combinations are possible in the form of mixed DERs. Further, DERs can be either fixed, i.e. uncontrollable, or flexible, i.e. controllable in terms of their power dispatch schedule. Therefore, DERs are classified according to the following typology in the remainder of this work:
- **Distributed generators**, which describe all energy systems that inject power into the electric or thermal grid and are further distinguished into: **–** Uncontrollable or **fixed generators**, e.g. renewable energy sources, which de- pend on external disturbances and in principle are cannot be actively dispatched. **–** Controllable or **flexible generators**, which represent generators with variable power output, e.g. CHP plants.
- **Loads**, which characterize the energy demand in the electric grid and thermal grid. Loads can be subdivided into: **–** Uncontrollable or **fixed loads**, i.e. traditional loads that do not receive any control or price signal from the district-scale energy system operator. **–** Controllable or **flexible loads**, which exhibit demand side flexibility (DSF) and can reshape their demand, e.g. HVAC systems. **– EV chargers**, which represent a new type of load expected to make up a signifi- cant share of the electric energy demand in the near future. Depending on the charging control system, this type of load can be characterized as fixed or flexible.
- **Storage systems**, i.e. ESSs, are electric energy storage systems or thermal energy storage systems (TESSs) with the ability act both as load and as generator.
- **Mixed DERs**, e.g. in the form of prosumers or virtual power plants (VPPs), represent an aggregation of other DERs as a superposition of generators, loads and ESSs, thus able closely control their interaction with the electric or thermal grid.
Other DER typologies can be found in [89, Figure 2], which presents a comprehensive classification of distributed generators based on process type and fuel type, or [90], which provides a classification of control mechanisms of flexible loads.

##### 2.3.2 Distributed generators

##### Fixed generators

Fixed generators describe resources that inject electric or thermal power in an uncontrollable fashion, i.e. there is no means for the energy system operator to influence their dispatch schedule. This typically refers to renewable energy sources, which are increasingly being

<u>2. Fundamentals of district-scale energy systems 2.3. Distributed energy resources</u> deployed at district-scale energy systems in the form of solar-photovoltaic (PV) systems, solar-thermal systems, small-scale wind-energy conversion systems and small-scale hydro- turbines [89]. At district-scale energy systems, solar-PV and solar-thermal systems are typically more common than wind-energy and hydro-turbine systems. Solar-PV systems directly convert solar energy to electric power by utilizing the photovoltaic effect in semiconducting materials. In Singapore, PV systems are accounted for approx.
0.3 GWp in 2019 [91, p. 14, Figure 4.1], i.e. only approx. 4 % of the 7.4 GWp total system demand [92] but baseline projections assume a realistic deployment of 1 GWp by 2030 and
2.5 GWp by 2050 [91, p. 7, Section 1]. A majority of these systems would be deployed in electric distribution grids, as approx. 60 % of the usable area for deployment consists of rooftops and facades [91, p. 28, Table 5.3].
##### Flexible generators

Flexible generators are controllable electric or thermal producers, i.e. their dispatch can be influenced through control inputs. This class of DERs comprises traditional generators, CHP plants, fuel cells, geothermal systems and other heat pumps [89]. Note that DHPs and DCPs according to sections2.2.2and2.2.3also fall into the category of flexible generators.

Traditional generators and CHPs can be based on combustion engines or small-scale com- bustion turbines, whereas traditional generators only produce electricity and CHPs produce thermal power and electric power simultaneously. Both CHPs and traditional generators can be driven either by fossil fuel or synthetic fuels based on biomass, waste and refuse. Particularly biomass-based and refuse-based CHPs have driven the deployment of con- trollable DERs, as these small-scale systems are typically connected at MV-level in the electric distribution system. All aforementioned DERs can in principal be actively dispatched, although uncertain operational constraints, e.g. varying synthetic fuel production from a biomass reactor, can limit the dispatch quantity. Other systems, e.g. chiller plants at DCPs, cannot be dispatched below a certain part load ratio.

##### 2.3.3 Loads

##### Fixed loads

Fixed loads are traditional uncontrollable electric and thermal loads, which can be broadly distinguished into household, commercial, industrial and transport-related energy demand based on the Singapore Energy Statistics [92]. Household-level electric and thermal energy demand is defined by space heating and cooling, hot water supply, appliances and lighting. The commercial sector includes wholesale, retail, hospitality, financial, information technology, science and other office-based activities, such that its energy demand is similarly dominated by space heating and cooling, appliances and lighting. These two sectors typically account the majority of DERs at district-scale electric and thermal grids. In Singapore, households account for approx. 15 % and commercial-related demand for approx. 37 % of the total electric energy demand of approx. 51 GW h in 2019 [92]. The industry sector, i.e. manufacturing and related activities, accounts for 41 % of Singapore’s electric energy demand, although this

<u>2. Fundamentals of district-scale energy systems 2.3. Distributed energy resources</u> includes large-scale consumers that may be connected at the electric transmission system. Similarly, the transport sector which accounts for 6 % of Singapore’s electric energy demand is typically served by separate electric infrastructure.
##### Flexible loads

Flexible loads describe electric or thermal consumers whose demand schedule can be controlled or influenced by the energy system operator. This is usually associated with DSF and is enabled by the internet of things, i.e. advanced communication infrastructure and embedded systems [90]. To this end, flexible loads are in fact traditional consumers with advanced control systems and communication interfaces towards energy system operators. Candidates for DSF are consumers with inherent energy storage, i.e. the ability to absorb energy for use during a curtailment period, or with the ability to defer demand, i.e. there is temporal laxity for completion of the end-use service [93]. Flexible loads with inherent energy storage are HVAC systems for space heating / cooling in buildings, hot water supply systems and other thermostatically controlled loads. Flexible loads with ability to defer demand include EV chargers, industrial manufacturing processes and appliances such as washing machines or pool pumps. Additionally, flexible loads may include consumers that accept pure curtailment, i.e. energy consumption is avoided entirely rather than deferred or stored, for example through the dimming of lighting systems.

From an economic perspective, DSF relies on the willingness of consumers to tolerate a degradation in service in return for monetary incentives for participation. In this context, [94, Section III.A] notes the duality of objectives in achieving DSF, i.e. the maximization of response versus the minimization of end-use service degradation. Further, [94] highlights the importance of non-disruptiveness in DSF to avoid response fatigue, i.e. the withdrawal of participants in the event of extended curtailment periods [95, p. 10].

##### EV chargers

The electric demand associated with EV charging can be characterized as either fixed load or as flexible load depending on the underlying control mechanism. In light of the push towards electrified transport systems [96], EV charging can be seen as both a challenge,

i.e. due to its large peak demand, and an opportunity, i.e. due to its DSF potential, and therefore is discussed separately here. Controllability of EV charging can be achieved through Vehicle-to-grid (V2G) capabilities, which are generally categorized into smart charging, i.e. unidirectional V2G, and V2G charging, i.e. fully bidirectional V2G. To this end, smart charging refers to the ability to control the charging power demand schedule, whereas V2G charging describes the ability to control the bidirectional exchange of electric power between the vehicle and the electric grid, i.e. both charging and discharging. V2G-enabled EV charging can be characterized as a superposition of flexible load, i.e. the smart charging component, and energy storage system, i.e. the V2G charging component.
24

<u>2. Fundamentals of district-scale energy systems 2.3. Distributed energy resources</u>
##### 2.3.4 Storage systems

##### Electric energy storage

Electric energy storage enables the conversion of electric energy to another form of potential energy, such that electric power is consumed, retained and injected in a fully controllable manner. Storage technologies can be distinguished into battery energy storage systems (BESSs), mechanical storage systems and capacitor-based storage systems [89, Section

2.2]. BESSs, which represent the most common storage technology, can be further classified based on the underlying electrochemical process, where Lithium-Ion and Lead-Acid represent the most common technologies for stationary storage applications [47, p. 36ff, Section 2.5.2]. Mechanical storage technologies include pumped hydro storage, flywheel systems and compressed air energy storage systems [89]. Since mechanical and capacitor-based storage are presently uncommon at district-scale energy systems, the following focuses only on BESSs. Among BESSs, Lithium-Ion systems are preferred for their high energy density, whereas Lead-Acid systems represent a low-cost alternative. Most BESS are limited to charging / discharging rates between 0.5 C to 1 C, although Lithium-Ion systems theoretically support charging rates of up to 10 C and discharging rates of up to 50 C [97, Section II.C], where C defines to the charging / discharging rate relative to the storage capacity as C = W/(W h). The response time of BESSs is in the order of seconds, where [98] experimentally identified response times between 2.5 s to 5 s across different battery technologies. To this end, BESSs have been demonstrated for fast-response applications such as frequency control [99] but also for slow-response applications such as energy arbitrage [100].
##### Thermal energy storage

TESSs can consume, retain and inject thermal power in a fully controllable manner. De- pending on the primary application, thermal storage refers either to heat storage in DHSs or cold storage in DCSs. Independent of the application, thermal storage technologies are generally distinguished into sensible heat storage, latent heat storage and thermochemical storage [101]. Sensible heat storage describes the storage of thermal power through a change of temperature in the storage medium, i.e. the stored thermal energy is proportional to the change in temperature. Latent heat storage utilizes the phase change energy of the storage medium, i.e. thermal power is charged or discharged at relatively constant temper- ature while the medium transforms from one phase to another. Thermochemical storage is based on the energy absorbed / released through a reversible chemical reaction, similar to BESSs. While thermochemical storage is characterized by high energy density, sensible storage is often preferred for relatively low system costs, whereas latent storage provides a trade-off between the two [101]. Note that in DHSs and DCSs, sensible and latent storage systems with water as storage medium are most common, which is due to relatively low cost and convenience, since water is typically also utilized as thermal transport fluid.

<u>2. Fundamentals of district-scale energy systems 2.3. Distributed energy resources</u>
##### 2.3.5 Mixed DERs

The concept of prosumers, i.e. producers and consumers, describes the encapsulation of different DERs at end-user-level [102]. For example, a household may operate a PV system, BESS and EV charger in addition to traditional household appliances, such that it can consume / inject electric power from / to the electric grid in a fully controllable fashion. To this end, prosumers fall into the class of mixed DERs according to IEC 61850-7-420 [2], which are able to achieve higher operational flexibility compared to stand-alone flexible generators, flexible loads or ESSs. In the commercial sector, the concept of prosumers somewhat coincides with load aggregators, e.g. proposed in [103], [104], that interact with the energy market on behalf of multiple flexible loads, thereby aggregating larger offering quantities as may be required, e.g. minimum curtailment offer of 0.1 MW in the Demand Response Programme of the NEMS [105]. In a similar fashion, [106] envisions prosumers as agents for brokering the energy market participation on behalf of end-users.

VPPs describe the aggregation of various flexible DERs for the purpose of offering services at the energy market [107, Section 3.1.4]. The concept slightly differs from prosumers in the sense that DERs are not expected to be co-located. Therefore, VPPs are aimed at transmission-system-level markets rather than district-scale markets [108]. Operation strategies for VPPs have been proposed for both fast-response applications such as ancillary service provision as well as slow-response applications such as day-ahead energy trade [109,

Table 3], where several real-world demonstrations are summarized in [109, Table 4].

## 3 Multi-energy system modeling and optimization

#### Contents

3.1 Definition and concepts.............................. 27
3.2 Scope and problem types........................... 28
3.3 Modeling dimensions.............................. 29
3.4 Existing software frameworks......................... 30
**3.1 Definition and concepts** MESs, also defined as smart energy systems in [80], [110], refer to integrated energy systems with a coordinated approach to planning and operation across different energy commodities [107], [111], [112].In the context of this work, MESs specifically describe combined district-scale electric and thermal grids which are coupled through DERs with the ability to convert between electric and thermal power. Broader definitions of MESs in [80], [107], [110]–[112] non-exhaustively consider electric energy systems, thermal energy system, gas networks, other chemical energy carriers and transport systems.Transport systems are included in light of the anticipated transport electrification and the potential operational flexibility from these systems. Note that MESs are essentially a structural concept, where the underlying technologies and modeling techniques for each subsystem are those that have been introduced in sections2.1to2.3. Based on [107, Section 3.1], MESs as a structural concept for the combination of multiple energy systems is related to energy hubs, microgrids as well as VPPs which were introduced in section2.3.5. Traditionally, energy system modeling, planning and operation were restricted to selected energy systems, particularly on the district-scale [107]. A key driver towards MES approaches is the global public policy push towards the reduction of greenhouse gas emissions, which relies on increasing efficiencies across all energy sectors.To this end, highly optimized solutions are needed for both planning and operation time-scales, which may be achieved through synergies across the different energy systems. The integration of MES planning and operation is enabled by both computational and technological factors. From a computational viewpoint, the increasing availability of high-performance computing resources facilitates
27

<u>3. Multi-energy system modeling and optimization 3.2. Scope and problem types</u> the coupling of detailed energy system models. Therefore, handling the complexity of mathematical models for multi-energy is becoming feasible. With regards to the technical dimension, the deployment of heat pumps has enabled the coupling of electric and thermal energy systems, whereas the deployment of EV charging interlinks electric energy and transport systems. In a similar fashion, fuel cells and power-to-gas systems may facilitate the coupling of electric, gas and chemical energy systems, whereas [113] even proposes the integration of carbon dioxide as an energy carrier in MESs based on solid-oxide fuel cells.
#### 3.2 Scope and problem types

Mathematical models of MESs can be obtained by aggregating or coupling the models of its subsystems, i.e. electric grids, thermal grids and DERs. To this end, complexity management is an important aspect of MES modeling in managing model formulation effort, model parameter data requirements and computational limitations. Consider the following statement from [114], which serves as a definition of the term “model”:

To an observer B an object M is a model of an object A to the extent that B can use M to answer questions that interest [them] about A.

To restate, a model needs to be just detailed enough for the purpose of the problem that is being studied. Applied to MES, complexity management ensures that models cover only a selected scope across different modeling dimensions, depending on a specific problem type.

The analysis of MESs can be classified into different problem types, which serve to distinguish the expected results as well as requirements for the mathematical models. Note that the characterization of problem types is interrelated with the modeling dimensions introduced in the next section. Based on [115, Section 2.2.1] and [116, Section 3.1], MES problems can be broadly distinguished into:

- **Operation problems**, which describe the analysis of the system at operation-timescale with the purpose of providing operation decision support [115]. Examples for this category are unit commitment problems, optimal control / model predictive control problems and market-clearing problems. In the context of this work, operation problems are further distinguished into: **– Nominal operation problems**, where the solution is obtained via non-linear simulation of the MES models. The purpose of this problem type is to describe the nominal behavior of the system, for example to serve as a baseline for an optimal operation problem. **– Optimal operation problems**, which are solve via numerical optimization in order to obtain an optimal solution for the control variables of the MES. Since approximate models may be required to pose the model in terms of an optimization problem, the optimal operation problem may rely on the nominal operation problem as a reference.
28

<u>3. Multi-energy system modeling and optimization 3.3. Modeling dimensions</u>
- **Planning problems**, which characterize design decisions for the MES, i.e. at planning- timescale, with the goal of providing investment decision support [115]. These studies can be addressed in terms the following sub-problems: **– Simulation-based scenario analysis**, with an aim of forecasting the system be- havior with regards to scenarios for the input parameters [116]. This captures the traditional approach in energy system planning, where are small set of scenarios,
i.e. design proposals, is first developed based on empirical engineering guidelines and then evaluated via simulation.
**– Optimal planning problems**, where an optimal solution is obtained for the design decision variables, e.g. component sizing and placement. This problem type is solved via numerical optimization and in literature sometimes simply referred to as “model” [24].

#### 3.3 Modeling dimensions

The modeling dimensions with regards to MES models can be distinguished according to the following typology, based on a synthesis of [112], [115]–[119]:

- **Temporal scale and resolution**, where the scale defines the time horizon which is covered by the model and the resolution describes the time interval of the temporal model discretization. Both dimensions can range from microseconds, e.g. for transient electric grid simulation, to decades, e.g. for MES planning optimization [116, Table 1].
- **Spatial scale and resolution**, where the scale describes the geographical extent which is included in the model and the resolution defines the smallest spatial discretization unit of the model. The spatial scale can range from district scale to continental scale, whereas the resolution ranges from plant level to country level. Refer to [112, Figure 5] for an overview of the relation between spatiotemporal scales and technological problem types.
- **Domain coverage** describes the extent to which the model considers overlapping technological, economic and social science aspects. The technological aspects refer to the modeling of the physical behavior of the energy system, i.e. based on the engineering perspective that was taken in sections2.1to2.3. Economic aspects are those relating to the interaction of energy systems in a market environment, e.g. the modeling of the market-clearing algorithm. Social science aspects cover the modeling of consumer acceptance and user behavior.
- **Sector coverage** indicates the scope of the model with regards to the different energy system commodities and technologies. Based on the definition of MESs from sec- tion3.1, the different sectors can be distinguished into electric energy systems, thermal energy systems, gas networks, other chemical energy carriers and transport systems. An important secondary dimension in this regard is the fidelity or level of approximation for the underlying models, e.g. electric grid power flows can be represented in terms of a simple power balance or in a detailed fashion with regards to the individual states
29

<u>3. Multi-energy system modeling and optimization 3.4. Existing software frameworks</u> in table2.1. Refer to [112, Figure 4] for an illustrative mapping between technological aspects and model types.
- The **analytical approach** describes whether the model formulation is obtained bottom- up, top-down or through a hybrid approach. In bottom-up models, each subsystem is modeled individually, e.g. based on first-order principles, and the complete model is obtained as an aggregation of the subsystem models. Conversely, top-down models immediately take the system-level perspective and incrementally develop subsystem models, e.g. in a data-driven fashion, thereby usually applying a low level of detail for each subsystem. Hybrid models utilize both techniques, e.g. by applying a dif- ferent approaches for each subsystem. Refer to [120, Section 2] for a more detailed classification of analytical approaches.
- The **solution method** denotes whether a model is solved via simulation, optimization or hybrid approaches. This aspect highlights the ability to cast the model into a particular solution logic. The reason lies in mathematical requirements posed particularly by numerical optimization techniques, i.e. convex optimization can only handle convex model equations. Hybrid approaches exist due to the availability of generalized heuristic optimization solvers, although convex optimization is preferred in some applications for global optimality guarantees.
#### 3.4 Existing software frameworks

Capabilities of existing software tools in the domain of district-scale MES modeling are compared in table3.1. Note that this serves as a preparation for the software development of MESMO in chapter5. To this end, representative tools are shortlisted based on the reviews [115], [116], [121], with a focus on software which is capable of modeling energy systems at district-scale and within operation-timescale. Specifically, the geographical coverage must be possible at local scale and spatial resolution at building scale according to [116]. For multi-period-enabled tools, the temporal resolution must lie within minutes to hours, which is needed to study operational issues [116, Table 1]. Tools which do not meet these criteria are excluded. Other software frameworks which closely resemble the features of any listing are also excluded for the sake of brevity. A brief description for each shortlisted tool is provided in the following:

- Siemens **PSS-SINCAL** is a commercial energy system analysis software [59]. Its focus is on high-fidelity steady-state as well as transient electric power flow studies but it also enables pipe network simulation, e.g. water distribution systems, district heating / cooling systems or gas networks. It has also been extended with modules for OPF studies. Similar software packages, such as NEPLAN [122], STANET [123] or EPANET [124], are omitted for the sake of brevity.
- DIgSILENT **PowerFactory** is a commercial power system analysis software, which enables steady-state as well as transient power flow studies [21]. Although its core focus is on high-fidelity simulation, the tool has been extended with modules for OPF
30

3. Multi-energy system modeling and optimization 3.4. Existing software frameworks

|||||Table 3.1: Software tools for district-scale energy system simulation and optimization.||||||||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Feature|PSS-SINCAL|PowerFactory|OpenDSS|GridLAB-D|MATPOWER|pandapower|pandapipes|PowerModels.jl|OPEN|urbs|Calliope|Homer|CEA MESMO|
|Categorization||||||||||||||
|a Sector coverage|M|E|E|E|E|e E|e T|E|E|M|M|M|M M|
|b Solution method|M|M|S|S|M|f M|S|O|M|O|O|M|M M|
|c Optimization|N|N|||M|M||M|C|C|C|N|H C|
|d Problem type|O|O|O|O|O|O|O|O|O|P|P|P|P O|
|Electric grid modeling||||||||||||||
|Power flow simulation|✓|✓|✓|✓|✓|✓|e|✓|✓|||✓|✓ ✓|
|Power flow optimization|✓|✓|||✓|f ✓||✓|✓|✓|✓|✓|✓ ✓|
|Balanced AC model|✓|✓|✓|✓|✓|✓||✓|✓|✓|||✓|
|Multi-phase AC model|✓|✓|✓|✓||||g ✓|✓||||✓|
|Transient dynamics model|✓|✓|h ✓|||||||||||
|Convex electric grid model|||||✓|f ✓||✓|✓|✓|✓||✓|
|Thermal grid modeling||||||||||||||
|Thermal power flow sim.|✓|||||e|✓|||||✓|✓ ✓|
|Thermal power flow opt.||||||||||✓|✓|✓|✓ ✓|
|Fluid pressure model|✓||||||✓||||||✓|
|Fluid temperature model|✓||||||✓|||||||
|Convex thermal grid model||||||||||✓|✓||✓|
|DER modeling||||||||||||||
|DER simulation||||✓|||||✓|||✓|✓ ✓|
|DER optimization|||||i ✓||||✓|✓|✓|✓|✓ ✓|
|Convex DER model|||||||||✓|✓|✓||✓|
|Other features||||||||||||||
|Multi-period sim. / opt.|||||||||✓|✓|✓|✓|✓ ✓|
|DLMP decomposition|||||j ✓||||||||✓|
|Energy market modeling||||✓|||||✓||||k ✓|

a Sector coverage: Electric (E), Thermal (T), Multi-energy (M). b Solution method: Simulation (S), Optimization (O), Mixed (M). c Optimization: Convex (C), Non-convex (N), Heuristic (H), Multiple (M). d Problem type: Operation (O), Planning (P). e pandapower and pandapipes can be coupled for MES simulation. f pandapower utilizes PowerModels.jl for OPF problems. g PowerModels.jl can be extended for multi-phase grid modeling through PowerModelsDistribution.jl. h OpenDSS can model electromechanical transients but not electromagnetic time-domain transients. i MATPOWER enables augmenting its OPF problem with user-defined variables, constraints and cost functions. j MATPOWER returns DLMPs but not decomposed into energy, loss and congestion components. k Market clearing problems can be expressed with MESMO, but are not directly implemented as problem type.

<u>3. Multi-energy system modeling and optimization 3.4. Existing software frameworks</u> studies. Related commercial tools, such as ETAP [125], are omitted for the sake of brevity.
- **OpenDSS** is the open-source distribution system simulator [20]. This tool enables clas- sical steady-state as well as transient power flow simulation studies. OpenDSS does not directly cater to optimization-based studies but has been utilized as a subsystem in OPF implementations, e.g. in [126].
- **GridLAB-D** is a software tool that connects distribution system simulation and DER simulation [28]. Its core capability is to coordinate in an agent-based fashion the simulation of various subsystems, where each subsystem model can be implemented independently. Through a modular approach, GridLAB-D supports studies ranging from classical power flow analysis to integrated energy market simulation with detailed models for the behavior of individual DERs.
- **MATPOWER** is open-source software for power system analysis in MATLAB or GNU Octave [22]. It originated as a tool for balanced AC power flow solution but has since been extended for OPF and optimal scheduling applications [127].
- **pandapower** is an open-source project for power system analysis in Python [128]. This tool was originally based on PYPOWER [129], i.e. a port of MATPOWER to Python, but has since been extended with additional power flow solution algorithms and an interface to PowerModels.jl [27] for OPF applications.
- **pandapipes** is a sibling project of pandapower and is focused on pipe network simula- tions, e.g. DHSs or gas networks [130].
- **PowerModels.jl** is an open-source framework for power system optimization in Ju- lia [27]. It enables power flow and OPF calculation based on a variety of network model formulations, where the focus is on comparing the computational performance of different power flow models and solution algorithms. The sibling project PowerMod- elsDistribution.jl [131] provides extensions for distribution grid modeling.
- **OPEN** is the Open Platform for Energy Networks [29]. This Python-based software enables simulation and optimization of power systems and DERs on the district-scale, with a focus on multi-period optimization and energy market modeling.
- **urbs** is an open-source software for energy system optimization [25] with a focus on capacity expansion planning and unit commitment of DERs. The sibling project ficus provides an extension for modeling multi-commodity energy systems in factories [132].
- **Calliope** is an open-source project for energy system optimization [24]. Its focus is on optimal operation and planning problems for MESs in a modular fashion, i.e. technology-agnostic and independent from the geographical scale and timescale. Similar open-source frameworks, such as oemof [133] and Temoa [134], are omitted for the sake of brevity.
- **Homer** is a commercial framework for energy system simulation and optimization [23]. Its focus is on optimal planning problems, i.e. investment decision support for renew- able energy and storage assets. Similarly positioned closed-source tools, such as
32

<u>3. Multi-energy system modeling and optimization 3.4. Existing software frameworks</u> EnergyPLAN [135], energyPro [136] and TIMES [137], are omitted for the sake of brevity.
- **CEA** is the City Energy Analyst [26], which is an open-source tool for the simulation and optimization of urban MESs. This tool focuses on the scenario-based analysis of energy systems and also enables genetic-optimization-based optimal planning.
As highlighted in section3.2, software tools for MES modeling can be characterized based on various modeling dimensions. In table3.1, the following dimensions are considered:

- **Sector coverage** is categorized in terms of the ability to model electric, thermal and MESs. In this context, electric power system tools comprise models for the electric grid and electric DERs. Thermal system tools enable the modeling of pipe networks for district heating / cooling and the thermal DERs. MES tools combine the modeling abilities of electric and thermal system tools. Note that other pipe networks, such as gas grids, are not explicitly distinguished here.
- **Solution method** is categorized into simulation and optimization. Simulation or fore- casting tools calculate the state variables of the energy system based on fixed inputs for control and disturbance variables, whereas optimization tools determine state and control variables that optimize an objective subject to operational constraints. Tools with mixed capabilities are categorized as such.
- **Optimization** methodologies are further categorized into convex, non-convex and heuristic approaches. Convex optimization is based on convex models and determinis- tic optimization solvers, where linear programming (LP), Quadratic programming (QC), second-order-cone programming (SOCP) and semi-definite programming (SDP) fall into this domain. Non-convex optimization utilizes deterministic solvers for non-convex problems, e.g. mixed-integer linear programming (MILP) through the branch-and- bound algorithm and non-linear programming (NLP) through the interior point algorithm. Heuristic optimization refers to genetic algorithms and associated algorithms as well as machine-learning-based optimization methods. Tools that enable multiple methodolo- gies are categorized as such.
- **Problem type** is categorized into operation and planning problems. Operation prob- lems include simulation and optimization on time horizons from hours to weeks for operation decision support as well as power system analysis. Planning problems include optimizations on time horizons from months to years for investment decision support.
Additionally, several specific model features are examined to characterize the sector coverage and solution method in more detail. To this end, the following features are considered:

- **Power flow simulation** describes the ability to solve the non-linear steady state electric power flow.
33

<u>3. Multi-energy system modeling and optimization 3.4. Existing software frameworks</u>
- **Power flow optimization** refers to the ability to solve an optimization problem based on the electric power flow.
- **Balanced AC model** highlights whether steady-state properties, i.e. voltage, branch flow and losses, can be represented for single-phase electric grids (see section6.1.2).
- **Multi-phase AC model** highlights whether steady-state properties, i.e. voltage, branch flow and losses, can be modeled for multi-phase unbalanced electric grids (see sec- tion6.1.4).
- **Transient dynamics model** describes the ability to model transient properties of the electric grid, in addition to steady-state properties.
- **Convex electric grid model** notes whether the electric grid model can be obtained in a convex form. This indirectly highlights whether the model formulation is accessible, which is typically not possible in closed-source tools.
- **Thermal power flow simulation** refers to the capability of solving the power flow problem of district heating / cooling systems.
- **Thermal power flow optimization** refers to the ability to solve an optimization problem based on the thermal power flow.
- **Fluid pressure model** highlights whether the thermal power flow includes a model for the fluid pressure.
- **Fluid temperature model** highlights whether a model for the fluid temperature is included.
- **Convex thermal grid model** notes whether the thermal grid model can be obtained in a convex form. This indirectly highlights whether the model formulation is accessible, which is typically not possible in closed-source tools.
- **DER simulation** describes the ability to simulate the system dynamics and behavior of DERs in the absence of any control or price signals.
- **DER optimization** describes the ability to solve an optimization problem considering system dynamics and behavior of DERs.
- **Convex DER model** notes whether the DER model can be obtained in a convex form. This indirectly highlights whether the model formulation is accessible, which is typically not possible in closed-source tools.
- **Multi-period simulation / optimization** refers to the ability to consider multiple time steps and capture inter-temporal linkages during simulation / optimization.
- **DLMP decomposition** is the ability to derive distribution locational marginal prices (DLMPs) or shadow prices as output of power flow optimizations. The DLMPs should further be decomposed into energy, loss and congestion components.
- **Energy market modeling** highlights the ability to model energy market-clearing algo- rithms or associated optimization problems.
The key takeaways from the feature comparison in table3.1can be summarized as follows:

<u>3. Multi-energy system modeling and optimization 3.4. Existing software frameworks</u>
- Simulation-focused tools and mixed-capability tools (PSS-SINCAL, PowerFactory, OpenDSS, GridLAB-D, MATPOWER, pandapower, pandapipes, OPEN) typically ad- dress operation problems, whereas optimization-focused tools (PowerModels.jl, urbs, Calliope, Homer, CEA) more commonly address planning problems. This may be due to many simulation-focused and mixed-capability tools being rooted in the power system domain, where optimization techniques are often applied for operation rather than planning decisions. At the same time, all MES tools (urbs, Calliope, Homer, CEA) are also optimization-focused tools. In fact, a subset of the MES tools (urbs, Calliope) does not support simulations, i.e. the models are strictly implemented as optimization problems.
- Electric grid modeling is possible through dedicated power system software (PSS- SINCAL, PowerFactory, OpenDSS, GridLAB-D, MATPOWER, pandapower, PowerMod- els.jl, OPEN) as well as MES tools (urbs, Calliope, Homer, CEA). However, only power system software provides detailed electric grid models, i.e. steady-state properties of balanced AC grids, whereas MES tools mostly utilize simplified energy balance / flow models¹. Further, multi-phase AC grid modeling is enabled only by a subset of the tools (PSS-SINCAL, PowerFactory, OpenDSS, GridLAB-D, PowerModels.jl, OPEN) and transient dynamic models, where available (PSS-SINCAL, PowerFactory, OpenDSS), are restricted to simulations, i.e. not available for optimization problems.
- Thermal grid modeling is enabled through dedicated pipe network simulation software (pandapipes) as well as MES tools (PSS-SINCAL, urbs, Calliope, Homer, CEA). Only a limited subset of tools (PSS-SINCAL, pandapipes, CEA) allows detailed thermal grid modeling including fluid pressure and fluid temperature properties, whereas most MES tools (urbs, Calliope, Homer) utilize simplified energy balance / flow models. Additionally, detailed thermal grid models are typically restricted to simulations².
- DER modeling is enabled by several power system and MES tools (GridLAB-D, MAT- POWER³, OPEN, urbs, Calliope, Homer, CEA). Detailed or custom DER system models can only be implemented in a subset of these tools (GridLAB-D, MATPOWER, OPEN, CEA), whereas other tools restrict the modeling to simplified dispatch and storage constraints (urbs, Calliope, Homer).
- The majority of tools clearly distinguishes between models for simulation and models for optimization because optimization models are usually adapted for the requirements of the optimization algorithm. To this end, these tools implement accurate non-linear models for simulation and approximate, e.g. convex or linear, models for optimization. This highlights the trade-off between accuracy and tractability in numerical optimization. The only exception is CEA, where the non-linear simulation models are directly utilized in the optimization through a genetic algorithm. 1 urbs implements a DC power flow model, where line flow and voltage are the only power flow variables. 2 CEA utilizes a genetic algorithm for optimization, i.e. the simulation is a sub-problem of the optimization. 3 MATPOWER enables augmenting its OPF problem with user-defined variables, constraints and cost
functions, which can be used to represent DER models

<u>3. Multi-energy system modeling and optimization 3.4. Existing software frameworks</u>
- Only MATPOWER directly enables obtaining distribution locational marginal prices (DLMPs) or shadow prices from the solution of the optimization. However, the DLMPs from MATPOWER are not decomposed into energy, loss and congestion terms. At the same time, there exists no tool which enables DLMPs for thermal grids or MESs.
- Energy market modeling is enabled in GridLAB-D and OPEN. GridLAB-D however only enables the usage of the market-clearing mechanism as part of a simulation problem. In OPEN, the energy market is enabled for optimization problems.
- All listed software tools either implement interfaces or are directly embedded in common programming languages, e.g. Python, MATLAB or Julia, whereas a small subset of tools (PSS-SINCAL, PowerFactory, OpenDSS, Homer, CEA) also provides a graphical user interface (GUI).
For a more comprehensive discussion of software tools for energy system modeling and optimization, please refer to the reviews [115], [116].

## 4 Fundamentals of software development

#### Contents

4.1 Software development life cycle......................... 37
4.1.1 Life cycle stages............................. 37

4.1.2 Life cycle models.	38
4.2 Software requirements.	39
4.2.1 Requirements development..	39
4.2.2 Functional requirements.	40
4.2.3 Quality attributes.. 41
4.3 Software architecture.	42
4.3.1 Scope and outcomes..	42
4.3.2 Design process.	42
4.3.3 Documentation.	43

4.1.2 Life cycle models............................ 38
**4.1 Software development life cycle**
**4.1.1 Life cycle stages** The software development life cycle (SDLC), also referred to as systems development life cycle, is a set of stages or phases that provides a foundation for organizing software projects. The stages of the SDLC can be characterized according to ISO 12207 [138, p. 17, Section
5.4] and ISO 24748 [139, p. 17, Table 1] as follows:
- In the **concept** or requirements gathering stage, the focus lies on identifying the stakeholders’ needs and the conceptualization of the project. This stage includes an initial system analysis and requirements development. The initial analysis seeks to identify main objectives, system boundaries, project feasibility and key capabilities compared to other solutions. This stage also includes the requirements development process, which identifies the software’s functional requirements and quality attributes. •During the **development** or design stage, the software requirements are transformed into software architecture. This begins with a detailed refinement of the requirements and specification of external interfaces. Based on the software architecture principles (section4.3), a suitable module structure and internal interfaces of the software system
37

<u>4. Fundamentals of software development 4.1. Software development life cycle</u> are designed. Furthermore, verification and validation tests should be defined at this stage. Regarding the architecture, feedback is obtained from all stakeholders who will produce, operate, use, support and retire the software. An initial prototype may be developed at this stage. •The **production** or construction phase refers to the transition from the software archi- tecture to the final software system. This begins with the translation of the architecture into source code. During this process, the software quality is assured by the verification and validation tests defined in the development stage. In addition, the software archi- tecture may be refined during this phase. At the end of this stage, the final software system is deployed and made available to the user.
- During the **utilization** or operation stage, the software system is in service. In this phase, the performance is continuously monitored and maintenance activities may be carried out.
- The **support** or maintenance stage covers activities to enable the continued use of the software system. This stage includes modifications to the original software architecture and implementation in order to address evolving requirements.
- The **retirement** stage refers to the process of taking the software system out of service.
Based on these stages, different SDLC models or software development processes define formalized approaches for the organization of software projects. Note that different naming conventions are possible for the stages of the SLDC, while the above nomenclature strictly follows ISO 24748. Notably, “development” may instead refer to the construction phase of the software project and “production” may refer solely to the deployment of the software project.

##### 4.1.2 Life cycle models

SDLC models or software development processes describe approaches for organizing the SDLC stages mentioned above. These models characterize different approaches for anticipating and addressing obstacles to manage the inherent uncertainties associated with cost, schedule, and functionality of the software project [138]. According to [140, pp. 44-45], the dominant models are:

- The **waterfall model**, which organizes the SDLC into a connected sequence of ac- tivities, i.e. the stages are completed one after the other with entry / exit conditions at the intersection of stages. The typical sequence is 1) concept, 2) development, 3) production, 4) utilization and 5) maintenance. Feedback paths are available on an as-needed basis but generally, the stages are performed unidirectionally from 1) to 5).
- **Iterative models**, which represent an enhancement of the waterfall model address the need for more feedback between different SDLC stages. In these models, the stages are still generally performed in sequential order from 1) to 5) according to waterfall model but the sequence is repeatedly executed. In each iteration of the sequence, a
38

<u>4. Fundamentals of software development 4.2. Software requirements</u> small subset of work is completed and passed as input to the next stage. The goal is to approach the final software system iteratively.
- **Agile methods**, which refer to a newer group of software development processes, e.g. Scrum, Extreme Programming and Crystal Clear. These methodologies are highly incremental and iterative, which represents a further evolution from the iterative models. Agile development is distinguished from iterative models by the more frequent delivery of software, close collaboration of developers and customers as well as an expectation of ever-changing requirements. These methods also employ variants of the SDLC stages, albeit significantly slimmed compared to their classical counterparts.
Evidently, for all presented SDLC models, the order of the SDLC stages roughly follows the order of their presentation in section4.1.1. The differences between SDLC models lie instead in the interlinking of the stages and the weighting of their importance. Particularly, the waterfall model and iterative models are generally more heavy on the concept and design stages, whereas agile methods put more emphasis on the production stage. Since the concept and development stages aim to uncover and reduce risks for the rest of the software project, the choice of SDLC model relates to the stakeholders’ risk appetite. As shown in [141, p. 29, Table 3-1], the average cost of fixing the costs increases in the later stages of the SDLC. However, the extensive preparatory effort may be outsized for small, informal software projects, where the rapid release may be more important to the overall project.

Since this work focuses mainly on documenting the outcomes of the concept and devel- opment stages for MESMO in chapter5, the remainder of this chapter is dedicated to the critical activities of these stages, i.e. requirements development in section4.2and software architecture in section4.3.

#### 4.2 Software requirements

##### 4.2.1 Requirements development

The outcome of the requirements development in the concept stage of the SLDC is a set of well-defined software requirements, which in turn serve as input to the design of the software architecture in section4.3. Traditionally, software requirements are distinguished into 1) functional requirements and 2) quality attributes, also referred to as non-functional requirements. The former defines the concrete functionality of the software, whereas the latter describes the characteristics of the system. Functional requirements are generally user-driven, whereas software engineers usually govern quality attributes. The process for obtaining the requirements can be structured according to [142, p. 15] into:

1. **Elicitation**, which involves the activities for discovering requirements, e.g. interviews, workshops, literature review or prototyping.
2. **Analysis**, which encompasses the structuring of received information into functional requirements and quality attributes.
39

<u>4. Fundamentals of software development 4.2. Software requirements</u>
**U1**: Use case 1 uses **U2**: Use case 2 **Actor** **Software system**

Figure 4.1: Exemplary use case diagram.

3. **Specification**, which refers to the translation of the requirements into a persistent and well-organized format.
4. **Validation**, which lastly ensures that the collected requirements satisfy the needs for input to design the software architecture.
The interested reader may refer to [142] for an extensive set of tools for the individual require- ments development phases. In the context of this work, the focus will be on the requirements analysis phase. Therefore, functional requirements are discussed in section4.2.2and quality attributes are elaborated in section4.2.3.

##### 4.2.2 Functional requirements

Functional requirements state what a software system must do and how it must react to user input [140, p. 64]. To this end, functional requirements are directly related to the goals, more specifically the business goals, of the stakeholders. According to [142, p. 9]:

Functional requirements specify the behaviors the product will exhibit under specific conditions. They describe what the developers must implement to enable users to accomplish their tasks (user requirements), thereby satisfying the business requirements.

An essential technique for analyzing functional requirements is use case modeling. Use case modeling aims at identifying how users interact with a software system to achieve their goals [140]. Essentially, use cases capture the key interfaces and functions through which users operate the system. This activity serves as a preparatory step in requirements gathering since use cases form the basis for functional requirements. Use cases are documented with

1) the use case diagram and 2) use case descriptions. The use case diagram is a unified modeling language (UML) diagram that depicts the relationship of actors and use cases. Figure4.1depicts an exemplary use case diagram. An actor is someone who interacts with the software system, where the categorization of actors is based on the roles of stakeholders. Actors are associated with use cases through communication links, which represent the bidirectional flow of information. Actors can have responsibilities towards the system, i.e. inputs, and expectations from the system, i.e. outputs, and each actor must be associated with at least one use case. A use case is a specific system function or process. Use cases can include or use other use cases, i.e. incorporate
40

<u>4. Fundamentals of software development 4.2. Software requirements</u> the behavior of the child use cases. Similarly, use cases can extend another use case, i.e. inherit and enhance the behavior of the parent use case. The use case description is textual and provides more detailed information on the actors’ relationship with each use case. In addition, the description specifies how an actor interacts with a system and how the system responds to the actions. This includes information on the pre-conditions, basic event flow, alternative flows, post-conditions and behavior in exception cases. User stories are a concept from agile software development that serve a similar purpose as use cases but are much less formal to reduce the up-front documentation effort. Instead, user stories capture what an user wants to achieve. To this end, user stories are not dissimilar to use cases but user stories deliberately exclude the context of the software system and the detailed process flow, which aims at eliciting ideas during development meetings.
##### 4.2.3 Quality attributes

Quality attributes, also referred to as non-functional requirements, characterize how well a software system functions and serve as assessment criteria for the software architecture. Therefore, the understanding of quality attributes guides the design and evaluation of software architecture. A complete typology for quality attributes is defined in ISO/IEC 25010 [143], where [140, p. 193, Section 12.4] provides a brief summary. According to [140, Chapters 5-11], the most common quality attributes for software systems are:

- **Availability** refers to the ability of the software system to avoid failures and to recover from failures.
- **Configurability** describes the ability to influence the behavior of the system without having to make implementation changes.
- **Interoperability** encompasses the ability to exchange data with other systems, i.e. syntactic interoperability, as well as the ability to interpret any exchanged data correctly,
i.e. semantic interoperability.
- **Modifiability** describes the ability to make changes to the functionality of the software system at reasonable development costs.
- **Performance** is about the ability of the system to meet timing requirements and complete operations within a reasonable runtime.
- **Testability** highlights the ability of the software system to reveal faults quickly, i.e. there should be a high probability for the system to reveal faults through appropriately designed tests.
- **Usability** is defined by the ease of learning or familiarization with the software system and the level of efficiency and convenience for the user to operate the system.
41

<u>4. Fundamentals of software development 4.3. Software architecture</u> The above-defined general quality attributes are system-independent and potentially apply to any software system. These attributes are selected and reformulated to apply for the system under consideration.
#### 4.3 Software architecture

##### 4.3.1 Scope and outcomes

Software architecture can be formally defined based on [140] as:

The software architecture is the set of structures needed to reason about the sys- tem, which comprises software elements, relations among them, and properties of both.

The role of software architecture, according to [144] is to support 1) uses cases of the software, 2) development of the software, 3) deployment of the software and 4) maintenance of the software. Use cases take the highest priority because these capture the purpose of the software and by definition, must be supported. In terms of supporting development, good software architecture helps to modularize development tasks such that different team members can work simultaneously without blocking each other. Deployment refers to setting up an instance of the software, where good software architecture helps limit the number of environments or dependencies that need to be set up. With respect to supporting mainte- nance, good software architecture anticipates changes to the software system, e.g. carefully defined internal interfaces reduce restructuring efforts when adding new components.

The outcomes of the software architecture design process can be subdivided into 1) module structures, 2) workflow structures and 3) allocation structures [140, pp. 10-11]. Module structures are the core element of the architecture and describe the decomposition of the system into a set of code and data units. This structure also defines how functional responsibilities are assigned to different modules. Workflow structures or component-and- connector structures characterize how different modules interact with one another during run time. Allocation structures are mappings of organizational and developmental manner,

e.g. how the module structure is reflected in the file structure of the source code or how the development tasks are distributed to the team members.
##### 4.3.2 Design process

The input for the design process of software architecture is the functional requirements and quality attributes. The goal of the design process is to address the most important require- ments, i.e. architecturally relevant requirements. Functional requirements are addressed in the design process by allocating responsibilities to architectural elements, i.e. assigning modules or classes to fulfill the functional requirements. However, functional requirements do not necessarily influence the structure of the software architecture, i.e. how the system is subdivided. For example, the functional requirements could be served by a single monolithic

<u>4. Fundamentals of software development 4.3. Software architecture</u> script file. To this end, the structure of the architecture is derived from the quality attributes or non-functional requirements, which also influence how architectural elements behave and interact [140]. The design process itself can be described as a series of decisions by the software architect. To highlight the concerns in the design process, consider the following categorization of design decisions according to [140, p. 73]:
1. **Allocation of responsibilities**, which refers to the identification and assignment of important system functions to architectural elements.
2. **Coordination models**, which are decisions on whether elements must interact or are prohibited from interacting as well as the mechanism of the interaction.
3. **Mappings among architectural elements** define how runtime workflows are orga- nized.
4. **Data models**, which specify the system-internal representation and organization of data and operations on the same.
5. **Management of resources**, which establishes the strategy to manage and interact with hardware systems.
6. **Binding time decisions** describe possibilities for variation in the architectural structure,
e.g. using a different set of modules depending on the type of user.
7. **Choice of technologies**, which refers to selecting the programming language(s), libraries and development tools for the architecture. This also refers to weighing the design constraints arising from the development team’s available languages, libraries or abilities.
Although the design process is not strictly formalized, guidance is available in the large body of literature on software architecture, e.g. [140], [144]–[147]. The available design guidance can be broadly categorized into 1) design tactics and 2) architectural patterns. Design tactics are first-order principles, i.e. fundamental methodologies that allow designing a software architecture from scratch. These tactics are often focused on achieving one distinct quality attribute and may require trade-off decisions by the software architect. Design tactics are extensively covered in [140], [144]. A general set of design tactics is proposed as “guidelines for good architecture” in [140, pp. 20-21]. Architectural patterns are packaged design decisions that have been repeatedly and successfully applied in practice. Such patterns refer to architecture classes with shared structures, behaviors and interactions between elements. Dedicated literature on architectural patterns is available in [145]–[147]. A comprehensive listing of tactics and patterns is omitted here and the interested reader is referred to the aforementioned literature.

##### 4.3.3 Documentation

To communicate the outcomes of the design process, the software architecture is documented by capturing the relevant architectural structures, i.e. module structures, workflow structures

<u>4. Fundamentals of software development 4.3. Software architecture</u>

||Module 1|uses|Module 2|Data item|
|---|---|---|---|---|
|Actor [Person]|[Module]|Software system X [Software system]|[Module]|[Data store]|

uses reads

Figure 4.2: Exemplary component diagram.

and allocation structures, as introduced in section4.3.1. To this end, multiple representations are possible for the same structure type, e.g. module-decomposition structure and data model as two distinct representations of module structures. Refer to [140, p.15, Table 1.1] for an overview of architectural structures. For the documentation, only the most meaningful structures need to be represented. For example, single-threaded software systems do not warrant the documentation of a concurrency diagram.

Views are utilized to break down structures into comprehensible elements, thereby managing the complexity in the documentation. Views describe abstract representations of the struc- tures, documented according to a chosen notation. The most common representations have been standardized in UML [148]. Alternatively, the C4 model [149], [150] defines a less formal set of structure views, which is often preferred in the agile development community [151]. Most software projects do not set strict requirements for the views. Instead, the chosen representation must be suitable to break down the complexity of the particular software architecture for the understanding of the development team. To this end, [140, p. 345, Section 18.6] suggests documenting the chosen format along with views themselves.

For this work, the C4 model [149], [150] is adapted to represent module structures, workflow structures and allocation structures for MESMO in chapter5. The C4 model represents architecture structures in terms of the following elements:

- A **person** represents any stakeholder or actor who interacts with the software system.
- The **software system** is the highest level of abstraction and consists of container and component elements.
- **Containers** describe subsystems or data stores, where each container is implemented / deployed separately.
- A **component** represents a grouping of functionality, such as a module in Python, which exposes a well-defined interface to other components.
- **Code** elements refer to the lowest level of abstraction, i.e. classes, objects, methods and functions.
Based on these elements, the C4 model establishes the following four hierarchical levels:

1. The **context diagram** serves to provide an overview, i.e. the interaction of the software system with the stakeholders and other software systems.
44

<u>4. Fundamentals of software development 4.3. Software architecture</u>

|Class 1|Class 2|uses Function 1|reads Data item|
|---|---|---|---|
|[Class]|[Class] Module X [Module]|[Function]|[Data store]|

extends

Figure 4.3: Exemplary code diagram.

2.The **container diagram** depicts a software system in terms of its container elements.
3. The **component diagram** decomposes each container into its components and high- lights the dependencies between different components. Figure4.2depicts an exem- plary component diagram.
4. The **code diagram** depicts the relationships between code elements of the software system. An exemplary code diagram is shown in fig.4.3.
The hierarchical levels serve as views for the different structures of the software architecture. The allocation structures, e.g. deployment and implementation structures, can be represented with the container diagram. Further, the module structures, e.g. decomposition and uses structures, can be represented with component and code diagrams. Lastly, the workflow structure can be represented with adapted component and code diagrams.

## Part II

# Methodology

## 5 Software architecture of MESMO

#### Contents

5.1 Prerequisites................................... 47
5.1.1 Scope................................... 47
5.1.2 Use case modeling........................... 48
5.1.3 Functional requirements........................ 50
5.1.4 Quality attributes............................ 52
5.2 Software architecture.............................. 55
5.2.1 Overview................................ 55
5.2.2 Module structures........................... 55
5.2.3 Workflow structures........................... 67
5.2.4 Allocation structures.......................... 70
**Outline and contributions**

This chapter describes the development process of the software architecture for MESMO. The process is directly based on the software development fundamentals outlined in chapter4. First, section5.1addresses prerequisites, i.e. use case modeling and requirements develop- ment. Then, the software architecture itself is outlined in section5.2, thereby addressing the use cases and requirements.

The software architecture constitutes the core original contribution of this thesis and the author entirely derived the definitions of stakeholders, use cases, requirements and software architecture.This forms the foundation for the software implementation of MESMO. A precursor of this work has been published by the author in [30]. The author has also been the core developer and maintainer of the MESMO software repository.

**5.1 Prerequisites**
**5.1.1 Scope** Revisiting the objectives of this thesis in section1.2, MESMO is developed to complement the existing software in the domain of district-scale energy system simulation and optimization.
47

|5.|Software architecture of MESMO|||5.1.|Prerequisites|
|---|---|---|---|---|---|
|||||U9||
|||uses||||
||U1 : Define scenario data|uses||U10||
|||uses||||
|||||U1 1||
|||||U12||
|||||U13||
||||uses uses|U14 : Obtain DER||
||U2 : Run nominal uses operation problem|U6 : Solve simulation problem|uses|time series model||
||U3 : Run optimal uses operation problem uses U4 : Run optimal planning problem uses|U7 : Solve optimization problem|uses uses uses|U15 U16 U17 DER model||
||uses uses|||U18 operation results||
||||uses uses uses|U19 operation results U20 : Obtain DER operation results||
||U5 : V iew result plots uses|U8 : Obtain results|uses|U21||
||||uses|||
|||||U22||
|||MESMO||||
||Use case modeling|||||
||1|||||
|||48||||

: Define electric grid data

: Define thermal grid data

: Define DER data **System operator** : Obtain non-convex electric grid model : Obtain non-convex thermal grid model

: Obtain convex **Researcher** **System planner** electric grid model : Obtain convex thermal grid model : Obtain convex

: Obtain electric grid

: Obtain thermal grid **Decision maker**

: Obtain electric DLMPs

: Obtain thermal DLMPs

Figure 5.1: Use case diagram for MESMO.

Therefore, it combines 1) convex MES modeling for 2) optimization-focused studies on the operation-timescale with a focus on 3) market-clearing and DLMP-based pricing mechanisms. Essentially, MESMO is developed as a software framework for defining and solving numerical optimization problems for MES operation. It implements convex models for electric grids, thermal grids and DERs, along with a set of optimization-focused utilities.

The mathematical modeling methodologies implemented in MESMO are introduced in chap- ters6to8for the electric grid, the thermal grid and DERs. The problem definitions for nominal and optimal operations are provided in chapter9. To this end, those chapters define the low-level details for the model implementations. The current chapter instead focuses on the high-level structural aspects of the software system.

##### 5.1.2

In preparation for MESMO’s software architecture development, specific use cases for MESMO are outlined in the following, which then form the basis for identifying the functional requirements in section5.1.3. Figure5.1depicts the use case diagram for MESMO. The following possible stakeholders in district-scale MESs are included as actors¹ in the use case diagram:

The term “stakeholder” is used instead of “actor” in the following, for consistency with the rest of the thesis.

<u>5. Software architecture of MESMO 5.1. Prerequisites</u>
- The **system operator** is responsible for maintaining and operating the district-scale energy system. This stakeholder is interested in modeling and optimizing short-term to medium-term dispatch decisions.
- The **system planner** looks at the long-term operation and upgrading of the district-scale energy system. This stakeholder seeks to model future developments and optimize long-term investment decisions.
- The **decision-maker**, e.g. policy maker or utility executive, takes responsibility for the strategic development of the district-scale energy system. This stakeholder is primarily interested in evaluating results prepared by other stakeholders.
- The **researcher** works on research and development tasks in the context of district- scale energy systems, e.g. investigation of novel operation strategies. To this end, the researcher is associated with the most diverse set of use cases.
These stakeholders are identified through observation of the fundamental activities in research and corporate contexts. MES studies are typically performed in an exploratory fashion in the research context, i.e. the model and problem formulation are continually iterated and require a high degree of modifiability. In the corporate context, the focus lies on obtaining insights in a highly effective manner, i.e. results for a study should be obtained quickly and reliably. Since activities in the corporate context are repeating continuously, the automation of typical tasks is a crucial concern. Both research and corporate work is often structured in projects with regular reporting intervals, where the upper-level funding agency expects results to be presented in a highly convenient fashion. These different concerns are best captured through the proposed classification of stakeholders into researcher, system operator, system planner and decision-maker.

Figure5.1highlights that use cases can be distinguished into 1) high-level functionality (U1 to U5) and 2) low-level functionality (U6 to U22). On the one hand, the system operator, system planner and decision-maker are interested in off-the-shelf solutions for their particular problems, e.g. running operation and planning problems (U2, U3, U4). On the other hand, the researcher requires more granular abilities, e.g. for setting up a custom optimization problem based on the bundled convex grid and DER models (U15, U16, U17).

On the high-level side, U1 describes the use case for defining scenario data to set up a test case for a district-scale energy system. The use cases U2 and U3 characterize the need to run nominal and optimal operation problems. The nominal operation problem (U2) is a simulation where inputs are provided for control variables, whereas the optimal operation problem (U3) determines optimal values for control variables based a numerical optimization. The use case U4 encapsulates solving a numerical optimization problem for the optimal energy system design and sizing. Results for each problem run should be returned in U2, U3 and U4 but U5 additionally describes a use case for producing results plots to visualize the outcomes of the problem runs. The system operator is using U1, U2, U3 and U5, whereas the system planner is associated with U1, U4 and U5. The decision-maker relies on system operator, system planner or researcher to prepare results, thereby only interacting with MESMO through U5.

<u>5. Software architecture of MESMO 5.1. Prerequisites</u> On the low-level side, U9, U10 and U11 describe the ability to define data for electric grid, thermal grid and DERs of a district-scale energy system. U9, U10 and U11 are included in U1 but exposed individually on the low-level side due to the more granular interest of the researcher. U6 and U7 are use cases for solving simulation problems and optimization problems, where U6 is used by U2 and U7 is used by U3 / U4. The researcher is directly associated U6 and U7 to enable modifications, e.g. adding additional constraints of the specific optimization problem. Solving a simulation problem in U6 uses U12, U13 and U14 for obtaining non-convex grid models and DER time series models. Solving an optimization problem in U7 additionally uses U15, U16 and U17 to obtain convex models for electric grid, thermal grid and DERs. Note that U12 to U17 are also associated with the researcher to enable constructing custom problem types directly from models. Once simulation or optimization problems have been solved in U2, U3, U4, U6 or U7, the solution results are obtained using U8, which uses U18 to U22 to get individual results components. Producing results plots in U5 correspondingly uses U8. The use cases U18, U19 and U20 are for obtaining results for the control, state and output variables of electric grid, thermal grid and DERs. Additionally, U21 and U22 describe the ability to retrieve DLMP values for electric and thermal grids. The researcher is directly associated with U18 to U22 as well.
##### 5.1.3 Functional requirements

The functional requirements for MESMO are directly derived from the use case modeling in the previous section. The functional requirements in this section restate the outlined use cases. Therefore, the following does not constitute a formal requirements document but rather a listing of grouped use case descriptions:

1. To address U2, U3 and U4, MESMO must provide high-level programmable inter- faces for the system planner and the system operator. These interfaces should be programmable such that these stakeholders can build custom workflows based on MESMO in at least one high-level programming language, such as Python or MATLAB. The high-level interfaces should implement the following problem types:
- Nominal operation problem, i.e. a simulation problem for the district-scale energy system, considering fixed nominal input for DERs’ power time series.
- Optimal operation problem, i.e. a numerical optimization problem for the minimiza- tion of operation cost, subject to the operational constraints of the district-scale energy system and its DERs.
- Optimal planning problem, i.e. a numerical optimization problem for the minimiza- tion of investment cost and operation cost, subject to the capacity and operational constraints of the district-scale energy system and its DERs.
2. To address U5, MESMO must implement a GUI for the decision-maker to analyze and interact with the results for scenarios that any other stakeholder has prepared. This GUI is intended as means for the demonstration of results in a high-level manner to facilitate the dissemination of findings from technical to non-technical personnel.
50

<u>5. Software architecture of MESMO 5.1. Prerequisites</u> Thus, the GUI takes over the role of manual post-processing and results visualization workflows from system planner, system operator or researchers.
3. With regards to U12 to U22, MESMO must implement low-level programmable inter- faces for the researcher, which are characterized by highly granular access to the model formulations. To this end, MESMO must ensure that models are subdivided into reasonably small modules in accordance with their mathematical formulation, which enables the researcher to modify or replace any part of the modeling tool-chain with custom mathematical expression. Thus, the researcher must be able to test new mathematical approaches and define highly custom workflows depending on the study topic at hand. The fundamental structure of the low-level interfaces is outlined as: •Electric grid modeling: **–** Obtain nodal and branch admittance matrices and incidence matrices for the
electric grid according to section6.1. **–** Obtain steady state power flow solution for nodal voltage, branch flows and losses via fixed-point algorithm according to section6.2.2. **–** Obtain sensitivity matrices of global linear approximate electric grid model according to section6.3. •Thermal grid modeling: **–** Obtain nodal and branch incidence matrices and friction factors according to section7.1. **–** Obtain thermal power flow solution for nodal pressure head, branch flows and pumping losses according to section7.1.2. **–** Obtain sensitivity matrices of global linear approximate thermal grid model according to section7.3. •DER modeling: **–** Obtain time series models for fixed DERs according to section8.2. **–** Obtain state-space models for flexible DERs according to section8.3. **–** Enable the modeling of fixed loads, fixed generators, flexible loads, flexible generators, ESSs, EV chargers, DHSs and DCSs. Enable flexible building modeling through the CoBMo toolbox [45]. •MES operation: **–** Obtain and solve nominal operation problems, i.e. steady-state simulations, of electric and thermal grids with DERs, i.e. MESs. **–** Define and solve numerical optimization problem for combined optimal oper- ation for electric and thermal grids with DERs, i.e. MESs. **–** Obtain DLMPs for the electric and thermal grids.

4. Regarding U1, U9, U10 and U11, MESMO must define a coherent scenario input data format comprising a complete set of model parameters for electric grid models, thermal grid models and DER models. The input data must be sufficiently well documented for system planner, system operator or researchers to define the test cases directly.
51

<u>5. Software architecture of MESMO 5.1. Prerequisites</u> Furthermore, MESMO must be enabled for interacting with common district energy system data formats, such as the MATPOWER format and the OpenDSS format.
5. To address U8 internally, MESMO must define a standardized results data object. The results object serves as an interface between high-level problem type definitions and low-level model definitions. To this end, the results object ensures that post-processing workflows can be developed independently of the specific models or interfaced prob- lems. In terms of MESMO development, this also facilitates standardization for inputs to the GUI.
6. Lastly, U6 requires MESMO to interface numerical solvers for convex optimization. Therefore, MESMO must define variables, constraints and objective for the optimization problems and retrieve both primal and dual variable results.
Recalling from section4.2, the functional requirements state what the software system must do. During the development of the software architecture, these functionalities or use cases are assigned to specific modules of the software. However, as stated in [140, p. 65, Section

4.2]:
##### Functionality does not determine architecture.

This is only partly true for MESMO because the structure of code elements is indeed aligned with the underlying mathematical modeling as highlighted in point 3 above. However, on a higher level, the software architecture is primarily informed by the quality attributes outlined in the next section.

##### 5.1.4 Quality attributes

The gathering of quality attributes focuses on narrowing down the architecturally significant requirements (ASRs) that inform architectural decisions. This process essentially applies, refines and specifies the quality attributes from the reference list provided in section4.2.3. For MESMO, the quality attributes were gathered by assessing the business goals of stakeholders during the project Platform for Interconnected Micro-Grid Operation (PRIMO), which is a collaboration between TUMCREATE, EDF Lab Singapore, Singapore Institute for Technology (SIT) and Nanyang Technological University (NTU). In this project, MESMO is intended as the underlying library for expressing optimal operation problems in the context of urban microgrids. To this end, the discussion among corporate and research entities in the project served as a valuable source for the definition of ASRs.

As a valuable structure for documenting quality attributes, [140, p. 304, Section 16.4] proposes the utility tree, i.e. a list-based format. In this format, the first level defines the quality attribute type, the second level defines the attribute refinement and the third level describes the ASR. Each item is labeled with a pair of “high”, “medium” and “low”, where the first label indicates the ASRs importance and the second level indicates its effect on the architecture. Based on this format, the quality attributes for MESMO are outlined as follows:

<u>5. Software architecture of MESMO 5.1. Prerequisites</u>
- **Configurability**
1.Custom mathematical models **–** Description: MESMO must enable the combination of built-in and custom externally defined mathematical models for the researcher. The researcher must be able to set up such a custom test case in less than a week. **–** Importance: high **–** Impact on architecture: medium
2.Custom problem types **–** Description: The software must support the formulation of custom simulation or optimization problems. The researcher must be able to define custom problem types based on the MESMO low-level APIs within less than 1 week. **–** Importance: high **–** Impact on architecture: medium
- **Interoperability**
3.Optimization solver compatibility **–** Description: MESMO must enable the utilization of the most widely available convex optimization solvers. The user must be able to set up and configure a different solver within less than 10 minutes. **–** Importance: medium **–** Impact on architecture: high
4.Software dependencies **–** Description: MESMO must be able to run on Windows, Mac and Linux without requiring the installation of commercial software. New users must be able to complete the software setup within less than 1 hour. **–** Importance: medium **–** Impact on architecture: medium
- **Modifiability**
5.Extending mathematical models **–** Description: MESMO must support the extension or change of mathematical models for electric grids, thermal grids and DERs. Fundamental changes to modeling methodologies must be implemented by a developer within less than one month. **–** Importance: medium **–** Impact on architecture: high
6.Extending problem types **–** Description: MESMO must support the definition of additional MES problem types. The implementation of a new problem type must be completed by a developer within less than one month. **–** Importance: medium
53

<u>5. Software architecture of MESMO 5.1. Prerequisites</u>
##### – Impact on architecture: high

- **Performance**
7.Solution time **–** Description: MESMO must facilitate reasonable solution time for medium- scale problems. Optimal operation problems for MESs with 1000 grid nodes and 1000 DERs and 48 time steps must be completed within less than 10 minutes. **–** Importance: medium **–** Impact on architecture: medium
8.Resource utilization **–** Description: The software must be able to run on medium-range business laptops, where the solution of optimal operation problems for MESs with 1000 grid nodes and 1000 DERs and 48 time steps must be completed without exceeding the resources of the system. **–** Importance: low **–** Impact on architecture: medium
- **Testability**
9.Unit testing coverage **–** Description: All mathematical modeling methodologies implemented in MESMO must be individually testable. Test coverage of unit test must be above 90 %. **–** Importance: low **–** Impact on architecture: low
- **Usability**
10.Learning curve **–** Description: The software must provide freely accessible documentation to facilitate untrained users to setup and use MESMO in less than 1 month. **–** Importance: medium **–** Impact on architecture: medium
11.Input error handling **–** Description: This ASR also considers the ability to detect failures that may not be obvious to the user, e.g. an incorrect power flow solution due to an error in the input data. **–** Importance: medium **–** Impact on architecture: low
Noted that the quality attributes are ordered alphabetically and not by importance. Note also that only the most important quality attributes in the context of MESMO are included in this list.

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
#### 5.2 Software architecture

##### 5.2.1 Overview

The software architecture for MESMO is defined in the following in terms of 1) module structures, 2) workflow structures and 3) allocation structures according to section4.3.1. The notation is based on the C4 model, which is introduced in section4.3.3. Although its notation is traditionally intended for views of the module structure, the C4 model is also utilized in the workflow and allocation structures for a more consistent representation of individual elements across the different views.

The different views of module structures describe the decomposition of the software system into data containers, modules, classes and functions. In line with the C4 model, the module structures are first introduced from a high level in the context view, which is followed by a comprehensive overview in the component view. Then, the individual modules are introduced though their respective code views. Note that code views of the plots and dashboard modules are omitted in the following because the concrete functionality has not been finalized at the time of writing. Similarly, the planning problem is currently not included in software architecture because this problem type has not yet been in MESMO.

The module structures are followed by the workflow structures for the exemplary nominal and optimal operation problems. The purpose of the workflow structures is to provide an understanding of the data and run-time event flow when executing a problem. This also serves as a template for user-developed custom workflows which utilize low-level module interfaces. Lastly, the allocation structures present an overview of the dependency, repository and branch structures, relevant to any developers contributing to MESMO. For the dependency structure, the container view of the C4 model is utilized.

##### 5.2.2 Module structures

##### Context view

Figure5.2depicts the context view of MESMO, i.e. a high-level overview of the most critical components and the interaction between the software system and its stakeholders. The user interfaces can be distinguished into high-level interfaces, i.e. the api module and the dashboard module, and low-level interfaces, i.e. the models modules. To this end, the api module and models modules describe programming interfaces, whereas the dashboard denotes the GUI. Researchers primarily interface MESMO directly through the models modules because they require highly granular access and modifiability of the model objects for custom workflows. System planners and system operators interface MESMO through the api module, which provides convenient access to the most common workflows, i.e. running nominal and optimal operation problems and producing results plots. Decision-makers interface MESMO through the GUI of the dashboard module. Note that the dashboard module has not yet been implemented at the time of writing.

Scenario and model data definitions are enabled through a standardized CSV-based input

<u>5. Software architecture of MESMO 5.2. Software architecture</u> defines
**Researcher** **System planner** [Person] **System operator** [Person] **Decision maker** [Person] [Person] uses uses uses

**Input files Application programming interface dashboard** **(*.csv) models** **(api)** [Module] [Data store] [Module] [Module] uses uses uses uses reads **data_interface problems plots** [Module] [Module] [Module]

uses **MESMO** [Software system]

**Low-level interfaces High-level interfaces**

Figure 5.2: Context view of MESMO.

file format, which is referred to in fig.5.2as “Input files (*.csv)”. The input files are expected to be defined by researchers, system planners and system operators. Decision-makers are expected to rely on other stakeholders to define appropriate scenarios for their review.

Internally, the api module implements API functions that rely on the problem module and plots module. The dashboard module implements the GUI framework but relies on the plots module to generate individual plots. The problems module implements the main workflows for setup and solution of different problem types, for which it uses the mathematical models defined in the models modules. The problems module also implements a standardized results object across all problem types, which is used by the plots module. The models modules further rely on the data_interface module to obtain the model data definitions from the input files.

##### Component view

The component view of MESMO in fig.5.3provides a complete overview of all components,

i.e. modules and data stores, of MESMO. The interaction between stakeholders and the software system follows the structure that has been outlined for fig.5.2and is not repeated here. Compared to fig.5.2, the models modules are represented individually in fig.5.3 as der_models module, electric_grid_models module and thermal_grid_models module. Further, the problems module, plots module and models modules all use the utils module, which implements auxiliary functionality, such as base classes and logging functions. Researchers may use the OptimizationProblem class and results-path creation function from the utils module for creating custom workflows and optimization problem definitions.
56

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
uses uses [Person] [Module] **dashboard** **Decision maker**

**plots** [Person] [Module] **System operator** **High-level interfaces**

uses **(api)** uses uses [Module]

|[Person]|Application programming interface|problems [Module]|||
|---|---|---|---|---|
|System planner||uses|uses||
||_models [Module] electric_grid|uses utils [Module]||MESMO [Software system]|

uses

Figure 5.3: Component view of MESMO.

|_models [Module]|uses config [Module]||
|---|---|---|
|thermal_grid|reads|config.yml / [Data store] config_default.yml|
||uses||

**Low-level interfaces**

|[Person] uses|[Module]|uses [Module]|reads/ writes Database|
|---|---|---|---|
|Researcher|der_models|data_interface|[Data store] (database.sqlite)|

defines **(*.csv)** reads **Input files**[Data store]

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
**config.yml config_default.yml** [Data store] [Data store]

reads

|parallel_pool|get_parallel|get_logger()|
|---|---|---|
|[Multiprocessing|sets _pool()|[Function]|
|Pool]|[Function] config [Module]||

|config|sets get_config()|uses base_path|
|---|---|---|
|[Dictionary]|[Function]|[String]|

Figure 5.4: Code view of the configuration module.

In addition to the above-described functionality, data_interface module creates an internal database, i.e. database.sqlite, which serves as a temporary data store for scenario and model data. The internal database enables the utilization of SQL statements for efficiently transforming the input data into model data objects, which are then used by the models modules. The config module facilitates the declaration of configuration parameters, e.g. the level of logging outputs or the choice of optimization solvers. It is used by the data_inter face module, utils module, problems module, plots module and models modules. The config module reads configuration parameter definitions from the data stores config.yml and config_default.yml in YAML format [152].

MESMO is intended as a software system that is deployed to individual workstations akin to a traditional desktop application, where all data and dependencies are kept local. Nevertheless, the software architecture is kept flexible enough to support alternative deployment structures in future, e.g. provisioning of a remote database system for the internal data store or operating MESMO as a server-side system that serves a web-based dashboard.

##### Configuration module

The config module (fig.5.4) implements the following functionality:

##### •Declaration of configuration variables in get_config().

##### •Setup of logger object in get_logger().

##### •Setup of parallel pool in get_parallel_pool().

The get_config() function is executed upon initialization of the config module and sets the config dictionary, which is available as public global variable for all modules of MESMO. The config dictionary encapsulates configuration parameters, such as logging level and optimization solver selection. The configuration parameters themselves are defined in the data stores config.yml and config_default.yml, where get_config() first reads the

<u>5. Software architecture of MESMO 5.2. Software architecture</u>

|ObjectBase|memoize()|log_time()|
|---|---|---|
|[Class] extends|[Function]|[Function]|
|ResultsBase|get_index()|get_timestamp()|
|[Class]|[Function]|[Function]|
|||uses|
|Optimization|get_element|get_results_path()|
|Problem|_phases_array()|[Function]|
|[Class]|[Function]||
|starmap()|get_element|write_figure|
|[Function]|_phases_string()|_plotly()|
||[Function]|[Function]|
||utils [Module]||

Figure 5.5: Code view of the utility module.
 latter to obtain the default settings and then config.yml for user-defined configuration parameters which supersede the default settings. The setup of logger objects is handled by get_logger(), where all other modules of MESMO instantiate a local logger object through get_logger() upon their initialization. The logger object itself is implemented in logging.Logger² of the Python standard library. However, get_logger() takes care of setting the logging level according to the configuration settings. The function get_parallel_pool() is used by starmap() from the utils module to instantiate a parallel pool upon first use. A handle to the parallel pool object is then set to the global variable parallel_pool. The usage of parallel processing is controlled through a configuration parameter. Aside from the functionality mentioned above, the config module also defines run-time settings for various Python modules upon initialization. For example, at the time of writing, default settings for the pandas and plotly libraries are set here.
##### Utility module

The utils module (fig.5.5) implements the following functionality:

##### •MESMO object base class in ObjectBase.

##### •Results object base class in ResultsBase.

##### •Optimization problem class in OptimizationProblem.

•Parallelization utility function in starmap(). 2 [https://docs.python.org/3/library/logging.html#logger-objects](https://docs.python.org/3/library/logging.html#logger-objects)

<u>5. Software architecture of MESMO 5.2. Software architecture</u> •Memoization, i.e. caching, function decorator in memoize().
- Indexing utility functions in get_index(), get_element_phases_array() and get_element_phases_string(). •Utility functions to capture and log elapsed time in log_time().
- Helper functions to create and return a current time stamp in get_timestamp and a path for a new results folder in get_results_path(). •A write utility function for plotly figures in write_figure_plotly().
The utils module essentially provides support functionality for the other modules of MESMO. To begin, the ObjectBase, ResultsBase and OptimizationProblem define base classes for MESMO, such that common functionality is not multiply defined in the model modules.

The starmap() and memoize() functions enable performance improvements to address the solution time ASR. Parallelization is enabled through the starmap() function, which can be utilized to process independent function executions in parallel, e.g. the initialization of multiple DER models. Therefore, starmap() replaces for-loop instances. Caching functionality is enabled with the memoize() decorator, which can be applied to arbitrary functions for speedup, i.e. the results of function calls are stored for subsequent calls. The memoize() is added to function definitions to enable the caching of the respective functions. Note that both starmap() and memoize() can be disabled though configuration parameters, i.e. the performance behavior of MESMO can be influenced without requiring source code changes.

The get_index(), get_element_phases_array() and get_element_phases_strin g() functions define low-level functionality to support convenient indexing into vectors and matrices of the mathematical model formulations. This is heavily utilized in the model modules.

The log_time() function enables time-based logging of function executions, which is mainly utilized in the problems module. This function is aimed at improving the testability of MESMO. Lastly, the get_timestamp, get_results_path() and write_figure_plotly() are helper functions that support the output of results.

##### Data interface module

The data_interface module (fig.5.5) implements the following functionality:

•Function to connect to the internal database in connect_database().

- Function to create or clear the internal database and reload all data from the input files in CSV format in recreate_database().
- Data container objects for scenario data in ScenarioData, price data in PriceData, DER data in DERData, electric grid data in ElectricGridData and thermal grid data in ThermalGridData.
60

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
**Database Input files** **(database.sqlite) (*.csv)** [Data store] [Data store]

reads writes reads

**connect recreate** **_database() _database()** [Function] uses [Function] uses

**ElectricGridData** uses **ScenarioData** uses **DERData** [Class] [Class] [Class]

uses **PriceData ThermalGridData** [Class] [Class] **data_interface** [Module]

Figure 5.6: Code view of the data interface module.

The primary purpose of the data_interface module is to address the software quality attributes regarding interoperability and modifiability. To this end, the data container objects of this module serve as an abstraction layer between external and internal data structures. More specifically, internal model objects, e.g. ElectricGridModel, rely exclusively on data container objects, e.g. ElectricGridData, for their model parameter input but do not read any external data definitions directly. This leans on the “clean architecture” principle from [144, p. 195, Chapter 22], which suggests that software layers that implement core functionality, i.e. models modules, should not need to know anything about the external interfaces of the software system, i.e. the input data definitions. This approach supports interoperability and modifiability because changes to the external data formats of MESMO do not induce any changes in the model implementations. Note however, that changes in the model implementations may indeed require changes to the data interface, as the required model parameters may change.

The connect_database() function establishes the connection to the internal database and returns a connection handle. At the time of writing, MESMO utilizes an SQLITE database as internal database, which is stored locally as database.sqlite. On the other hand, if the local database does not yet exist, it is created through a call to recreate_database(). This function creates an empty database and loads the CSV input files into the database. If the local database exists, a call to recreate_database() clears the existing database before parsing the CSV input files. The MESMO CSV input format is aligned with the internal database schema, such that each CSV file corresponds to a table in the SQL database. Therefore, the CSV file name is interpreted as table name and the values in the first row are interpreted as column names. Note that MESMO can in principle be adapted to use other SQL database software than SQLITE, through modification of connect_database() and recreate_database().

<u>5. Software architecture of MESMO 5.2. Software architecture</u>

||ElectricGridModel||LinearElectricGrid|
|---|---|---|---|
||[Class]||Model [Class] extends|
|ElectricGridModel|extends|ElectricGridModel|LinearElectricGrid|
|OpenDSS||Default|ModelGlobal|
|[Class] uses|PowerFlowSolution [Class]|[Class]|[Class] uses|
|PowerFlowSolution|extends|PowerFlowSolution|ElectricGrid|
|OpenDSS||FixedPoint|OperationResults|
|[Class]||[Class] PowerFlowSolution ZBus [Class] electric_grid_models [Module]|[Class] ElectricGrid DLMPResults [Class]|

uses

uses

uses

Figure 5.7: Code view of the electric grid models module.

The data container objects, i.e. ScenarioData, PriceData, DERData, ElectricGridDa ta and ThermalGridData, implement routines for selecting and transforming data from the database into a suitable format for the model input. To this end, the data containers encapsulate only the relevant data items for the corresponding model class and the current scenario. The DERData, ElectricGridData and ThermalGridData objects contain model parameters for the namesake model classes. The PriceData contains the set of price time series for the current scenario. The ScenarioData object contains scenario information, such as the set of time steps and general parameters of the current scenario. Note that other data objects use the ScenarioData object, e.g. to obtain the set of time steps for resampling time series data.

##### Electric grid models module

The electric_grid_models module (fig.5.7) implements the following functionality:

- Fundamental electric grid models in ElectricGridModel, ElectricGridModelDefau lt and ElectricGridModelOpenDSS.
- Power flow solution algorithms in PowerFlowSolution, PowerFlowSolutionFixedPo int, PowerFlowSolutionZBus and PowerFlowSolutionOpenDSS.
- Linear electric grid models in LinearElectricGridModel, LinearElectricGridMo delGlobal and LinearElectricGridModelLocal.
62

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
- Electric grid operation problem results in ElectricGridOperationResults and ElectricGridDLMPResults.
The ElectricGridModel class implements a base class for electric models, which consists of index sets for nodes, branches and DERs and reference vectors for the nodal voltage, branch power flow and DER power injection / load. This base class is extended in Elec tricGridModelDefault with the mathematical definitions of the fundamental electric grid model. To this end, the model implements nodal and branch admittance matrices along with branch and DER mapping matrices. The ElectricGridModelOpenDSS similarly extends the ElectricGridModel class, where the focus lies on implementing an OpenDSS model based on the provided grid definition data. This essentially acts as an interface to OpenDSS [20], which is provided in MESMO to allow for benchmarking of obtained power flow solutions. The implementation relies on OpenDSSDirect.py [153], which provides a Python interface and command-line executables of OpenDSS.

The PowerFlowSolution class implements an abstract base class for power flow solutions, thereby declaring the expected output variables of the power flow solution. This base class is extended in PowerFlowSolutionFixedPoint for the fixed-point solution algorithm and in PowerFlowSolutionZBus for the Z-bus solution algorithm, which both use and ElectricGridModelDefault object as an input for the power flow solution. The PowerF lowSolutionOpenDSS class implements a power flow solution through OpenDSS, where it relies on an OpenDSS model being defined in ElectricGridModelOpenDSS.

The LinearElectricGridModel class implements a base class for linear electric model, where the expected sensitivity matrices of the linear grid model are declared. This class also implements the methods define_optimization_variables, define_optimization_c onstraints and define_optimization_objective to define variables, constraints and objective for an optimal operation problem based on the linear grid model. Further, the base class implements get_optimization_results and get_optimization_dlmps to obtain the DLMPs and other results after the optimization problem was solved. The linear model base class is extended in LinearElectricGridModelGlobal and LinearElectricGridMo delLocal with the mathematical definitions for the sensitivity matrices based on the global and local approximation methods.

The results container classes ElectricGridOperationResults and ElectricGridDLMP Results encapsulate the output from get_optimization_results and get_optimizatio n_dlmps. To this end, the container classes declare a standardized interface for results data. This addresses the software quality attribute for modifiability since it ensures a decoupling of the mathematical model implementation from the post-processing functionality in the plots and dashboard modules.

##### Thermal grid models module

The thermal_grid_models module (fig.5.8) implements the following functionality:

##### •Fundamental thermal grid model in ThermalGridModel.

<u>5. Software architecture of MESMO 5.2. Software architecture</u>

|||uses|
|---|---|---|
|ThermalGridModel|ThermalPowerFlow|LinearThermalGrid|
|[Class]|uses Solution|Model|
||[Class]|[Class]|
|||uses|
||ThermalGrid|ThermalGrid|
||DLMPResults|OperationResults|
||[Class] thermal_grid_models [Module]|[Class]|

Figure 5.8: Code view of the thermal grid models module.
 •Thermal power flow solution algorithm in ThermalPowerFlowSolution.
- Linear thermal grid models in LinearThermalGridModel, LinearThermalGridModel Global and LinearThermalGridModelLocal.
- Thermal grid operation problem results in ThermalGridOperationResults and ThermalGridDLMPResults.
The ThermalGridModel class implements the fundamental thermal grid model consisting of index sets for nodes, branches and DERs in the thermal grid as well as branch parameter and mapping matrices. Based on this, the ThermalPowerFlowSolution implements the thermal power flow solution algorithm for the thermal grid. Note that the distinction into base classes and detail classes is omitted due to the lack of differentiation the thermal grid models but a structure similar to the electric_grid_models module may be introduced at a later point.

The LinearThermalGridModel class implements the base for linear thermal grid models, where the expected sensitivity matrices of the linear grid model are declared along with the methods define_optimization_variables, define_optimization_constraints and define_optimization_objective to define variables, constraints and objective for an optimal operation problem based on the linear grid model. The linear model base class is extended in LinearThermalGridModelGlobal and LinearThermalGridModelLocal with the mathematical definitions for the sensitivity matrices based on the global and local approximation methods.

The results container classes ThermalGridOperationResults and ThermalGridDLMPRes ults encapsulate the output from get_optimization_results and get_optimization_d lmps. To this end, the container classes declare a standardized interface for results data. Similar to the results classes in the electric_grid_models module, this addresses the software quality attribute for modifiability.

##### DER models module

The der_models module (fig.5.8) implements the following functionality:

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
**FlexibleDERModel FexibleLoadModel** extends [Class] [Class] **DERModel** extends [Class] **FlexibleGenerator** **FixedDERModel** **Model** [Class] [Class] uses extends

**make_der_model() FixedLoadModel StorageModel** [Function] [Class] [Class]

uses **FixedGenerator** **DERModelSet CoolingPlantModel** **Model** [Class] [Class] [Class] uses **DERModelSet FixedEVCharger** **HeatingPlantModel** **OperationResults Model** [Class] [Class] [Class]

**FlexibleBuilding** **Model** [Class] **der_models** [Module] uses

**cobmo** [Software system]

Figure 5.9: Code view of the DER models module.

•Fundamental DER models in DERModel, FixedDERModel and FlexibleDERModel.

- Various fixed DER models in FixedLoadModel, FixedGeneratorModel, FixedEVCha rgerModel.
- Various flexible DER models in FlexibleLoadModel, FlexibleGeneratorModel, St orageModel, CoolingPlantModel, HeatingPlantModel, FlexibleBuildingModel.
##### •DER model set in DERModelSet.

##### •DER operation problem results in DERModelSetOperationResults.

•Factory function for DER model objects in make_der_model().

The DERModel class serves as an abstract base class for DER models, which declares fun- damentally expected model variables, such as nominal power time series or grid connection indicators. The classes FixedDERModel and FlexibleDERModel are abstract base classes that extend DERModel with variable declarations that are distinct for fixed or flexible DER models. These classes also implement the methods define_optimization_variables, define_optimization_constraints and define_optimization_objective to define

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
**models** [Module]

uses

|NominalOperation|OptimalOperation|Results|
|---|---|---|
|Problem|Problem|[Class]|
|[Class]|[Class]||
||problems [Module]|uses|

Figure 5.10: Code view of the problems module.

variables, constraints and objective for an optimal operation problem based on the linear grid model. Further, the base classes implement get_optimization_results to obtain the results after the optimization problem was solved.

The concrete mathematical model definitions for fixed DER models are implemented in FixedLoadModel, FixedGeneratorModel, FixedEVChargerModel, which respectively extend FixedDERModel. The corresponding model definitions for flexible DER models are implemented in FlexibleLoadModel, FlexibleGeneratorModel, StorageModel, CoolingPlantModel, HeatingPlantModel, FlexibleBuildingModel, which respectively extend FixedDERModel. Note that this listing represents the currently implemented DER models at the time of writing but MESMO may be augmented with other model types in the future. To this end, the definition of base classes in DERModel, FixedDERModel and FlexibleDERModel addresses the modifiability software quality attribute, as it defines a standardized interface for custom DER model implementations.

The class DERModelSet implements a container class for all DER models of a MESMO scenario. To this end, all DER models of a MESMO scenario are loaded upon initialization of the DERModelSet. Further, the class implements wrapper methods for define_optimizatio n_variables, define_optimization_constraints, define_optimization_objective and get_optimization_results. This class relies on the factory function make_der_model () to create the relevant DER models. Note that the DER initialization is parallelized through starmap() from the utils module.

##### Problems module

The problems module (fig.5.10) implements the following functionality:

##### •Nominal operation problem in NominalOperationProblem.

##### •Optimal operation problem in OptimalOperationProblem.

##### •Results container class in Results.

<u>5. Software architecture of MESMO 5.2. Software architecture</u>

|||database.sqlite|
|---|---|---|
|Researcher||[Data store]|
|[Person]|||
|NominalOperation Problem|loads ElectricGridModel|loads ElectricGridData|
|[Object]|[Object]|[Object]|

reads

|||DERModelSet|DERData|
|---|---|---|---|
|||[Object]|[Object]|
||||uses|
|solve()|uses|||
|[Method]|loads|PowerFlowSolution [Object]|DERModel [Object]|

has loads

|get_results()|uses|||
|---|---|---|---|
|[Method]|returns|||
|save()||Results|Results files (*.csv)|
|[Method]|has|[Object] writes|[Data store]|

Figure 5.11: Workflow diagram of the nominal operation problems.

The classes NominalOperationProblem and OptimalOperationProblem define the setup workflow for nominal and optimal operation problems. Further, these classes implement the methods solve() for solving the problem and get_results() for obtaining the solutions. The concrete workflow structures for nominal and optimal operation problems are highlighted below in section5.2.3.

The results container class Results declares the expected results variables for operation problems. To this end, this class inherits from the individual model results classes Electric GridOperationResults, ElectricGridDLMPResults, ThermalGridOperationResults, ThermalGridDLMPResults and DERModelSetOperationResults. As discussed for the results classes in the electric_grid_models module, this addresses the software quality attribute for modifiability.

##### 5.2.3 Workflow structures

##### Nominal operation problem

The nominal operation problem is a simulation problem of the electric grid, thermal grid and DERs. The workflow diagram for an exemplary nominal operation problem is depicted in fig.5.11. In this example, the thermal grid is not considered for the sake of brevity. For the

<u>5. Software architecture of MESMO 5.2. Software architecture</u> purpose of this documentation, the researcher is assumed to control the workflow within a read-eval-print loop (REPL), i.e. successively executing statements in the command line. The workflow begins with the researcher creating an object of the NominalOperationProb lem class. In the initialization routine of this object, the child objects ElectricGridModel and DERModelSet are created. In turn, the initialization routine of ElectricGridModel loads an ElectricGridData object, whereas DERModelSet loads an DERData object. The data objects respectively establish a connection to database.sqlite through connect_d atabase() and then obtain the relevant data items. In ElectricGridModel, the index sets and model matrices are then defined based on the obtained data. In DERModelSet all DER models for the current scenario are created through make_der_model(), thereby loading multiple DERModel objects. Once the initialization routine is completed, control is returned to the researcher. The researcher then calls the solve() method of the NominalOperationProblem object. This method first obtains the nominal power time series for each DER in the DERModelSet. Then, based on the DER nominal power vector for each time step as well as the ElectricGr idModel, the solve() method obtains a PowerFlowSolution for each time step. Internally, this is handled through the starmap() function, as the power flow solution for each time step can be calculated independently and thus in parallel. The power flow solutions are stored within the NominalOperationProblem object and then control is returned to the researcher. Next, the researcher calls the get_results() method of the NominalOperationProblem object. This method transforms the results from the PowerFlowSolution objects into the results variables expected in the Results object, which is then created by passing the relevant variables into the container. Eventually, the get_results() method returns the Results object to the researcher. In the last step, the researcher may save the results to the file system through the save() method of the Results object.
##### Optimal operation problem

The optimal operation problem is a numerical optimization problem of the district-scale electric grid, thermal grid and DERs. The workflow diagram for an exemplary nominal operation problem is depicted in fig.5.12. Similar to the nominal operation problem workflow above, the thermal grid is not considered for the sake of brevity and the researcher is assumed to control the workflow within a read-eval-print loop (REPL), i.e. successively executing statements in the command line.

The researcher begins the workflow by creating an object of the OptimalOperationProblem class. In its initialization routine, the OptimalOperationProblem creates child objects of the ElectricGridModel, GlobalLinearElectricGridModel and DERModelSet classes. To begin, the ElectricGridModel loads an ElectricGridData object, which establishes a connection to database.sqlite through connect_database() and obtains the relevant data items. In ElectricGridModel, the index sets and model matrices are then defined

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
**database.sqlite** **Researcher** [Data store]

|Researcher|||[Data store]|
|---|---|---|---|
|[Person]||||
|OptimalOperation Problem|ElectricGridModel|loads ElectricGridData||
|[Object]|[Object] uses|uses|[Object]|
||LinearElectricGrid|PowerFlowSolution||
||Model [Object]|loads|[Object]|

[Person] reads

loads

**DERModelSet DERData** loads [Object] [Object]

has uses

**define_optimization** **DERModel** **_constraints()** [Object] [Method] has

**define_optimization** **_objective()** [Method]

**define_optimization** **_variables()** [Method]

**Optimization** **Problem** uses [Object]

has

**solve() solve()** calls [Method] [Method]

|get_results()|calls|get_optimization||
|---|---|---|---|
|[Method]|returns|_results() [Method]||
|save()||Results|Results files (*.csv)|
|[Method]|has|[Object] writes|[Data store]|

Figure 5.12: Workflow diagram of the optimal operation problems.

based on the obtained data. Based on this, the GlobalLinearElectricGridModel is

<u>5. Software architecture of MESMO 5.2. Software architecture</u> instantiated based on the index sets and model matrices of the ElectricGridModel object. Furthermore, a PowerFlowSolution object is loaded for the nominal loading conditions of the electric grid, which is required as a reference point for the global approximation method according to section6.3.2. Note that GlobalLinearElectricGridModel is utilized here instead of LinearElectricGridModel, which is the abstract parent class that only implements the model interface / structure but not the actual mathematical model formulation. Lastly, in DERModelSet all DER models for the current scenario are created through make_der_model(), thereby loading multiple DERModel objects. Furthermore, the initialization routine of the OptimalOperationProblem creates an object of the OptimizationProblem class. This object serves as a container for the mathematical definitions of the numerical optimization problem, i.e. its variables, constraints and objective definition. To this end, the OptimizationProblem class provides the necessary abstractions to enable a solver-agnostic problem definition. Continuing, the initialization routine of the OptimalOperationProblem defines the variables, constraints and objectives of the optimal operation problems. In this regard, the architecture of MESMO is structured such that variables, constraints and objective are implemented through methods within the respective model classes. This addresses the quality attributes for modifiability and modularity of the software. It ensures that 1) model interface changes are kept coherent with the optimization problem definitions and 2) variables, constraints and objective definitions can be obtained for each model individually. Therefore, the OptimalOperationProblem iterates through the methods define_optimization_variables(), define_optimization_constraints() and define_optimization_objective() of LinearElectricGridModel and DERModelSe t, where the OptimizationProblem object is passed to each method in order to attach the variables, constraints and objective definitions. Once the initialization routine is completed, control is returned to the researcher. The researcher then calls the solve() method of the OptimalOperationProblem object. This method calls the solve() method of the OptimizationProblem object, which in turn passes the optimization problem definition to the solver interface. It invokes the external optimization solver to obtain the solution. Next, the researcher calls the get_results() method of the OptimalOperationProblem object. This method obtains the results for all model variables by invoking the get_optim ization_results() methods of the LinearElectricGridModel and DERModelSet. The results are then transformed into the results variable structures which are expected in the Results object, which is then created by passing the relevant variables into the container. Eventually, the get_results() method returns the Results object to the researcher.
##### 5.2.4 Allocation structures

##### Dependencies

In principle, MESMO’s software architecture presented in sections5.2.2and5.2.3can be implemented in any software environment or programming language. Nevertheless, the choice of dependencies is influenced by some the functional requirements and quality

<u>5. Software architecture of MESMO 5.2. Software architecture</u>

|MESMO|||
|---|---|---|
|[Software system]||implemented in|
|der_models|uses|cobmo|
|[Module]|[Software system]||

**electric_grid** **OpenDSSDirect.py** **_models** uses [Software system] [Module]

reads/ **data_interface sqlite3** uses writes [Module] [Software system] **Database** [Data store] **(database.sqlite)** has **Python** **plots plotly** [Language] uses [Module] [Software system]

uses uses

**dashboard dash** serves uses [GUI] [Module] [Software system] **eb application** **W**

**utils cvxpy** uses [Module] [Software system]

uses

**Numerical solver** **(Gurobi, CPLEX, ...)** [Software system]

Figure 5.13: Container view of MESMO, highlighting the external software dependencies.

attributes from sections5.1.3and5.1.4. To this end, the container view in fig.5.13highlights the main dependencies of the current implementation of MESMO.

The primary programming language of MESMO is Python, such that all modules in fig.5.3 are implemented in this language. The following considerations have contributed to this choice of programming language:

- Python, along with MATLAB and C++ is commonly used among researchers in energy engineering. Therefore, the choice for this language enables researchers to readily in- tegrate MESMO with their existing modeling workflows. Furthermore, existing modeling efforts could be utilized in MESMO, such as the building modeling toolbox CoBMo [45].
- In Python, there is a rich environment of libraries for convex optimization and plotting and dashboarding applications. The former ensures that MESMO does not need to implement low-level solver interfaces. In contrast, the later ensures a future-facing development with the need for high-level user interfaces in mind.
71

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
- Since Python and most of its libraries are available free and open source, this ensures accessibility of MESMO, which is also intended for open-source distribution for the benefit of stakeholders in the research domain.
The above points mainly address interoperability ASRs. However, a drawback of choice for Python over C++ or Julia is the performance disadvantages that are associated with language. This trade-off is tolerated in the context of MESMO because the interoperability ASRs are slightly more important than the performance ASRs according to section4.2.3.

The further dependencies of MESMO are all Python packages, which ensures straightforward dependency management through the Python setup and package management facilities. On the modeling side, MESMO utilizes the cobmo and OpenDSSDirect.py, where cobmo implements the underlying mathematical models for FlexibleBuildingModel and Open DSSDirect.py serves as an interface to OpenDSS [20] in ElectricGridModelOpenDSS as well as PowerFlowSolutionOpenDSS. The sqlite3 provides low-level interfaces for interacting with the internal SQLITE database, i.e. database.sqlite. The packages plotly and dash provide plotting and dashboarding functionalities, where dash will serve the future implementation of a web-based GUI out of MESMO. Lastly, cvxpy implements a convex optimization problem modeling framework and interfaces to various open-source and commercial solvers [18].

##### Repository structure

MESMO is intended as a software system that is deployed to individual workstations akin to a traditional desktop application, where all data and dependencies are kept local. In line with this, the components of MESMO are fully contained within a single software repository. The repository structure, i.e. file structure, of MESMO follows the recommended Python package structure from [154] as depicted in fig.5.14. The repository is implemented as a Git repository [155] for version control and at the time of writing is hosted at GitHub³.

The main code base of the MESMO Python package is contained within the mesmo directory. The file __init__.py simply contains import statements for the individual modules, such that all modules are loaded when importing MESMO. The remaining Python files in the mesmo directory represent the modules from fig.5.3, where Python interprets the file names as module names. Additionally, this directory contains the default configuration parameters in config_default.yml and the database_schema.sql file, which contains declarations for the data-structure of the internal SQL database, i.e. database.sqlite. In principle, the mesmo directory only contains code and declarative information but strictly no scenario or model data definitions or custom execution scripts.

The scenario and model data are contained within the data directory. This directory consists of CSV files in MESMO data format⁴, which define example test case scenario data. The CSV files are organized into sub-directories for the individual test cases. The data directory 3 [https://purl.org/mesmo/repository](https://purl.org/mesmo/repository) 4 [https://purl.org/mesmo/docs/0.5.0/data_reference.html](https://purl.org/mesmo/docs/0.5.0/data_reference.html)

<u>5. Software architecture of MESMO 5.2. Software architecture</u>
**MESMO Repository**

**.github**

**cobmo cobmo** [Software system] **Input files Database data** [Data store] [Data store]

**docs**

**examples**

**MESMO mesmo** [Software system]

**__init__.py**

**api api.py** [Module] **config config.py** [Module] **config_default.yml config_default.yml** [Data store] **data_interface data_interface.py** [Module]

**data_schema.sql**

**der_models der_models.py** [Module] **electric_grid_ electric_grid_models.py** **models**[Module] **plots plots.py** [Module] **problems problems.py** [Module] **thermal_grid_ thermal_grid_model.py** **models**[Module] **utils utils.py** [Module] **Results files results** [Data store]

**tests**

**config.yml config.yml** [Data store]

**...**

**setup.py**

Figure 5.14: Repository structure of MESMO.

<u>5. Software architecture of MESMO 5.2. Software architecture</u> further contains the database.sqlite file for the internal database in SQLITE format, which is created locally upon first run of MESMO and initially will contain the example test case definitions from the CSV files. The docs directory contains the software documentation for MESMO, which is based on the Sphinx documentation builder [156]. The directory contains markdown (MD) files for each section of the documentation and Sphinx configuration files and other assets of the documentation. At the time of writing, the documentation is automatically built via GitHub Actions and deployed to GitHub Pages whenever changes are pushed to the repository. Consequently, the documentation is made available for users online in HTML format⁵. The examples directory contains example run scripts, which demonstrate typical use cases of MESMO. This directory and online documentation are intended as the main entry point for new users. Therefore, these examples are highly commented and serve as templates for custom applications utilizing the MESMO high-level and low-level interfaces. For developers, the examples directory contains a development sub-directory intended for work-in-progress scripts relating to the implementation of new features in MESMO. Results data items of an example run scripts are by default stored into the results directory. This directory is provided for convenience to keep all MESMO-related data within a single location. The Git repository is configured to ignore any files in this directory, such that results are local-only and are not committed to the main repository. The test directory contains unit tests for the classes and functions of all modules. Although MESMO does not strictly follow test-driven development [157], unit tests are an important tool for collaborative development because they help reveal if code changes impact other functionalities in unexpected. To this end, the test directory contains one unit test script for each module of MESMO. The unit tests are automatically executed through GitHub Actions whenever changes are pushed to the repository and alerts to developers are triggered on test failures. The aforementioned automations with GitHub Actions for documentation and tests are configured in the .github directory. In addition, the workflows sub-directory contains one YAML file in GitHub Actions format for each automation workflow. The top-level repository folder contains several configuration and supplementary files. The file config.yml is the counterpart of config_default.yml and contains custom user- defined configuration parameters. This file is intended for local changes to the MESMO configuration. e.g. choice of optimization solver, and the Git repository is configured to ignore this file, such that it is not committed to the main repository. Finally, the file setup.py defines installation routines and external package dependencies of MESMO, including references to the dependencies from fig.5.13. The CoBMo toolbox is included as a Git submodule [155, p. 305, Section 7.11] in the cobmo directory. This approach is chosen to allow for integrated development of CoBMo alongside 5 [https://purl.org/mesmo/docs/0.5.0](https://purl.org/mesmo/docs/0.5.0)
74

<u>5. Software architecture of MESMO 5.2. Software architecture</u> MESMO. At the time of writing, CoBMo also has not been released to any Python package index and thus could not integrated through setup.py as another external dependency. A few top-level files have been excluded in fig.5.14for the sake of brevity: README.md and LICENSE contain descriptive information for the repository and licensing information for its distribution. The .gitignore and .gitmodules files contain configuration definitions for the
6,7 Git repository. The file environment.yml defines an alternative installation routine.

##### Version control

For the development of MESMO, Git [155] is utilized as version control system (VCS) for the code repository, which at the time of writing is hosted at GitHub⁸. The management of branches in the Git repository is based on the git-flow principle from [158]. To this end, the repository contains the following branches:

- The **master** branch contains stable release versions of the repository. Changes to the master branch are only made when 1) fixing a critical bug or 2) publishing a new release. Only administrators of the repository can send and merge pull requests to this branch.
- The **develop** branch is intended as the main branch for development, i.e. always containing the latest code base. The develop branch will thus contain the latest changes which have not yet been thoroughly tested and released to the master branch. Anyone can send pull requests to develop, which will then be merged by administrators.
- Multiple **feature** branches can be created to develop new features simultaneously. The idea is to keep unstable development or improvement works separate from the main develop branch. Once the work is complete, a pull request is created for the feature branch to be merged into the develop branch.
Every time the master branch changes, a new version number is defined according to the semantic versioning principle [159]:

1. New releases cause a changing version number in the first digit for major changes and in the second digit for minor changes (e.g. from 0.1.1 to 0.2.0).
2.Bug fixes cause a changing version number in the third digit (e.g. from 0.1.1 to 0.1.2).
6 [https://purl.org/mesmo/docs/0.5.0/getting_started.html#alternative-installation](https://purl.org/mesmo/docs/0.5.0/getting_started.html#alternative-installation) 7 [https://purl.org/mesmo/docs/0.5.0/contributing.html#updating-environment-yml](https://purl.org/mesmo/docs/0.5.0/contributing.html#updating-environment-yml) 8 [https://purl.org/mesmo/repository](https://purl.org/mesmo/repository)

## 6 Electric grid modeling

#### Contents

6.1 Fundamental electric grid model......................... 77
6.1.1 Scope and assumptions......................... 77

6.1.1 Scope and assumptions..	77
6.1.2 Single-phase power flow..	77
6.1.3 Three-phase power flow....	80
6.1.4 Multi-phase power flow...	84
6.1.5 Line admittance model.....	86
6.1.6 Transformer admittance model...	87
6.1.7 DER connection...	88
6.1.8 Source connection...	89
6.1.9 Source and no-source notation....	89
6.2 Non-linear power flow solution.....	90
6.2.1 Outline...	90
6.2.2 Fixed-point method.	91
6.3 Linear approximate model...	92
6.3.1 Fundamental linear model...	92
6.3.2 Global approximation.	94

.....

**Outline and contributions**

This chapter first introduces fundamental power flow formulations for the electric grid along with a solution algorithm for the non-linear power flow problem.Secondly, a method for obtaining a linear approximate grid model is presented. The former is utilized for the nominal operation problem formulation, whereas the latter is a prerequisite for defining the convex optimal operation problem.

The fundamental modeling methodologies presented in this chapter are derived from [11], [31]–[33]. However, the model formulation has been redeveloped for this thesis to present a more consistent description than previous works. The non-linear power flow solution and the linear approximate modeling are based on the works [11], [34] and have only been restated and corrected in this thesis.

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u>
#### 6.1 Fundamental electric grid model

##### 6.1.1 Scope and assumptions

The focus of electric grid modeling in the context of MESMO is to express the state variables of the electric grid as a function of the input variables. To this end, the electric grid is abstracted to nodes and branches, where nodes refer to vertices, i.e. interconnection points of DERs and branches, and branches refer to edges, i.e. power delivery elements such as lines or transformers.

The following includes only steady-state properties because transient electric grid states are currently excluded from the scope of MESMO. Furthermore, the electric grid modeling is restricted to three-phase alternating current (AC) systems. Specifically, direct current (DC) systems are currently not considered in MESMO.

##### The considered state variables are:

•Nodal voltage vector *u* *f t* •Branch power flow vector in “from” and “to” direction *s, s* *ls ls* •Active and reactive power losses *p,q*

The “from” and “to” directions are defined according to fig.6.1and section6.1.2. Note that “from” and “to” are represented as directions 1 and 2 in the MESMO implementation.

##### The considered input variables are:

- DER power injection vector *s*, which is decomposable into active power *p* and reactive power *q* as *s* = *p* + *jq*
This assumes that all DERs can be described with PQ models, i.e. all DERs act as constant power sources or loads. A future extension to a more general ZIP model, i.e. DERs with constant-power, constant-current, and constant-impedance portions, is possible on the basis of [32], [61]. DERs can be modeled as wye-connected or delta-connected according to section6.1.7.

The fundamental electric grid model is first formulated based on the single-phase power flow in section6.1.2. Then, extensions for the three-phase and multi-phase power flow are progressively introduced in sections6.1.3and6.1.4.

##### 6.1.2 Single-phase power flow

As a starting point, consider the single-phase electric power flow across the branch (1*,*2) between two nodes 1 and 2 of the electric grid according to fig.6.1. The branch flows can be expressed as:

*f f t t* *s₁* = *u₁i₁ s₁,*2= *u₂i₁* (6.1a) *,*2*,*2*,*2

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u>
Figure 6.1: Single-phase power flow between two nodes of the electric grid.

<u>y</u> *sh* <u>y</u> *sh* *f* <u>1,2</u> *se t* <u>1,2</u> *se*

|i₁ =|(u₁ − u₂) u₁ + y₁|= i₁|u₂ + y₁|(u₂ − u₁)||(6.1b)|
|---|---|---|---|---|---|---|
|,2|,2|,2||,2|||
|f|f||||||
|,2|,2|t1,2|t1,2||se|sh|
||||||,2|,2|

*,*2*,*2*,*2*,*2 2 2

The scalars *s₁* and *i₁* denote the complex power and current flowing in “from”-direction from node 1 into branch (1*,*2). Consequently, *s* and *i* denote the complex power and current flowing in “to”-direction from node 2 into branch (1*,*2), i.e. towards node 1. This formulation adopts the *π*-model for the branch (1*,*2), where the scalars *y₁* and *y₁* are the complex series and shunt admittance. The *π*-model can be utilized to represent both lines or transformers as branches, where definitions follow in sections6.1.5and6.1.6.

The relation between nodal injections and branch flows is derived from the power balance of each node as:

*s₁* = *u₁i₁ s₂* = *u₂i₂* (6.2a) *f t t f* *i₁* = *i₁* *,*2 + *i₀,*1*i₂* = *i₁,*2+ *i₂* *,*3 (6.2b)

Here, the scalars *i₁,s₁* and *i₂,s₂* denote the complex current and power injections at node 1 and 2, respectively. Note that injections can represent both generation, i.e. when its value takes a positive sign, and load, i.e. when its value takes a negative sign.

Additionally, the complex power loss *s* *ls* 1*,*2due to the power flow at branch (1*,*2) can be expressed as:

||||ls|f t|f|t|||
|---|---|---|---|---|---|---|---|---|
||||,2|,2 ,2|,2|,2|||
|||el|||||||
|f b|f n b|||tb n|tb|||el|
|f|bsh|||tb bsh||||el|
|b|n|bse n|n||n bse|n|n||

*s₁* = *s₁* + *s₁* = *u₁i₁* + *u₂i₁* (6.3a)

As the next step, the power flow eqs. (6.1) to (6.3) can be generalized for all nodes *n ∈N* *el* and branches *b ∈B* as:

*s* = *u f i s* = *u t i ∀b ∈B* (6.4a) *b b* <u>y y</u> *i* = *u f* + *y u f − u t i* = *u t* + *y u t − u f ∀b ∈B* (6.4b) 2 *b b b*2*b b b*

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u> *sn*= *unin∀n ∈N*
*el* (6.4c) X X *f tb el* *i* *n*= *ib*+ *i ∀n ∈N* (6.4d) *b∈Bn* *el,f* *b∈Bn* *el,t* X *ls f tb* *s* = *u* *n* *f i* *b* + *unt i* (6.4e) *el* *b b* *b∈B*

*f tb* The indices *n* *b* and *n* denote the nodes at “from” and “to” ends of branch *b*. The symbols *el,f el,t* *Bn*and *Bn*are the sets of all branches connecting to node *n* in “from” and “to” direction. Note that the scalar *s* *ls* describes the total complex power loss at all branches but not at individual branches. Further, note that eq. (6.4b) can be substituted in eqs. (6.4d) and (6.4e) as:

X <u>y</u>*sh*X *ysh* *i* *n*= <u>b</u> *u* *n* *f* + *ybseu* *n* *f − unt* + *b* *unt* + *ybseunt − u* *n* *f ∀n ∈N* *el* *el,f* 2 *b b b* *el,t* 2*b b b* *b∈Bnb∈Bn* (6.5a) ! X <u>y₁</u>*sh* <u>,2</u> <u>y₁</u> *sh* <u>,2</u> *s* *ls* = *u* *n* *f u* *n* *f* + *u* *n* *f y₁* *se* *,*2 *u* *n* *f − unt* + *unt unt* + *unt y₁* *se* *,*2 *unt − u* *n* *f* *el* *b* 2 *b b b b b*2*b b b b* *b∈B* (6.5b)

Then, the power flow eqs. (6.4) and (6.5) can be transformed into a vectorized notation as:

|f|f f|t|t t|
|---|---|---|---|
|f f||t t||

*s* = diag *A u i s* = diag *A u i* (6.6a)

*i* = *Y u i* = *Y u* (6.6b)

*s* = diag (*u*) *i* (6.6c) *i* = *Yu* (6.6d)

*s* *ls* = *u* ⊺ *Y u* (6.6e)

*el el*

|f|f B ×1|t t|B ×1||||
|---|---|---|---|---|---|---|
|||||N ×1|||
||||N ×1||||
|N ×N||||f t|B ×N f t|B ×N|

The vectors *s, i ∈* C and *s, i ∈* C denote the branch power and branch power *el* vectors in “from” and “to” direction. The vectors *i, s ∈* C are the nodal complex current *el* and power injection vectors, whereas *u ∈* C is the nodal voltage vector. The matrix *el el el el* *Y ∈* C is the nodal admittance matrix and *Y, Y ∈* C are the branch *el el* admittance matrices in “from” and “to” direction. The matrices *A, A ∈* R denote the branch incidence matrices in “from” and “to” direction. Note that the compact form of the nodal current eq. (6.6d) is derived from:

*i* = *A* *f* *i* *f* + *A* *t* *i* *t* *Y* = *A* *f* *Y* *f* + *A* *t* *Y* *t* (6.7a)

The corresponding vectors are defined as: h i h i *f/t f/t f/t f/t* *s* = *s* *b* *i* = *i* *b* (6.8a) *b∈Belb∈Bel*

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u>
*s* = [*sn*] *n∈Nel* *i* = [*in*] *n∈Nel* *u* = [*un*] *n∈Nel* (6.8b)

Further, the definition of the matrices follows from eqs. (6.4) and (6.5) as: ( h i 1 for *n* = *n* *f/t* *f/t f/t f/t b* *A* = *a* *b,n* *a* *b,n* = (6.9a) (*b,n*)*∈Bel×Nel*0 otherwise  *sh*   <u>y</u> <u>b</u> *se f/t* h i   2 + *yb*for *n* = *n* *b* *f/t f/t f/t* *Y* = *y* *b,n* *y* *b,n* =*se t/f*(6.9b) (*b,n*)*∈Bel×Nel* *− yb*for *n* = *n* *b*   0 otherwise  *sh*   X <u>y</u> <u>b</u> *se*   + *yb*for *n* = *m*  2 *b∈Bnel* *Y* = [*yn,m*] (*n,m*)*∈Nel×Nel* *yn,m*= X (6.9c)  *se*   *−yb*otherwise  *b∈Bnel∩Bm el*

Here, the symbol *Bn* *el* denotes the set of all branches connected to node *n*, where *Bn* *el* = *el,f el,t* *Bn∪Bn*.

Equations (6.6), (6.8) and (6.9) define the complete single-phase power flow formulation for the electric grid. Note that this formulation is restricted to single-phase analysis, which assumes DER power injections to be perfectly balanced accross all three phases of the AC system. Further, the formulation does not apply to multi-phase grid configurations, i.e. mixed three-phase, two-phase and / or single-phase sections within the same grid. However, the presented formulation forms an important basis for the following three-phase and multi-phase considerations.

##### 6.1.3 Three-phase power flow

The single-phase power flow formulation from section6.1.2can be transformed for three- phase grid configurations through a few extensions. First, consider the three-phase example in fig.6.2. Compared to the single-phase example, the nodes 1 and 2 are split up for the three phases *a*, *b* and *c*. Further, for branch (1*,*2), which is also split up for the three phases, the *π*-model considers three-phase element matrices for the series admittance *Y₁* *se* *,*2and shunt admittance *Y₁* *sh* *,*2. In these three-phase element admittance matrices, the diagonal entries are the self-admittance values of each phase similar to the single-phase admittance, whereas the off-diagonal entries are the mutual admittance values, which describe the inductive / capacitive coupling of different phases. Please refer to sections6.1.5and6.1.6for the derivation of element admittance matrices for lines and transformers.

For notational convenience, the three-phase power flow properties can be collected into three-phase vectors, where the symbol *P* denotes the set of all phases *P* = *{a,b,c}*: h i h i *f/t f/t,p f/t f/t,p* *s* *b* = *s* *b* *i* *b* = *i* *b* (6.10a) *p∈P p∈P*

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u>
Figure 6.2: Three-phase power flow between two nodes of the electric grid.

*p p p* *sn*= [*sn*]*p∈Pin*= [*in*]*p∈Pun*= [*un*]*p∈P*(6.10b)

|f/t f/t|3×1|||
|---|---|---|---|
|b b n n n ×1|×1|||

The vectors *s, i ∈* C are the complex branch power and current in from / to direction. The vectors *s, i ∈* C³ denote the complex nodal power and current injections. Lastly, the vector *u ∈* C³ is the complex nodal voltage.

The branch power flow expression follows as:

*f f t t* (6.11a)

|s₁ = diag (u₁) i₁|||s₁ = diag (u₂) i₁|||
|---|---|---|---|---|---|
|,2||,2|,2||,2|
|f|1sh ,2|se|t|1sh ,2|se|
|,2||,2|,2||,2|

*,*2*,*2*,*2*,*2 <u>Y Y</u> *i₁* = *u₁* + *Y₁* (*u₁ − u₂*) *i₁* = *u₂* + *Y₁* (*u₂ − u₁*) (6.11b) 2 2

Correspondingly, the relation between nodal injections and branch flows is expressed as:

*s₁* = diag (*u₁*)*i₁ s₂* = diag (*u₂*)*i₂* (6.12a)

|f t||||t f|
|---|---|---|---|---|
|,2 ls 1,2|,1|||,2 ,3|
|ls|⊺ f|⊺ t|⊺ f|⊺ t|
|,2|,2|,2|,2|,2|

*i₁* = *i₁* + *i₀ i₂* = *i₁* + *i₂* (6.12b)

The complex power loss *s* at branch (1*,*2) can be expressed as:

*s₁* = 1 *s₁* + 1 *s₁* = *u₁i₁* + *u₂i₁* (6.13a)

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u> Equations (6.11) and (6.12) can be generalized for all nodes similar to section6.1.2, eqs. (6.4) and (6.5). Consequently, the generalized and vectorized three-phase power flow equations are derived as:

|f|f f|t|t t|
|---|---|---|---|
|f f||t t||

*s* = diag *A u i s* = diag *A u i* (6.14a)

*i* = *Y u i* = *Y u* (6.14b)

*s* = diag (*u*) *i* (6.14c) *i* = *Yu* (6.14d) *ls* ⊺

|s = u|Y u||||||(6.14e)|
|---|---|---|---|---|---|---|---|
|f f|3B ×1|t t|3B ×1 3N|×1|3N ×1|||
|3N ×3N|||||f t|3B ×3N f t|3B ×3N|

*el el* The vectors *s, i ∈* C and *s, i ∈* C denote the branch power and branch *el* power vectors in “from” and “to” direction. The vectors *i, s ∈* C are the nodal complex *el* current and power injection vectors, whereas *u ∈* C is the nodal voltage vector. The *el el el el* matrix *Y ∈* C is the nodal admittance matrix and *Y, Y ∈* C are the *el el* branch admittance matrices in “from” and “to” direction. The matrices *A, A ∈* R denote the branch incidence matrices in “from” and “to” direction. The corresponding vectors are defined as: h i h i *f/t f/t f/t f/t* *s* = *s* *b* *i* = *i* *b* (6.15a) *b∈Belb∈Bel* *s* = [*sn*] *n∈Nel* *i* = [*in*] *n∈Nel* *u* = [*un*] *n∈Nel* (6.15b)

Further, the definition of the matrices follows as: ( h i *I ∈* R³ *×*3 for *n* = *n* *f/t* *f/t f/t f/t b* *A* = *A* *b,n* *A* *b,n* = (6.16a) (*b,n*)*∈Bel×Nel*0 *∈* R³*×*3otherwise  *sh*   <u>Y</u> <u>b</u> *se f/t* h i   2 + *Yb*for *n* = *n* *b* *f/t f/t f/t* *Y* = *Y* *b,n* *Y* *b,n* =*se t/f* (6.16b) (*b,n*)*∈Bel×Nel* *− Yb*for *n* = *nb*   0 *∈* R³ *×*3 otherwise  *sh*   X <u>Y</u> <u>b</u> *se*   + *Yb*for *n* = *m*  2 *b∈Bnel* *Y* = [*Yn,m*] (*n,m*)*∈Nel×Nel* *Yn,m*= X (6.16c)  *se*   *−Yb*otherwise  *b∈Bnel∩Bm el*

*f tb el* The indices *n* *b* and *n* denote the nodes at “from” and “to” ends of branch *b* The symbol *Bn* denotes the set of all branches connected to node *n*.

There is an important distinction in the three-phase power flow eqs. (6.14) to (6.16) from the single-phase formulation because the nodal power and current injections *sn, in*do not directly correspond to the DER injections but depend on the interconnection scheme of the DERs with the nodes. To this end, consider that DERs are attached to node *n* through

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u>
Figure 6.3: Three-phase wye and delta connection of DER injections.
 either wye (*Y*) or delta (∆) connection, as depicted in fig.6.3. Note that both wye and delta connection can occur at the same node because multiple DERs with different connection type may coincide. According to Kirchhoff’s laws, the relation of nodal, wye and delta injections is described by the following equations: *a a a a Y,a* ∆*,ca* ∆*,ab Y,a a Y,a* ∆ *a bn* ∆*,ab* *sn*= *unin*= *unin*+ *in− insn*= *uninsn,ab*= *un− u in*(6.17a) *bn bn bn bn Y,b* ∆*,ab* ∆*,bc Y,b bn Y,b* ∆ *bn cn* ∆*,bc* *s* = *u i* = *u in*+ *in− insn*= *u insn,bc*= *u − u in*(6.17b) *cn cn cn cn Y,c* ∆*,bc* ∆*,ca Y,c cn Y,c* ∆ *cn a* ∆*,ca* *s* = *u i* = *u in*+ *in− insn*= *u insn,ca*= (*u − un*) *in*(6.17c) Again, the properties can be collected into three-phase vectors:
*Y Y,p Y Y,p* *sn*= *sn p∈{a,b,c}in*= *in p∈{a,b,c}*(6.18a) ∆ ∆ ∆ ∆ *sn*= *sn,p p∈{ab,bc,ca}in*= *in,p p∈{ab,bc,ca}*(6.18b)

Then, eq. (6.17) can be transformed into vectorized notation, utilizing the delta phase mapping matrix Γ for the delta connections according to [11], [33]:

*Y* ⊺ ∆ *Y Y* ∆ ∆ *el* *sn*= diag (*un*) *in−* Γ *insn*= diag (*un*) *insn*= diag (Γ*un*) *in∀n ∈N*

(6.19a)  

||||
|---|---|---|
|aa|ab|ac|
|ba|bb|bc|
|ca|cb|cc|

Γ Γ Γ 1 *−*1 0 Γ = Γ Γ Γ =0 1 *−*1 (6.19b) Γ Γ Γ *−*1 0 1

The aggregation of eq. (6.19) for all nodes follows as:

*Y* ⊺ ∆ *Y Y* ∆ ∆ *s* = diag (*u*) *i −* (*H*) *i s* = diag (*u*) *i s* = diag (*Hu*) *i* (6.20a)

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u>
Figure 6.4: Multi-phase power flow between two nodes of the electric grid.
   Γ ... 3*Nel×*3*Nel* *H* =   *∈* R (6.20b)
Γ

The matrix *H* denotes the aggregated delta phase mapping matrix.

The complete three-phase power flow is defined by eqs. (6.14) to (6.16) and (6.20). This formulation forms the basis for the following multi-phase power flow considerations.

##### 6.1.4 Multi-phase power flow

Figure6.4depicts an exemplary multi-phase grid configuration, where node 1 is three-phase and node 2 is two-phase, i.e. missing phase *b*. Furthermore, branch (0*,*1) is three-phase, whereas branch (1*,*2) is two-phase in *a,c* and branch (2*,*3) is single-phase in *c*. Accordingly, the series and shunt element admittance matrices for branch (1*,*2) are two-phase, i.e. elements for missing phases are not considered. To account for the missing phases, the set of phases for all nodes *N* *el* and the set of phases for all branches *B* *el* are introduced as:

*N* *el* = *{{*(*n,p*)*}p∈Pn}* *n∈Nel* (6.21a)

*B* *el* = *{{*(*b,p*)*}p∈P* *b* *}* *b∈B* (6.21b)

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u> The symbols *Pn, Pb*denote the set of phases at node *n* and the set of phases at branch *b*, i.e. excluding any missing phases. The symbols *N*
*el* *, B* are the set of all nodes and the set of all branches. Essentially, *N* *el* *, B* *el* contain elements only for those phases which exist for each node and branch, whereas 3*N* *el* *,*3*B* assume exactly 3 phases for each node and branch.

The three-phase power flow eqs. (6.14) to (6.16) and (6.20) can directly be adapted for the multi-phase case with a modified notation based on eq. (6.21) as:

|f|f f|t|t t|
|---|---|---|---|
|f f||t t||

*s* = diag *A u i s* = diag *A u i* (6.22a)

*i* = *Y u i* = *Y u* (6.22b)

*s* = diag (*u*) *i* (6.22c) *i* = *Yu* (6.22d)

*s* *ls* = *u* ⊺ *Y u* (6.22e) *Y* ⊺ ∆ *Y Y* ∆ ∆

|s = diag (u)|i − (H )|i s|= diag (u) i||s|||
|---|---|---|---|---|---|---|---|
|f|f B ×1|t t|B ×1|||||
||||N|×1|N ×1|||
|N ×N|||||f t f|B ×N t B N|×N ×N|

= diag (*Hu*) *i* (6.22f)

*el el* The vectors *s, i ∈* C and *s, i ∈* C denote the branch power and branch power *el* vectors in “from” and “to” direction. The vectors *i, s ∈* C are the nodal complex current *el* and power injection vectors, whereas *u ∈* C is the nodal voltage vector. The matrix *el el el el* *Y ∈* C is the nodal admittance matrix and *Y, Y ∈* C are the branch *el el* admittance matrices in “from” and “to” direction. The matrices *A, A ∈* R denote the *el el* branch incidence matrices in “from” and “to” direction. The matrix *H ∈* R denotes the aggregated delta phase mapping matrix. The corresponding vectors are defined as: h i h i *f/t f/t,p f/t f/t,p* *s* = *s* *bel* *i* = *i* *bel* (6.23a) (*b,p*)*∈B* (*b,p*)*∈B* *s* = [*s* *p* *n*](*n,p*)*∈Nel i* = [*i* *p* *n*](*n,p*)*∈Nel u* = [*u* *p* *n*](*n,p*)*∈Nel* (6.23b) h i h i *s* *Y/*∆ = *s* *Y/* *n* ∆*,p* *el* *i* *Y/*∆ = *i* *Y/* *n* ∆*,p* *el* (6.23c) (*n,p*)*∈N* (*n,p*)*∈N* (6.23d)

Further, the definition of the matrices follows as: h i *f/t f/t* *A* = *a* (*b,pb*)*,*(*n,pn*) *el el* (6.24a) ((*b,pb*)*,*(*n,pn*))*∈B ×N* ( *f/t n b* *f/t*1 for *n* = *nb*and *p* = *p* *a* (*b,pb*)*,*(*n,pn*) = (6.24b) 0 otherwise h i *f/t f/t* *Y* = *y* (*b,pb*)*,*(*n,pn*) *el el* (6.24c) ((*b,pb*)*,*(*n,pn*))*∈B ×N*  *b n*   <u>y</u> *sh,p p* *b n*   <u>b</u> + *y* *se,p p* for *n* = *n* *f/t* and *p* *n* *∈P* *b b b* *f/t*2 *y* (*b,pb*)*,*(*n,pn*) = *se,pbpnt/f n* (6.24d)   *− y* for *n* = *n* and *p ∈Pb*   *b b*  0 otherwise

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u> *Y* = *y*(*n,pn*)*,*(*m,pm*)
((*n,pn*)*,*(*m,pm*))*∈Nel×Nel* (6.24e)  *sh,pnpm* !   X <u>y</u> <u>b</u> *se,p* *npm*   + *yb*for *n* = *m*  2 *y*(*n,pn*)*,*(*m,pm*)= *b∈Bn,p* X *n* (6.24f)  *se,p* *npm*   *−yb*otherwise  *b∈Bn,pn∩Bm,pm* h i *H* = *a* ∆ (*n,pn*)*,*(*m,pm*) (6.24g) ((*n,pn*)*,*(*m,pm*))*∈Nel×Nel* ( *n m* ∆ Γ *p p* for *n* = *m* *a* (*n,pn*)*,*(*m,pm*) = (6.24h) 0 otherwise

*f tb* The indices *n* *b* and *n* denote the nodes at “from” and “to” ends of branch *b*. The symbol *Pb* describes the set of all phases at branch *b*. The symbol *Bn,p*denotes the set of all branches connected to node *n* at phase *p*. Note that Γ is defined in eq. (6.19b).

Equations (6.22) to (6.24) define the complete multi-phase power flow. Note that this is a generalization and therefore also a valid formulation of the three-phase and single-phase power flow.

##### 6.1.5 Line admittance model

The line admittance model describes the series and shunt admittance matrices for multi- phase lines. The series impedance can be characterized according to [31, p. 77, Chapter 4] as:

The series impedance of a [...] distribution line consists of the resistance of the conductors and the self and mutual inductive reactances resulting from the magnetic fields surrounding the conductors.

Further, for the shunt admittance [31, p. 121, Chapter 5]:

The shunt admittance of a line consists of the conductance and the capacitive susceptance. The conductance is usually ignored because it is very small compared to the capacitive susceptance. The capacitance of a line is the result of the potential difference between conductors.

Therefore, the line admittance model can be compiled based on the 1) resistance, 2) inductive reactance and 3) capacitance element matrices as:

|||−1|
|---|---|---|
|bse|b b|b b|
|bsh|el b b||

*Y* = (*R l* + *jX l*) (6.25a) <u>j</u> *Y* = 2*πf C l* (6.25b) 2

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u> The matrices *Y*
*bse* and *Y* *bsh* denote the series and shunt admittance matrices of line *b*. The matrices *Rb*, *Xb*and *Cb*denote the resistance, reactance and capacitance element matrices of line *b*. The symbols *f* *el* and *lb*denote the AC frequency of the electric grid and the length of line *b*.

The matrices *R*

|, X and C|can be defined depending on the conductor properties and|||
|---|---|---|---|
|b b|b b b b|b b|b|

arrangement according to [31, Chapter 4-5], e.g. through the Carson equations. At the time of writing, MESMO expects *R*, *X* and *C* as input parameters and their formulation is excluded here for the sake of brevity. Note that MESMO only requires the definition of a lower triangular matrix for *R*, *X* and *C* (see data reference¹) because these matrices are typically symmetric [32].

##### 6.1.6 Transformer admittance model

The transformer admittance model describes the series and shunt admittance matrices for multi-phase distribution transformers. These matrices can be interpreted according to [32, p. 6, Section IV-C] as follows:

In distribution systems, a three-phase transformer can be appropriately repre- sented by two blocks, namely, a series block representing the per unit leakage admittance, and a shunt block modeling transformer core losses.

Note that distribution grid transformers appear in various phase connection schemes, where [31, p. 249, Chapter 8] and [32, p. 6, Table III] summarize the most common connection schemes. At the time of writing, the following connection schemes can be modeled in MESMO:

•Grounded Wye-Grounded Wye (wye-wye) •Grounded Wye-Delta (wye-delta) •Delta-Delta (delta-delta)

Depending on the connection scheme, the series and shunt admittance matrices are defined according to [32, p. 6, Table III] as:    *Ybtrf,* 1 for wye-wye *Y* *btrf,* 1 for wye-wye   *se,f*<u>1</u>1 *se,t* 2

|se,f||1|se,t|2||
|---|---|---|---|---|---|
|b|trf 2 b|btrf, trf,2 b|b|btrf, trf,2 b||
||btrf,1|||trf,1 b||
|sh,f||3|sh,t||trf,3|
|b [https://purl.org/mesmo/docs/0.5.0/data_reference.html#electric-grid-line-types-matrices|trf](https://purl.org/mesmo/docs/0.5.0/data_reference.html#electric-grid-line-types-matrices|trf) b trf,2 b|btrf,|b|trf b trf,2 b|b|

*Y* = *Y* for wye-delta *Y* = *Y* for wye-delta (6.26a)     *n*   *Y* for delta-delta *Y* for delta-delta    *Y* for wye-wye    *Y* for wye-wye   ⊺ <u>1 1</u> *Y* = *− Y* for wye-delta *Y* = *− Y* for wye-delta *n*   *n*   *Y* for delta-delta *Y* for delta-delta

(6.26b) 1

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u>

||se,f|se,t|sh,f|sh,t||||
|---|---|---|---|---|---|---|---|
|trf b|b|b|b|b|trf,1 b|trf,2 b|trf,3 b|
 The matrices *Y*, *Y*, *Y*, *Y* denote the series and shunt admittance matrices of transformer *b* in from / to directions. The matrices *Y*, *Y* and *Y* denote the supplemental transformer admittance matrices according to [32, p. 6, Section IV-C]. The symbol *n* is the turns ratio of transformer *b*. The supplemental transformer admittance matrices are defined as:
    *trf trf trf trf* *y* *b* 0 0 2*y* *b* *−y* *b* *−y* *b* *trf,*1   *trf,*2<u>1</u>   *Y* *b* =  0 *y* *btrf* 0  *Yb*= *−y* *btrf* 2*y* *btrf* *−y* *btrf*  (6.27a) *trf*3*trf trf trf* 0 0 *y* *b* *−y* *b* *−y* *b* 2*y* *b*   *trf trf*! *−*1 *−y* *b* *y* *b* 0*trf trf trf* *trf,*3   *trf*2*rbjxb|sb|*

|Y|=  0|−y|y |y =|+|||(6.27b)|
|---|---|---|---|---|---|---|---|---|
|b trf b|trf b trf b|btrf|btrf trf b|b|||2 n|trf b|
||||||n||||

*b btrf btrf b* 2 *trf trf*100 100 *u tb* *y* 0 *−y*

The scalar *y* denotes the base admittance value of transformer *b*. The symbols *r* and *x* are the percentage resistance and reactance values in percentage of the voltage when *trf* operating at nominal apparent power. The scalars *|s* *b* *|* and *u t* denote the nominal apparent *b* power, i.e. rated power, and the nominal voltage the secondary node of transformer *b*.

##### 6.1.7 DER connection

DERs may be only either wye or delta-connected as described in section6.1.3and fig.6.3. Since MESMO allows for single-phase, two-phase as well as three-phase wye and delta connections, more general combinations of line-to-line and line-to-ground connections can be represented through superposition of multiple wye and delta DERs. Furthermore, all DERs are described with PQ models, i.e. all DERs act as constant power sources or loads. *Y N* *el* *×*1 The nodal power injections from wye-connected DERs *s ∈* C and delta-connected ∆ *N* *el* *×*1 *Del×*1

|∆ N|×1||||D ×1|
|---|---|---|---|---|---|
||||Y ∆|Y ∆||
|el|Y ∆|N ×D||||

DERs *s ∈* C are related with the DER power vector *s ∈* C as follows:

##### s = A s (6.28a)

##### s = A s (6.28b)

*el el* The matrices *A, A ∈* R are the wye and delta DER mapping matrices. The symbol *D* denotes the set of DERs.

The mapping matrices are defined as:   <u>1</u>*n* h i *p*for *n* = *nd*and *p ∈Pd* *A* *Y* = *a* *Y* (*n,pn*)*,del* *a* *Y* (*n,pn*)*,d* = *Nd*(6.29a) ((*n,pn*)*,d*)*∈N ×Del* 0 otherwise   <u>1</u>*n* h i *p*for *n* = *nd*and *p ∈Pd* *A* ∆ = *a* ∆ (*n,pn*)*,del* *a* ∆ (*n,pn*)*,d* = *Nd*(6.29b) ((*n,pn*)*,d*)*∈N ×Del* 0 otherwise

<u>6. Electric grid modeling 6.1. Fundamental electric grid model</u>
*p* The symbol *Pd*denotes the set of phases that DER *d* is connected to. The scalar *N* *d* denotes the total number of that DER *d* is connected to. Note that this assumes that the power injection or load of DER *d* is balanced across its connected phases. Nevertheless, unbalanced loading conditions can be modeled by defining multiple single-phase or two-phase DERs at the same node.

##### 6.1.8 Source connection

The source node of the electric grid is characterized with a constant nominal voltage as:

|||||
|---|---|---|---|
|||sr,a|j|
|sr sr,b sr,c|sr sr,a|sr,b sr,c sr,b|j j sr,c|

*a e* <u>−</u> 3 <u>2π</u> *u* = *u* *a e*  (6.30a) <u>2π</u> *a e*3

The vector *u* *sr* denotes the three-phase source node voltage. The scalar *u* *sr* denotes the source voltage magnitude. The scalars *a,a,a ∈{*0*,*1*}* indicate whether phases *a,b,c* are connected as *a* *sr,a* *,a,a* = 1. Therefore, a multi-phase source node can be modeled by selecting only the relevant phases.

The nodal no-load voltage of the electric grid, i.e. assuming no injection or load from any DERs, can be expressed based on the source node voltage and the admittance matrix as:

||||nl,ns|ns,ns −1|ns,sr|sr|||
|---|---|---|---|---|---|---|---|---|
|nl,ns sr,ns|nl N /P ×1 N /P|N ×1 ×P|nl sr ns N|sr sr N ×P ×N /P|ns nl,ns sr|ns ns,ns|N /P ×N|/P|
||||||||sr||

##### u = (Y) Y u (6.31a)

*u* = *A u* + *A u* (6.31b)

*el* The vector *u ∈* C denotes the complete no-load nodal voltage vectors, whereas *el sr* *u ∈* C denotes the no-load voltage vector of no-source nodes, i.e. all nodes excluding the source node itself. The matrices *A* and *A* denote the source and no- *el sr* source mapping matrices, where *A ∈* R maps the voltage of the source node to *el el sr* the nodal voltage vector and *A ∈* R maps the voltages of no-source nodes *el sr el sr* to the nodal voltage vector. Correspondingly, the matrices *Y ∈* R and *el sr sr* *Y ∈* R denote the partial admittance matrices from no-source nodes to no-source nodes and from source node to no-source nodes. The symbol *P* denotes the set of enabled phases at the source node.

##### 6.1.9 Source and no-source notation

The source / no-source mapping matrices are defined as: h i *sr sr*

|A =|a|||||
|---|---|---|---|---|---|
||(n,p),p|((n,p),p|)∈N ×P sr|n|sr|
||sr (n,p),p|||||
|ns|ns (n ,p),(n|,p) ((n ,p|),(n ,p))∈N|×N /P||

(*n,pn*)*,psr el* (6.32a) ((*n,pn*)*,psr*)*∈N ×Psr* ( 1 for *n* = *n* and *p* = *p* *a n sr* = (6.32b) 0 otherwise h i *A* = *a*1 1 2 2 *el el* (6.32c) 1 1 2 2 *sr*

<u>6. Electric grid modeling 6.2. Non-linear power flow solution</u>
( *ns* for *n¹* = *n²* and *p¹* = *p²* *a* (*n,p*)*,*(*n,p*) = (6.32d) 0 otherwise

The partial admittance matrices between source and no-source nodes are defined based on the mapping matrices as:

|sr,sr|sr ⊺|sr|ns,ns|ns ⊺|ns|
|---|---|---|---|---|---|
|sr,ns sr,sr|ns ⊺ ns,ns sr,ns|sr|ns,sr|sr ⊺|ns|
|||||el||

*Y* = (*A*) *YA Y* = (*A*) *YA* (6.33a) *Y* = (*A*) *YA Y* = (*A*) *YA* (6.33b)

The matrices *Y*, *Y*, *Y* and *Y* *ns,sr* are referred to as partial admittance because they contain distinct portions of the complete nodal admittance matrix *Y*. In the special case that the source node phases are arranged to be the first entries in *N*, these matrices can be interpreted according to [11, p. 58, Section 3.4.1]:

*Y* *sr,sr* *Y* *ns,sr* *Y* =*sr,ns ns,ns*(6.34a) *Y Y*

That is, the partial admittance matrices represent a partitioning of the complete nodal admittance matrix.

For notational convenience in the formulation of power flow solution algorithms below, the following short-hand notations are defined for the source / no-source variable vectors: *sr sr* ⊺ *ns ns* ⊺ *u* = (*A*) *u u* = (*A*) *u* (6.35a) *Y,sr sr* ⊺ *Y sr* ⊺ *Y Y,ns ns* ⊺ *Y ns* ⊺ *Y* *s* = (*A*) *s* = (*A*) *A s s* = (*A*) *s* = (*A*) *A s* (6.35b) ∆*,sr sr* ⊺ ∆ *sr* ⊺ ∆*,ns ns* ⊺ ∆ *ns* ⊺ ∆ *s* = (*A*) *s* = (*A*) *s s* = (*A*) *s* = (*A*) *A s* (6.35c)

The source variable vectors are denoted by () *sr*, whereas the no-source variable vectors are denoted by () *ns*. The source / no-source mapping matrices *A* *sr*, *A* *ns* are defined according to section6.1.8, eq. (6.32). The DER mapping matrices *A* *Y*, *A* ∆ are defined in section6.1.7, eq. (6.29).

#### 6.2 Non-linear power flow solution

##### 6.2.1 Outline

The power flow solution describes the process of solving the power flow equations in eqs. (6.14) to (6.16) and (6.20), in order to obtain the state variables of the electric grid ac- cording to section6.1.1. To this end, the power flow solution essentially is a simulation of the steady-state power flow. As prerequisite for the power flow solution, recall from section6.1.7 that DERs are described with wye or delta-connected PQ models, i.e. all DERs act as constant power sources or loads. Furthermore, the following assumes that the source node of the electric grid can be characterized with a constant voltage according to section6.1.8.

The power flow problem is then solved by inserting the DER power vector *s* and the nominal source voltage *u* *sr* into the power flow equations in eqs. (6.14) to (6.16) and (6.20). However,

<u>6. Electric grid modeling 6.2. Non-linear power flow solution</u> these equations to not yield an explicit equation for the nodal voltage vector *u*, particularly due to the appearance of *u* in the delta injections eq. (6.20). Therefore, recursive solution techniques have been formulated for the power flow problem, such as the fixed-point method from [11], which is described in section6.2.2. Once a solution for the nodal voltage vector is obtained, the branch power flow vectors *s*
*f* *, s* *t* and total loss *s* *ls* can be obtained based on eq. (6.22) as: *f f f* (6.36a)

|s = diag|A u|Y u|
|---|---|---|
|t ls|t|t|

*s* = diag *A u Y u* (6.36b)

*s* = *u* ⊺ *Y u* (6.36c)

##### 6.2.2 Fixed-point method

According to [11], [33], the power flow solution can be obtained with the following fixed-point equation: ⊺

|ns|nl,ns|ns,ns −1||ns −1|Y,ns|ns,ns|ns −1|∆,ns|
|---|---|---|---|---|---|---|---|---|
|n|sr sr|ns ns||n−1|||n−1||
||n n−1|n|||||||
|ns Y,ns|∆,ns||||||||
||||ns,ns|ns,ns||sr|||
|ns,ns|sr ⊺|ns||sr|ns||||

*u* = *u* + (*Y*) diag(*u*) *s* + (*H*) diag *u s* (6.37a) *u* = *A u* + *A u* (6.37b)

The indices (), () denote the current and the previous fixed-point iteration. The vectors *u*, *s*, *s* denote the no-source vectors for voltage, wye power injections and delta power injections according to eq. (6.35). The vector *u* denotes the three-phase source node voltage. The matrices *Y* and *H* denote the partial admittance and delta phase mapping matrix from no-source to no-source nodes according to eq. (6.33), where *H* = (*A*) *HA*. The matrices *A* and *A* denote the source and no-source mapping matrices according to eq. (6.32).

In addition to the fixed-point equation, [11], [33] define conditions for existence and unique-

|||rf Y,rf|∆,rf Y|∆|||
|---|---|---|---|---|---|---|
||Y,rf|∆,rf|rf 2 rf 2|Y,rf|∆,rf||
|Y|Y,rf ∆|∆,rf|||||
|||||rf|||
|rf Y,rf|∆,rf||||||
|||||||rf|
|∆,rf|||||||
|Y ∆|||||Y|∆|

ness of a solution for a given set of *u*, *s, s*, *s, s* as:

*ξ*(*s, s*) *< γ*(*u*) (6.38a) <u>1 γ(u) − ξ(s, s)</u> *ξ*(*s − s, s − s*) *<* (6.38b) 4 *γ*(*u*)

The vectors *u*, *s, s* denote the reference point of the nodal voltage vector and the nodal power injection vectors, i.e. an existing valid solution for the power flow. Note that the chose reference point must satisfy eq. (6.38a), where the no-load point *u* = *u* *nl*, *s* *Y,rf* = 0*, s* = 0 is a trivial choice for the reference point, if no other solution is available. The vectors *s, s* denote the present power injection vectors, i.e. the values for which the solution is thought, where condition eq. (6.38b) constrains the choice of *s, s* depending on the reference point. The short-hand symbols *ξ* and *γ* are defined as:

|Y,rf ∆,rf|nl,ns −1|ns,ns −1|nl,ns −1|Y,ns|
|---|---|---|---|---|
|||||∞|

*ξ*(*s, s*) := diag *u* (*Y*) diag *u* diag *s*

<u>6. Electric grid modeling 6.3. Linear approximate model</u>
! *nl,ns* *−* *ns,ns − nl,ns* *−* ∆*,ns* + diag *u* (*Y*) diag *|H |u* diag *s* *∞* (6.39a) <u>(|u</u> *ns* <u>|)i(|H</u> *ns,ns* <u>u</u> *ns* <u>|)i</u> *γ*(*u*) := min min *nl,ns* *,*min *ns,ns nl,ns* (6.39b) *i* (*|u |*)*i i* (*|H ||u |*)*i*

Based on eqs. (6.37) and (6.38), a comprehensive algorithm for obtaining a power flow solution with the fixed-point method is described in algorithm1. Here, the no-load point

|rf,ns|nl,ns|Y,rf|∆,rf|||
|---|---|---|---|---|---|
|s|Y,cn|∆,cn|Y,cn|Y ∆,cn|∆|
||||u|||
||||||lim|

*u* = *u*, *s* = 0*, s* = 0 is chosen as reference point for the solution, as a previous power flow solution may not always be available. The candidate power injection vectors are initially set to *s* = *s*, *s* = *s*. If the solution condition eq. (6.38a) does not hold for *s, s* the power values are iteratively scaled down with the scaling factor *f* in the outer loop. Once the condition holds, a solution is obtained in the fixed point loop. A valid fixed-point solution is reached when the voltage value change across two iterations falls below the threshold *ε*. Subsequently, the power values are scaled back up, until *f* *s* = 1, while iteratively obtaining fixed-point solutions. Both the outer loop and the fixed-point loop cannot exceed the respective iteration limits *M* and *N* *lim*.

#### 6.3 Linear approximate model

##### 6.3.1 Fundamental linear model

The linear electric grid model formulates a linear representation of the non-linear power flow equations from sections6.1and6.2. This forms the basis for the convex formulation of optimal operation problems in chapter9. Based on the type of approximation, the following linear models are distinguished:

- Linear model based on **global approximation** (section6.3.2), where the model repre- sents a secant plane between the no-load point and a reference point of the power flow manifold.
- Linear model based on **local approximation**, where the model represents a tangent plane at a reference point of the power flow manifold.
Note that MESMO currently only implements global approximation methods, although future implementations for local approximations are anticipated and the fundamental linear model formulation is decoupled from the approximation methods.

For both approximation types, the linear electric grid model is represented in terms of sensitivity matrices for changes in the electric grid state variables with regards to changes in the DER power injection / load as:

*|ut|* = *|u* *rf* *|* + *M* *|u|,p* ∆*pt*+ *M* *|u|,q* ∆*qt∀t ∈T* (6.40a) *f f,rf |sf|,p |sf|,q* *|st|* = *|s |* + *M* ∆*pt*+ *M* ∆*qt∀t ∈T* (6.40b)

6. Electric grid modeling 6.3. Linear approximate model **Algorithm 1:** Electric power flow solution based on fixed-point method **begin** initialization: *u* *ns* *n*=0= *u*
*rf,ns* = *u* *nl,ns*, *s* *Y,rf* = 0, *s* ∆*,rf* = 0, *s* *Y,cn* = *s* *Y*, *s* ∆*,cn* = *s* ∆; *f* *s* = 1, *m* = 1, *n* = 1 **repeat** outer loop: *Y,cn Y,rf* ∆*,cn* ∆*,rf* <u>1</u> *γ*(*u* *rf*)2*−ξ*(*sY,rf,s*∆*,rf*) **if** *ξ*(*s − s, s − s*) *≥* 4 *γ*(*urf*) **then** *s* <u>f</u> *s* *f* = 2; **else if** *f* *s* *<* 1 **then** *f* *s* = 2*f* *s*;

*s* *Y,cn* = *f* *s* *s* *Y*, *s* ∆*,cn* = *f* *s* *s* ∆; *Y,cn Y,rf* ∆*,cn* ∆*,rf* <u>1</u> *γ*(*u* *rf*)2*−ξ*(*sY,rf,s*∆*,rf*) **if** *ξ*(*s − s, s − s*) *<* 4 *γ*(*urf*) **then** **repeat** fixed-point loop: *u* *ns* *n*= *u* *nl,ns* + *ns,ns −*1 *ns −*1 *Y,ns ns,ns* ⊺ *ns −*1 ∆*,ns*

(*Y*) diag(*un−*1) *s* + (*H*) diag *un−*1*s*; *n* = *n* + 1;
**until** *u* *ns* *n− u* *ns* *n−*1 1*< ε* *u* *; n ≥ N* *lim*; *u* *ns* *n*=0= *u* *rf,ns* = *u* *ns* *n*; *m* = *m* + 1; *Y,cn Y,rf* ∆*,cn* ∆*,rf* <u>1</u> *γ*(*u* *rf*)2*−ξ*(*sY,rf,s*∆*,rf*) *s lim* **until** *ξ*(*s − s, s − s*) *<* 4 *γ*(*urf*) *; f* = 1*; m ≥ M*; **begin** result variable update: *u* = *A* *sr* *u* *sr* + *A* *ns* *u* *ns* *n*<u>;</u> *s* *f/t* = diag *A* *f/t* *u Y* *f/t* *u*; *s* *ls* = *u* ⊺ *Y u*;

*tt t,rf |s |,pt|s |,qt* *|s |* = *|s |* + *M* ∆*pt*+ *M* ∆*qt∀t ∈T* (6.40c) *ls ls,rf pls,p pls,q*

||p = p|+ M|∆p + M|∆q||∀t ∈T||(6.40d)||
|---|---|---|---|---|---|---|---|---|---|
||tls ls,rf t|q ,p ×1 f t|t tt|q ,q t B ×1||||||
|el|el el el||||ls t|tls||||
||t t|D ×1 |u|,p||u|,q|N|×D||s |,p||s |,q|rf el |s |,q|el|
|B ×D|p ,p|,q q ,p|q ,q|1×D||||||
|t|t rf|t t|rf||t t|D ×1||||

*t t t* *ls ls* *q* = *q* + *M* ∆*p* + *M* ∆*q ∀t ∈T* (6.40e)

*Nel el* The vectors *|u | ∈* R, *|s |, |s | ∈* R are the voltage magnitude at electric grid nodes *n ∈N* and the branch power flow magnitude in from / to direction at electric grid branches *b ∈B* for time step *t ∈T*. The scalars *p* and *q* denote the total active and reactive loss for time step *t*. The reference point for each property is denoted by (). The *el* vectors ∆*p,* ∆*q ∈* R are the active and reactive power change at DERs *d ∈D* *el el f f|s |,pt t* for time step *t*. The matrices *M, M ∈* R, *M, M, M, M ∈* *el el lspls ls ls el* R, *M, M, M, M ∈* R are the sensitivity matrices for the change of the respective properties to the active and reactive power change, which in turn are defined *el* as ∆*p* = *p − p*, ∆*q* = *q − q*. The vectors *p, q ∈* R are the absolute active

<u>6. Electric grid modeling 6.3. Linear approximate model</u>
*el el rf rf* and reactive power demand of the DERs *dt t*

|∈D. The vectors p|, q|are the active and|
|---|---|---|
|el|t|t|

reactive power demand reference of the DERs *d* *el*.

Based on the linear electric grid model, the operational constraints of the electric grid are expressed as:

||sr t|⊺ t|ls t|||
|---|---|---|---|---|---|
||tsr − f|⊺ t t f,+|tls +|||
|sr|t tt|t,+||||
|t|tsr|||− f,+|+ t,+|

*p −* 1 *p* = *p ∀t ∈T* (6.41a)

*q −* 1 *q* = *q ∀t ∈T* (6.41b) *|u |≤|u |≤|u | ∀t ∈T* (6.41c)

*|s |≤|s | ∀t ∈T* (6.41d) *|s |≤|s | ∀t ∈T* (6.41e)

The scalars *p* and *q* denote the active and reactive power demand at the source node of the electric grid at time step *t*. The symbols *|u |* and *|u |* denote the lower and upper bound on the nodal voltage magnitude, whereas *|s |*, *|s |* denote the upper bound on branch power flow magnitude in from / to direction. Note that eqs. (6.41a) and (6.41b) express the active and reactive power balance of the electric grid.

The reference point denoted by () *rf* is typically chosen to be 1) the nominal operation point for the global approximation or 2) the an estimate of the actual operation point for the local approximation. The reference properties for the linear approximate model eq. (6.40) are then obtained by solving the reference power flow problem of the electric grid, e.g. through fixed- point solution based on section6.2.2, and a global or local approximation for the sensitivity matrices can be obtained as a function of the reference properties according to section6.3.

##### 6.3.2 Global approximation

A linear model based on global approximation can be formulated based on [11], where the fol- lowing approach is taken: First, expressions for the sensitivity matrices of the complex-valued nodal voltage are formulated with respect to changes in the wye and delta power injections. Second, sensitivities for other electric grid state variables are thought as expressions with regards to the nodal voltage. Then, the desired sensitivity matrices with regards to changes in the DER power vectors can be formulated by aggregating the expressions.

The global approximation of the voltage sensitivity represents a secant plane between the no-load point *u* *nl* and a reference operation point *u* *rf* of the power flow manifold. As it turns out, the fixed-point equation in eq. (6.37) describes such a secant plane [33] and therefore lends itself to deriving the voltage sensitivity as the partial derivative of the complex-valued voltage with regards to the power injection vectors. To this end, the sensitivities of the nodal voltage for a change in the power injection is formulated as:

*Y* <u>δu</u>

|u,p ns,ns|ns|ns,ns −1||rf,ns −1||
|---|---|---|---|---|---|
||Y,ns|||||
|u,q ns,ns|ns|ns,ns|−1|rf,ns|−1|
||Y,ns|||||

*M* = = (*Y*) diag(*u*) (6.42a) *δp* *Y* <u>δu</u> *M* = = *−j* (*Y*) diag(*u*) (6.42b) *δq*

<u>6. Electric grid modeling 6.3. Linear approximate model</u> ∆ <u>δu</u>

|u,p ns,ns||ns|ns,ns −1|ns,ns|⊺|ns,ns rf,ns|−1|
|---|---|---|---|---|---|---|---|
|||∆,ns||||||
|u,q ns,ns||ns ∆,ns|ns,ns|−1 ns,ns|⊺|ns,ns|rf,ns −1|
||ns||ns,ns|sr||||
 *M* = = (*Y*) (*H*) diag *H u* (6.42c)
*δp* ∆ <u>δu</u> *M* = = *−j* (*Y*) (*H*) diag *H u* (6.42d) *δq*

The source variable vectors are denoted by (), whereas the no-source variable vectors are denoted by (). Accordingly () denotes the partial sensitivities of no-source nodal voltage with regards to no-source nodal injections, which follows the notation for admit- tance matrices from eq. (6.33). Since the source voltage remains constant according to section6.1.8, the remaining partial sensitivities are matrices of zeros:

*u,pY/qY/p*∆*/q*∆ *sr,sr* *M* = 0 (6.43a)

*u,pY/qY/p*∆*/q*∆ *sr,ns* *M* = 0 (6.43b)

*u,pY/qY/p*∆*/q*∆ *ns,sr* *M* = 0 (6.43c)

Note that eqs. (6.42) and (6.43) express the voltage sensitivities with regards to the nodal wye / delta power injection vectors *p* *Y* *, q* *Y* *, p* ∆ *, q* ∆, whereas the fundamental linear model in eq. (6.40) is expressed with regards to the DER active / reactive power vectors *p, q*. With the chain rule *δx* <u>δz</u> = *δy* <u>δz</u> *δx* <u>δy</u>, the according representation of the voltage sensitivities is obtained as:

*u,pδu δu δp* *Y* *δu δp* ∆ *u,pYY u,p*∆∆ *M* = = *Y* + ∆ = *M A* + *M A* (6.44a) *δp δp δp δp δp*

*u,qδu δu δq* *Y* *δu δq* ∆ *u,qYY u,q*∆∆ *M* = = *Y* + ∆ = *M A* + *M A* (6.44b) *δq δq δq δq δq*

Here, the matrices *A* *Y*, *A* ∆ denote the DER mapping matrices according to section6.1.7, eq. (6.29).

Then, the sensitivities of the voltage magnitude *M* *|u|,p* *, M* *|u|,q* can be derived from sensitivi- ties of the complex-valued voltage *M* *u,p* *, M* *u,q* with the following derivation rule according to [33, p. 5, Section V-A]:

*δ|y|* 1 *δy* = Re *y* where *y ∈* C*,x ∈* R (6.45a) *δx |y| δx*

Thus, the sensitivities of the voltage magnitude are expressed as:

||u|,p|rf −1|rf|u,p|
|---|---|---|---|
||u|,q|rf −1|rf|u,q|

*M* = diag *|u |* Re diag *u M* (6.46a)

*M* = diag *|u |* Re diag *u M* (6.46b)

The sensitivities of the branch flow magnitude with regards to the DER power vector are represented using the chain rule *δx* <u>δz</u> = *δy* <u>δz</u> *δx* <u>δy</u> as:

*|sf/t|,p*<u>δ|s</u> *f/t* <u>| δ|s</u> *f/t* <u>| δu</u>*|sf/t|,u u,p* *M* = = = *M M* (6.47a) *δp δu δp*

<u>6. Electric grid modeling 6.3. Linear approximate model</u>
*|sf/t|,q*<u>δ|s</u> *f/t* <u>| δ|s</u> *f/t* <u>| δu</u>*|sf/t|,u u,q* *M* = = = *M M* (6.47b) *δq δu δq*

The sensitivity of the branch power magnitude with regards to the complex-valued voltage *|sf/t|,u* *M* is then derived from eqs. (6.36) and (6.45) as:

*|sf/t|,u*<u>δ|s</u> *f/t* <u>|</u>*f/t,rf −*1 *f/t,rf s* *f/t,u* *M* = = diag *|s |* Re diag *s M* (6.48a) *δu* *s* *f* = diag *A* *f* *u Y* *f* *u* (6.48b)

*s* *f/t,u*<u>δs</u> *f/t* *f/t rf f/t f/t rf f/t* *M* = = diag *A u Y* + diag *Y u A* (6.48c) *δu*

Note that the above relies on the following derivation rule:

*δ* (diag (*y*) *z*) *δz δy δz δy* = diag (*y*) + diag (*z*) = diag (*y*) + diag (*z*) (6.49a) *δx δx δx δx δx*

|δ(yz)|δy|δz|
|---|---|---|
|δx|δx|δx|

This utilizes the product rule = *z* + *y* as well as the commutativity of the Hadamard product, i.e. diag(*x*)*y* = diag(*y*)*x*.

The sensitivities of the active / reactive losses with regards to the DER power vector are similarly derived using the chain rule *δx* <u>δz</u> = *δy* <u>δz</u> *δx* <u>δy</u> as:

|||δx|δy|||
|---|---|---|---|---|---|
||ls|ls|ls|||
|p ,p|ls|ls|ls|s ,u|u,p|
|q ,q||||s ,u|u,q|

*ls δp δs δs δu ls* *M* = = Re = Re = Re *M M* (6.50a) *δp δp δu δp* *ls δq δs δs δu ls* *M* = = Im = Im = Im *M M* (6.50b) *δq δp δu δq*

*s* *ls,u* The sensitivity of the complex-valued loss with regards to the complex-valued voltage *M* is then derived from eq. (6.36) as:

*s* *ls* = *u* ⊺ *Y u* (6.51a)

*s* *ls,u*<u>δs</u> *ls* ⊺ ⊺ *M* = = *u Y* + *Y u* (6.51b) *δu*

Note that the above relies on the following derivation rule:

|⊺|||
|---|---|---|
||⊺|⊺|
|δ(yz)|δy|δz|
|δx|δx|δx|

*δ* (*y z*) *δz δy*⊺*δz*⊺*δy* = *y* + *z* = *y* + *z* (6.52a) *δx δx δx δx δx*

This utilizes the product rule = *z* + *y* as well as commutativity of the dot product,

i.e. *x* ⊺ *y* = *y*
⊺

*x*.
96

## 7 Thermal grid modeling

#### Contents

7.1 Fundamental thermal grid model........................ 98
7.1.1 Scope and assumptions........................ 98

7.1.1 Scope and assumptions.	98
7.1.2 Thermal power flow.	99
7.1.3 Pipe pressure loss model.	102
7.1.4 DER connection.	103
7.1.5 Source connection.. 104
7.1.6 Source and no-source notation.. 104
Non-linear power flow solution..	105
7.2.1 Outline.	105
7.2.2 Explicit method for radial networks...	106
Linear approximate model.. 107
7.3.1 Fundamental linear model.. 107
7.3.2 Global approximation for radial networks.	108

7.2
....

7.3
**Outline and contributions**

This chapter first introduces fundamental power flow formulations for the thermal grid along with a solution algorithm for the power flow problem. Secondly, a method for obtaining a linear approximate thermal grid model is presented. The former is utilized for the nominal operation problem formulation, whereas the latter is a prerequisite for defining the convex optimal operation problem.

The fundamental thermal grid model and non-linear thermal power flow solution have been redeveloped for this thesis but are essentially adapted from the established fundamentals for water distribution systems, DCSs and DHSs in [35]–[38]. This portion of the work was supported through the master theses [39], [40], which the author supervised. An entirely original contribution of this thesis is the linear approximate thermal grid model in this chapter, which serves as the basis for formulating the thermal grid DLMPs in chapter9. This work was previously published by the author in [14], [41].

<u>7. Thermal grid modeling 7.1. Fundamental thermal grid model</u>
#### 7.1 Fundamental thermal grid model

##### 7.1.1 Scope and assumptions

The focus of thermal grid modeling for MESMO is to express the state variables of DHSs and DCSs as function of the input variables. In the following, “thermal grid” is used as generalized term for both DHSs and DCSs, where the chosen modeling approach is general enough to cover both system types. The thermal grid is abstracted to nodes and branches, where nodes refer to vertices, i.e. interconnection points of DERs and branches, and branches refer to edges, i.e. pipes or other fluid delivery elements. A source node is defined as the connection point to the main DHP or DCP. Note that additional decentralized heating plants and cooling plants can be represented as DERs in the thermal grid. The layout of supply and return piping is assumed to be symmetric, such that the thermal grid can be modeled with a single graph.

The following does not consider the nodal supply / return fluid temperatures and thermal losses. To this end, the current thermal grid model implementation in MESMO assumes thermal losses to be neglectable and supply / return fluid temperatures to be constant, i.e. the fluid transport across branches is isothermal as well as isenthalpic and the enthalpy difference between supply and return side is constant. A future extension of the thermal power flow formulation with a model for thermal losses is possible based on the work [72]. Further, the thermal transport fluid is assumed to be incompressible.

##### The considered state variables are:

##### •Nodal pressure head vector h

•Branch volume flow vector *q* *th,b*

•Pump power demand *p* *pm*

The pressure head or hydraulic head *h* in units of length is utilized here to represent quantities *st* <u>p</u> *st* of pressure and is related to the static fluid pressure *p* as *h* = *ρ* *flg*, where the constants *g* and *ρ* *fl* denote the gravitational acceleration and the density of the thermal transport fluid,

e.g. water. State variables of the DHP or DCP are not included here. Instead, these plants are represented with DER models according to sections8.3.6and8.3.7.
##### The assumed input variables are:

•DER thermal power injection vector *p* *th*

Note that the injection / load of DERs is assumed to be controlled in terms of thermal power,

i.e. all DERs act as constant power sources or loads. Furthermore, the fluid temperature difference across the ETS of each DER is assumed to be constant, which requires DERs to control their fluid return temperature. Furthermore, a distributed pumping scheme is assumed, i.e. distribution pumps are installed at the ETS of each DER rather than centrally.
98

<u>7. Thermal grid modeling 7.1. Fundamental thermal grid model</u>
Figure 7.1: Thermal power flow between two nodes of the thermal grid.
 The fundamental thermal grid model is introduced based on the thermal power flow in section7.1.2.
##### 7.1.2 Thermal power flow

The key model components of the thermal power flow formulation are 1) the branch head balance, 2) the nodal flow balance and 3) the hydraulic loss equations. In comparison to the electric power flow, the nodal flow balance is equivalent to the Kirchhoff current law and the branch head balance corresponds to the Kirchhoff voltage law. Note that this assumes neglectable thermal losses across branches and constant supply and return fluid temperatures.

As a starting point, consider the thermal power flow across the branch (1*,*2) between two nodes 1 and 2 of the thermal grid according to fig.7.1. The extended Bernoulli equation for incompressible fluids describes the steady-state fluid flow along branch (1*,*2) as:

*f* 2 *t* 2 *v* <u>1,2 v</u> *el* <u>1,2</u> *el ls* + *h₁* + *h₁* = + *h₂* + *h₂* + ∆*h₁,*2(7.1a) 2*g* 2*g* *th,f th,t* *f* <u>4q₁</u> <u>,2</u> *t,* <u>4q₁</u> <u>,2</u> *v₁* *,*2 = *th* 2 *v₁*2= *th* 2 (7.1b) *π*(*d₁* *,*2 ) *π*(*d₁* *,*2 )

*f th,f* The scalars *v₁* *,*2 and *q₁* *,*2 denote the average fluid velocity and branch volume flow rate in “from”-direction from node 1 into branch (1*,*2). Consequently, *s* *t* 1*,*2and *i* *t* 1*,*2denote the average fluid velocity and branch volume flow rate in “to”-direction from node 2 into branch (1*,*2),

i.e. towards node 1. The symbols *h*
*el* 1*,h* *el* 2describe the elevation of node 1 and 2, whereas *h₁,h₂* are the pressure head at nodes 1 and 2. The scalar ∆*h* *ls* 1*,*2denotes hydraulic head removed due to losses. Note that the hydraulic head *h* in units of length is used to represent *st* <u>p</u> *st* quantities of pressure and is related to the static pressure *p* as *h* = *ρ* *flg*. The constants *g* and *ρ* *fl* denote the gravitational acceleration and the density of the thermal transport fluid,

e.g. water. The scalar *d*
*th* 1*,*2denotes the pipe diameter of branch (1*,*2). Note that this variant of the Bernoulli equation expresses each component in terms of hydraulic head, which allows a more convenient notation than the traditional form in terms of energy [36, p. 69]. Also note that the actual fluid velocity is not homogeneously distributed across the branch cross-section due to shear stresses [35, pp. 26-28] but this does not impact the validity of the Bernoulli equation.

<u>7. Thermal grid modeling 7.1. Fundamental thermal grid model</u> The Bernoulli equation from eq. (7.1) can be simplified by assuming that 1) all nodes of the thermal grid are at the same elevation *h*
*el* 1= *h* *el* 2and 2) the average fluid velocity is *f t, th*

|f|t,|||||||th|
|---|---|---|---|---|---|---|---|---|
|,2|2|||||th,f|th,t|,2|
|||||||,2|,2||
|||||ls|||||
|||||1,2|||||
|||ls|||||||
|||1,2 ls|th th,f|2 th|th,t 2||||
|||,2|,2 ,2|,2|,2||||

constant *v₁* *,*2 = *−v₁*2. The latter follows from the assumed constant pipe diameter *d₁,*2and the incompressibility of the thermal transport fluid, which yields *q₁* = *−q₁*. Therefore, eq. (7.1) is reformulated as:

##### h₁ − h₂ = ∆h (7.2a)

Further, the head loss ∆*h* is defined as:

∆*h₁* = *r₁ q₁* = *r₁ q₁* (7.3a)

This notation utilizes a compact representation for the head loss model similar to [72], [84], where the scalar *r₁* *th* *,*2denotes the loss coefficient of branch (1*,*2), which is defined according to the pipe pressure loss model in section7.1.3.

The branch flows are related to the nodal flow balance as follows:

*th,n th,n th th,n th,n th* *p₁* = *q₁* ∆*h p₂* = *q₂* ∆*h* (7.4a) *th,n th,t th,f th,n th,t th,f*

||q₁ = q₀|+ q₁||q₂ = q₁|+ q₂|||(7.4b)|
|---|---|---|---|---|---|---|---|---|
||th,n th,n|,1|,2 th,n|th,n|,2 th,n|,3 th,n th,t|th,n th,f|th,t|
|||||||,1|,2|,2|
|th,f ,3||||||||f|
|t||||th|||||

*,*1*,*2*,*2*,*3

*th,n* The scalars *p₁*, *p₂* as well as *q₁*, *q₂* are the thermal power injection / load as well as nodal volume flow rate at nodes 1, 2. By convention, *p₁*, *p₂*, *q₁*, *q₂* are positive for thermal power injections and negative for thermal loads. The scalars *q₀*, *q₁*, *q₁* and *q₂* denote the branch volume flow rate at branches (0*,*1), (1*,*2) and (2*,*3), where () and () denote the “from” and “to” direction. The symbol ∆*h* denotes the enthalpy difference between primary and secondary side of the thermal grid.

Pumping power demand in thermal grids occurs can be distinguished into 1) primary pumping demand and 2) secondary pumping demand [160, p. 434, Figure 13-9]. Primary pumping occurs within the fluid circuit of the central district heating / cooling plant, whereas secondary pumping occurs within the thermal grid itself. As district heating / cooling plants are modeled separately, the following only considers the secondary pumping demand. Recall from section7.1.1that MESMO assumes a distributed pumping scheme the thermal grid, i.e. distribution pumps are installed at the ETS of each DER rather than centrally at the district heating / cooling plant. Therefore, the pump power demand at nodes 1 and 2 is expressed as:

*pm*<u>−g</u>*th,n ets pm*<u>−g</u>*th,n ets* *p₁* = *th,pm* *q₁* 2*h₁* + ∆*h p₂* = *th,pm* *q₂* 2*h₂* + ∆*h* (7.5a) *η η*

The scalars *g* and *η* *th,pm* denote the gravitational acceleration and the pump efficiency. The scalars ∆*h* *ets* denote the hydraulic head loss across the ETSs at nodes 1 and 2. Note the factor 2 consider that the nodal pressure heads *h₁,h₂* occur symmetrically for the supply side as well as the return side of the thermal grid.

<u>7. Thermal grid modeling 7.1. Fundamental thermal grid model</u> As the next step, the thermal power flow eqs. (7.2) to (7.5) can be generalized for all nodes *n ∈N* *th* and branches *b ∈B*
*th* as: X X *th,n th,n th th,n th,t th,f th* *pn*= *qn*∆*h qn*= *q* *b* + *q* *b* *∀n ∈N* (7.6a) *b∈Bn* *th,t* *b∈Bn* *th,f* *th,f/t* <u>4q</u>

|f/t|b th,f/t||||th,f|2|th|
|---|---|---|---|---|---|---|---|
|b|th|2|n|n|bth b|||
||b||pm||th,n th,pm n|n||
||f|tb||n∈N||||
||b|||||||
|th,f|th,t|||||||
|n|n|||||||

*v* = *h f − h t* = *r q ∀b ∈B* (7.6b) *π*(*d*) *b b* X <u>−g</u> *ets* *p₁* = *q* 2*h* + ∆*h* (7.6c) *th* *η*

The indices *n* and *n* denote the nodes at “from” and “to” ends of branch *b*. The symbols *B* and *B* are the sets of all branches connecting to node *n* in “from” and “to” direction.

Then, the thermal power flow eq. (7.6) can be transformed into a vectorized notation as:

*th,n th,n th th,n th,f* ⊺ *th,f th,t* ⊺ *th,t* *p* = *q* ∆*h q* = *A q* + *A q* (7.7a)

*f/t th* *−*2<u>4</u> *th,f/t th,f/t th,t/f th,f/t th th,f/t* *v* = diag *d q A h − A h* = diag *q* diag *r q* *π* (7.7b) <u>−g</u>

|pm||th,n ⊺|ets||
|---|---|---|---|---|
||pm||||
|B ×1|||th,n th,n|N ×1|
||th|fr mn|B ×1 th,f th,t|N ×1 B ×N|

*p* = *q* 2*h* + ∆*h* (7.7c) *η*

*th,f/t f/tth* The vectors *q, v ∈* R denote the branch volume flow rate and branch fluid *th* velocity vectors in “from” and “to” direction. The vectors *q, p ∈* R are the *th* nodal volume flow rate and thermal power injection vectors, whereas *h ∈* R is the *th* nodal pessure head vector. The vectors *d,* ∆*h,* ∆*h ∈* R denote the branch pipe *th th* diameter, friction loss and minor loss vectors. The matrices *A, A ∈* R denote the branch incidence matrices in “from” and “to” direction. The corresponding vectors are defined as: h i h i h i h i *th,f/t th,f/t f/t f/t th th th* *q* = *q* *b* *v* = *v* *b* *d* = *dbr* = *rbth* *b∈Bthb∈Bthb∈Bthb∈Bth* (7.8a)

||h i||h i|||
|---|---|---|---|---|---|
|th,n|n th,n n∈N|th,n|th,n n n∈N|n n∈N||

*q* = *q p* = *p h* = [*h*] *th* (7.8b) *th th*

Further, the definition of the branch incidence matrices follows from eq. (7.6) as: ( h i 1 for *n* = *n* *f* *th,f th,f th,f b* *A* = *a* *b,n* *a* *b,n* = (7.9a) (*b,n*)*∈Bth×Nth*0 otherwise ( h i 1 for *n* = *n* *t* *th,t th,t th,t b* *A* = *a* *b,n* *a* *b,n* = (7.9b) (*b,n*)*∈Bth×Nth*0 otherwise

<u>7. Thermal grid modeling 7.1. Fundamental thermal grid model</u> Lastly, eq. (7.7) can be slightly simplified due to the relationship *q*
*th,t* = *−q* *th,f* as follows:

*th,n th,n th th,n th,b* ⊺ *th,b* *p* = *q* ∆*h q* = *A q* (7.10a)

*b th −*2<u>4</u>*th,b th,b th,b th th,b* *v* = diag(*d*) *q A h* = diag *q* diag *r q* (7.10b) *π* <u>−g</u>

||||pm|th,n|⊺|ets||
|---|---|---|---|---|---|---|---|
||th,b|th,f|th,t|pm||||
|f|t|||||th,b|th,f|

*p* = *q* 2*h* + ∆*h* (7.10c) *η*

Here, the vector *q* = *q* = *−q* denotes the branch volume flow vector and the vector *v* *b* = *v* = *−v* denotes the branch fluid velocity vector. The matrix *A* = *A − A* *th,t* denotes the branch incidence matrix.

##### 7.1.3 Pipe pressure loss model

The pipe pressure loss model describes the hydraulic head loss in pipes of the thermal grid. Based on [39, p. 8, Section 2.1.4], the head losses in pipes can be divided into 1) friction losses and 2) minor losses. Friction losses result from shear stresses between the viscous fluid and the pipe walls, whereas minor losses occur due turbulence at flow deviations, e.g. curved pipe fittings, junctions or valves [36, p. 102].

Recall that the head loss ∆*h* *ls* *b* of pipe *b* is defined with a head loss model similar to [72], [84], where the scalar *r* *bth* denotes the loss coefficient:

||ls|th,f|2|
|---|---|---|---|
||b|bth b||

##### ∆h = r q (7.11a)

Further, the head loss is formed by the sum of friction and minor losses as:

|||ls|fr|mn||
|---|---|---|---|---|---|
|||b|b|b||
|fr|mn|||||
|b|b fr b|mn b|||th,f b|

##### ∆h = ∆h + ∆h (7.12a)

The symbols ∆*h* and ∆*h* describe the friction head losses and minor head losses at branch *b*. Note that losses ∆*h* and ∆*h* correlate with the branch volume flow rate *q*.

Friction losses can be modeled with the Darcy-Weisbach equation as:

<u>l</u> *th* 2 *fr fr* <u>b</u> *f* ∆*h* *b* = *f* *b th* *v* *b* (7.13a) 2*d* *b* *g*

The symbols *l* *bth* and *d* *th* *b* denote the length of the branch and its pipe diameter. The scalar *fr* *f* *b* denotes the friction factor of branch *b*, which is a non-linear expression of fluid velocity, fluid viscosity and pipe properties depending on the flow regime, i.e. different approximations apply for laminar and turbulent flow. At laminar conditions, the friction factor can be described with the correlation in eq. (7.14a). In the turbulent flow regime, the friction factor can be approximated with the Swamee-Jain formula [35, p. 34] in eq. (7.14b). The definition of the friction factor follows as:

*fr*<u>64</u> *f* *b* = for 0 *≤ Reb≤* 4000 (7.14a) *Reb*

<u>7. Thermal grid modeling 7.1. Fundamental thermal grid model</u>
<u>. ε</u> *th* *fr −* <u>b</u> *−* *f* *b* = *th* 2 for 4000 *≤ Reb≤* and 10 *≤* *th* *≤* (7.14b) <u>ε</u> <u>b 5.74</u>*db* ln

3*.*7*dth* + (*Re*)0*.*9 *b b*
*f th* <u>v</u> <u>b</u> <u>d</u> <u>b</u> *Reb*= *fl* (7.14c) *ν*

The symbol *Reb*denotes the Reynolds number of the flow at branch *b*. The scalars *ν* *fl*, *d* *th* *b* and *ε* *th* *b* are the fluid viscosity, pipe diameter and pipe wall roughness at branch *b*. The 8 *−*6 <u>ε</u> *th* <u>b</u> *−*2 conditions 4000 *≤ Reb≤* 10 and 10 *≤* *d* *th≤* 10 describe the validity range of the *b* Swamee-Jain formula, which is expected to hold for typical operating conditions of district heating / cooling systems. Within the validity range, Swamee-Jain formula stays within one percent of accuracy to the Colebrook-White equation. The latter is a more precise implicit expression of the friction factor but is avoided in water system simulation tools due to requiring iterative solution [35, p. 34]. Note that in the laminar flow regime, the friction loss *fr* *h* *b* becomes a linear expression of the fluid velocity by inserting eq. (7.14a) in eq. (7.13). However, the laminar flow regime is rare under typical operating conditions in district heating / cooling systems [161, p. 17].

##### Minor losses can be expressed as:

*f* 2 *v* <u>b</u> ∆*h* *mn* *b*= *fbmn*(7.15a) 2*g*

The scalar *f* *bmn* denotes the minor loss coefficient at branch *b*. Values for minor loss coefficients can be obtained based on the type of fittings along the branch, e.g. given in [35,

p. 41, Table 2.6].
*f* <u>4qb</u> *th,f* Finally, the loss coefficient *r* *bth* can be derived based on eqs. (7.11) to (7.15) and *v* *b* = *π*(*dth*)2 *b* as:

|||8l|8||
|---|---|---|---|---|
|fr,rf b|fr,rf b|bth th 5 2 b|th 4 b|2|
|th,b,nm||||b,nm|
|b||||b|

*r* *bth*= *f* + *fbmn*(7.16a)

(*d*) *π g* (*d*) *π g*
Note that *f* is the friction factor of branch *b* at reference conditions, i.e. for nominal branch flow *q* and corresponding nominal fluid velocity *v*. This approximation of the friction factor based on [72] introduces a small error, which is neglectable under the assumption that the branch flow remains relatively close to the nominal branch flow under operating conditions.

##### 7.1.4 DER connection

Thermal DERs are connected to single nodes of the thermal grid, although multiple DERs can be connected to the same node. Furthermore, all DERs are described with constant power models, i.e. all DERs act as constant power sources or loads. Recall that by convention,

<u>7. Thermal grid modeling 7.1. Fundamental thermal grid model</u> thermal power injections are represented with positive power values and thermal loads are represented with negative power values.
*th,n Nth×*1 The nodal thermal power injection vector *p*

||||∈ R||as well as nodal volume flow rate||
|---|---|---|---|---|---|---|
|th,n|N ×1|th,n th,n|th,d th th,d th|th −1|th|D ×1|
|th,d|N ×D|||||th|
||th||||||

*th,n Nth×*1 *th Dth×*1 vector *q ∈* R are related to the DER power vector *p ∈* R as follows:

##### p = A p (7.17a)

##### q = A p ∆h (7.17b)

*th th* The matrix *A ∈* R is the DER mapping matrices. The symbol *D* denotes the set of DERs. The scalar ∆*h* denotes the enthalpy difference between primary and secondary side of the thermal grid.

The DER mapping matrix *A* *th,d* is defined as: ( h i 1 for *n* = *n* *th,d th,d th,d d*

|A =|a||a =|
|---|---|---|---|
|d|n,d (n,d)∈N|×D|n,d|

*n,d n,d* (7.18a) (*n,d*)*∈Nth×Dth*0 otherwise

The symbol *n* denotes the thermal grid node at which DER *d* is connected.

##### 7.1.5 Source connection

The source node of the thermal grid is characterized with a constant pressure head as:

*h* *sr* = 0 (7.19a)

The scalar *h* *sr* denotes source node pressure head. The nodal no-load pressure head of the thermal grid, i.e. assuming no injection or load from any DERs, follows simply as:

*h* *nl* = 0 (7.20a)

The vector *h* *nl* denotes no-load nodal pressure head vector.

##### 7.1.6 Source and no-source notation

For notational convenience in the formulation of power flow solution algorithms below, the following short-hand notations are defined for the source / no-source variable vectors:

|sr|sr ⊺|||ns|ns ⊺|||
|---|---|---|---|---|---|---|---|
|th,n,sr|sr ⊺ th,n|sr ⊺ th,d|th|th,n,ns|ns ⊺ th,n|ns ⊺ th,d|th|

*h* = (*A*) *h h* = (*A*) *h* (7.21a)

*p* = (*A*) *p* = (*A*) *A p p* = (*A*) *p* = (*A*) *A p* (7.21b)

*th*

|sr th,n,sr|N ×1|||
|---|---|---|---|
||ns sr|th,n ns|N /n ×1|

The scalars *h,p ∈* R denote the pressure head and thermal power injection *th sr* at the source node. The vectors *h, p ∈* R denote the nodal pressure head and thermal power injection vectors of no-source nodes, i.e. all nodes excluding the source node *n* *sr* itself. The matrices *A* and *A* denote the source and no-source mapping

<u>7. Thermal grid modeling 7.2. Non-linear power flow solution</u>
*th*

||sr|N ×1|
|---|---|---|
|N ×N|/n||
||th,d||

matrices, where *A ∈* R maps the source variables to the nodal variable vectors and *nsth th sr* *A ∈* R maps the no-source variables to the nodal variable vectors. The DER mapping matrices *A* is defined in section7.1.4

The source / no-source mapping matrices are defined as: ( *sr sr sr* 1 for *n* = *n* *sr*

|A =|a|||= a|
|---|---|---|---|---|
||n,1 n∈N|||n,1|
|ns|ns n ,n|(n ,n)∈N|×N /n|ns n ,n|

*n,*1 *n∈Nth n,*1(7.22a) 0 otherwise ( h i 1 for *n¹* = *n²* *A* = *a*1 2*a*1 2= (7.22b) 1 2 *th th sr* 0 otherwise

Correspondingly, the partial branch mapping matrices for source and no-source nodes are defined as:

*th,b,sr sr* ⊺ *th,b* *A* = (*A*) *A* (7.23a) *th,b,ns ns* ⊺ *th,b* *A* = (*A*) *A* (7.23b)

The matrices *A* *th,b,sr*, *A* *th,b,ns* are referred to as partial matrices because they contain distinct portions of the complete branch mapping matrix *A* *th,b*. In the special case that the source node phases are arranged to be the first entries in *N* *th*, these matrices can be interpreted similar to eq. (6.34):

*th,bA* *th,b,sr* *A* =*th,b,ns*(7.24a) *A*

That is, the partial mapping matrices represent a partitioning of the complete branch mapping matrix.

#### 7.2 Non-linear power flow solution

##### 7.2.1 Outline

The power flow solution describes the process of solving the power flow equations in eqs. (7.8) to (7.10), in order to obtain the state variables of the thermal grid according to section7.1.1. To this end, the power flow solution essentially is a simulation of the steady-state power flow. As a prerequisite for the power flow solution, recall from section7.1.4that DERs are described with constant power models, i.e. all DERs act as constant thermal power sources or loads. Furthermore, the following assumes that the source node of the thermal grid can be characterized with a constant pressure head according to section7.1.5.

The thermal power flow is essentially by inserting the DER thermal power vector *p* *th* into and the nominal source node head *h* *sr* into the power flow equations in eqs. (7.8) to (7.10). In the first step, a solution for the nodal pressure head vector *h* and the branch flow vector *q* *th,b* are obtained. The further state variables are then obtained as expressions of these two

<u>7. Thermal grid modeling 7.2. Non-linear power flow solution</u> variables according to eq. (7.25) below. An explicit solution can directly be obtained for radial networks as presented in section7.2.2. At the time of writing, MESMO only supports radial networks for both non-linear power flow and linear approximate modeling of thermal grids, such that the following is restricted to radial network configuration. Refer to [84] for a more comprehensive overview of other solution algorithms for meshed networks. Once a solution for the nodal pressure head vector and the branch flow vector is obtained, the branch velocity vector *v*
*b* and the pump power *p* *pm* can directly be obtained based on eq. (7.10) as:

<u>4</u>

|b|th −2|th,b|
|---|---|---|
|pm|th,n ⊺||

*v* = diag(*d*) *q* (7.25a) *π* <u>−g</u>*ets* *p* = *pm* *q* 2*h* + ∆*h* (7.25b) *η*

##### 7.2.2 Explicit method for radial networks

The thermal grid represents a radial network if it corresponds to a graph-theoretical tree *NthBthNth* as *N* = *N* + 1, i.e. the number of nodes *N* is higher by one than the number of *Bth* branches *N*. In this case, the branch volume flow rates can be obtained directly from the mass balance in eq. (7.10a), where the branch mapping matrix for no-source nodes *A* *th,b,ns* *Nth/nsr*=*NBth* becomes a square and invertible matrix because *N*. Therefore, the thermal power flow equations can be solved explicitly as:

*th,b th,b,ns* ⊺ *−*1 *th,n,ns th* *−*1 *q* = *A p* ∆*h* (7.26a)

The vector *p* *th,n* denotes the nodal thermal power injection vector of no-source nodes. The matrix *A* *th,b,ns* denotes the branch mapping matrix for no-source nodes. The scalar ∆*h* *th* denotes the enthalpy difference between primary and secondary side of the thermal grid.

Based on the branch flow vector *q* *th,b*, the nodal pressure head vector *h* can be obtained directly as:

||th,b,ns|−1|th,b|th th,b|
|---|---|---|---|---|
|sr|ns ns|sr sr|||
||sr|th,b,ns|−1||
|||th|||
|th,b|||||

*ns* *h* = *A* diag *q* diag *r q* (7.27a)

*h* = *A h* + *A h* (7.27b)

The vectors *h* *ns* denote the nodal pressure head vector of no-source nodes. The scalar *h* denotes the pressure head at the source node. Note the assumption of *h* *sr* = 0 from section7.1.5. The scalars *h* denote the pressure head and thermal power injection at the source node. Notice that the inversion *A* is only possible under the assumption of a radial network. The loss coefficient *r* is determined based on current branch flow vector *q* according to the pipe pressure loss model in section7.1.3. Lastly, the remaining state variables of the thermal grid are then derived according to eq. (7.25).

This method can be cast into the solution algorithm implemented in MESMO according to algorithm2.

7. Thermal grid modeling 7.3. Linear approximate model **Algorithm 2:** Thermal power flow solution based on the explicit method for radial networks **begin** initialization: *th,n th,d th th −*1 *q* = *A p* ∆*h*; **begin** explicit solution evaluation:

|th,b|th,b,ns|⊺ −1|th,n,ns|||
|---|---|---|---|---|---|
|||||th||
|ns|th,b,ns|−1|th,b||th th,b|
 *q* = *A q*; Evaluate loss coefficient vector *r* according to eqs. (7.14) to (7.16); *h* = *A* diag *q* diag *r q* **begin** result variable update:

||ns ns||
|---|---|---|
|b|th|−2 π 4 th,b|
|pm|−g th,n|⊺|
||η||
 *h* = *A h*; *v* = diag(*d*) *q*;
*ets* *p* =*pmq* 2*h* + ∆*h*;

#### 7.3 Linear approximate model

##### 7.3.1 Fundamental linear model

The linear thermal grid model formulates a linear representation of the non-linear power flow equations from eqs. (7.25) to (7.27). This forms the basis for the convex formulation of optimal operation problems in chapter9. Based on the type of approximation, the following linear models are distinguished:

- Linear model based on **global approximation** (section7.3.2), where the model repre- sents a secant plane between the no-load point and a reference point of the power flow manifold.
- Linear model based on **local approximation**, where the model represents a tangent plane at a reference point of the power flow manifold.
Note that MESMO currently only implements a global approximation method for radial networks, although future implementations for local approximations are anticipated and the fundamental linear model formulation is decoupled from the approximation methods.

For both approximation types, the linear thermal grid model is represented in terms of sensitivity matrices for changes in the thermal grid state variables with regards to changes in the DER power injection / load as: *th*

|t|rf|h,p th t||
|---|---|---|---|
|th,b|th,b,rf|q ,p|th|
|t|t||t|
|pm|pm,rf|p ,p|th|
|t|||t|
|t N|×1 tth|B ×1||

*h* = *h* + *M* ∆*p ∀t ∈T* (7.28a) *th,b th* *q* = *q* + *M* ∆*p ∀t ∈T* (7.28b) *pm th* *p* = *p* + *M* ∆*p ∀t ∈T* (7.28c)

*th thth* The vectors *h ∈* R, *q ∈* R are the pressure head at thermal grid nodes *n ∈N* and the branch volume flow rate at thermal grid branches *b ∈B* *th* for time step *t ∈T*. The

<u>7. Thermal grid modeling 7.3. Linear approximate model</u> *pm* scalar *pt*denotes the total pumping power demand for time step *t*. The reference point for
*rf th Dth×*1. The vector ∆*pt*

|each property is denoted by ()|||∈ R|is the thermal power change||||
|---|---|---|---|---|---|---|---|
|||th|h,p|N ×D|q|,p|B ×D|
|p|,p|1×D||th t|th t|th,rf||
|th|D ×1|||th,rf||||
|t||||t||||

*th h,pthNth×Dthqth,b,pthBth×Dth* at DERs *d ∈D* for time step *t*. The matrices *M ∈* R, *M ∈* R, *pm th th* *M ∈* R are the sensitivity matrices for the change of the respective properties to the thermal power change, which in turn is defined as ∆*p* = *p − p*. The vector *th* *p, ∈* R is the thermal power vector and the vector *p* is the thermal power reference vector.

Based on the linear thermal grid model, the operational constraints of the thermal grid are expressed as:

<u>1</u>*pm*

||th,sr|⊺ th|
|---|---|---|
|th,pm −|t|t|
|th,b,−|th,b|th,b,+|
||t||

*p −* 1 *p* = *p ∀t ∈T* (7.29a) *η* *h ≤ h ∀t ∈T* (7.29b)

*q ≤ q ≤ q ∀t ∈T* (7.29c)

##### 7.3.2 Global approximation for radial networks

*q* *th,b,pthh,pthppm,pth* A global approximation for the sensitivity matrices *M*, *M*, *M* can be obtained based on the explicit formulation of the thermal grid power flow problem eqs. (7.25) to (7.27). The global approximation essentially forms a linear expression as a tangent between the no-load point and the nominal operation point of the thermal grid for each non-linear model equation. The following formulations only apply for radial networks, i.e. *NthBth* *N* = *N* + 1, since they are based on the explicit solution method from section7.2.2.

To begin with, the sensitivities of the branch flow with respect to a change in the nodal volume flow injection can be derived from eq. (7.26) as:

|q ,q|th,b|⊺ −1|
|---|---|---|
||th,n,ns||

*th,b th,n,ns* <u>δq 1</u>*th,b,ns* *M* = = *th* *A* (7.30a) *δq* ∆*h*

Note that eq. (7.30) expresses the branch flow sensitivity with regards to the nodal volume flow injection vector *q* *th,n,ns*, whereas the fundamental linear model in eq. (7.28) is expressed

|||||th|δz|δz δx δy|
|---|---|---|---|---|---|---|
||||||δx|δy|
|q ,p|th,b th|th,b th,n,ns|th,n,ns th|q ,q|ns ⊺ th,d||

with regards to the DER thermal power vector *p* *th*. With the chain rule <u>δz</u> = <u>δz</u> *δx* <u>δy</u>, the according representation of the branch flow sensitivity is obtained as:

*th,b th δq δq δq th,b th,n,ns* 1 *M* = = = *M* *th*

(*A*) *A* (7.31a)
*δp δq δp* ∆*h*

Then, the sensitivities of the nodal pressure head with regards to the DER thermal power

||δz|δz δx δy||
|---|---|---|---|
||δx|δy||
|th,b th|ns th,b,ns|−1|q ,p|

vector are represented using the chain rule = as:

*h,pth* <u>δh δh δq</u>*th,rfth,b th* *M* = *th* = *th,b* = *A A* diag *r M* (7.32a) *δp δq δp*

<u>7. Thermal grid modeling 7.3. Linear approximate model</u> Note that this expression approximates the loss coefficient at reference conditions *r*
*th* = *th,rf h,pth* *r* to retain *M* as a constant value. This approximation is suitable for the global approximation because the branch flow losses are monotonically increasing for the pipe pressure loss model presented in section7.1.3.

Lastly, the sensitivities of the pump power with regards to the DER thermal power vector are represented by once again using the chain rule *δx* <u>δz</u> = *δy* <u>δz</u> *δx* <u>δy</u> as:

||pm||||⊺|
|---|---|---|---|---|---|
|p ,p|th|pm|th,d th|th,rf|h,p|

*pm* *pm th δp δp δh −*2*g* 1 *th* *M* = = *th* = *A p M* (7.33a) *δp δh δp η* ∆*h*

This expression approximates the nodal volume flow at reference conditions by taking *th th,rf ppm,pth* *p* = *p* to retain *M* as a constant value. This approximation is suitable for the global approximation because the pumping losses are monotonically increasing with the DER power demand.

## 8 Distributed energy resource modeling

#### Contents

8.1 Fundamental DER model............................. 111
8.1.1 Scope and assumptions......................... 111
8.1.2 Fixed DER model............................. 111
8.1.3 Flexible DER model.......................... 112
8.2 Fixed DERs.................................... 114
8.2.1 Fixed loads................................ 114
8.2.2 Fixed EV chargers............................ 114
8.2.3 Fixed generators............................. 114
8.3 Flexible DERs................................... 114
8.3.1 Flexible loads............................... 114
8.3.2 Flexible generators........................... 116
8.3.3 Flexible EV chargers........................... 117
8.3.4 Flexible buildings............................. 121
8.3.5 Storage systems............................ 129
8.3.6 Cooling plants.............................. 131
8.3.7 Heating plants............................. 133
**Outline and contributions**

This chapter presents the mathematical formulations for DER models, which are distinguished into fixed and flexible DERs. The chapter begins by outlining fundamental model formats for fixed DERs and flexible DERs. Then, the specific models for individual DER types are successively developed.

The fundamental fixed and flexible DER model representations in this chapter have been chosen to suit the modeling framework of MESMO. However, these representations do not differ significantly from the prevailing formulation in previous works. Nevertheless, note the important choice for keeping flexible DER models in state-space form for notational coherence across all DER types, inspired by works in the building modeling domain [42], [43]. As minor original contributions, the models for fixed loads, fixed EV chargers, fixed generators, flexible loads, flexible EV chargers and flexible generators have been developed as part of this thesis.

<u>8. Distributed energy resource modeling 8.1. Fundamental DER model</u> The flexible building model is an original work of the author but has primarily been developed as part of the author’s master thesis in [44]. As part of this Ph.D. thesis, the model was implemented and published in the Control-oriented Building Model (CoBMo) toolbox in [45], which includes contributions from supervised master students in [46]–[49]. The storage system, cooling plant and heating plant models are original but minor contributions of this thesis, whose development was supported through two supervised master theses [39], [40].
#### 8.1 Fundamental DER model

##### 8.1.1 Scope and assumptions

The focus of DER modeling with regards to MESMO is to express DER’s power injection or load based on its operation constraints. In this context, the term “DER” refers to any type of energy system which is connected to the district-scale electric grid or thermal grid, e.g. loads, generators as well as ESSs. MESMO distinguishes 1) fixed DERs and 2) flexible DERs. Fixed DERs are uncontrollable from the district-scale system operation perspective, i.e. these DERs follow a fixed dispatch schedule. Conversely, flexible DERs refer to controllable energy systems with the ability to adjust their dispatch schedule. Fixed DERs are modeled with time series models, whereas flexible DERs are represented with state-space models in MESMO. Note that this constrains the DER modeling in MESMO to strictly linear mathematical models.

The following model variables are considered for DERs:

- DER active / reactive vector *p* / *q*, i.e. the interconnection to the electric grid (see section6.1) •DER thermal vector *p*
*th*, i.e. the interconnection to the thermal grid (see section7.1)

##### •State vector x

##### •Output vector y

##### •Control vector c

##### •Disturbance vector d

##### 8.1.2 Fixed DER model

Fixed DERs are represented with time series models, where fixed nominal power schedules are taken as input. To this end, the fixed DER model assumes that the dispatch schedule for DER power injection or load is predetermined.

The input power values *p* *in* *t*for time series models can be provided to MESMO in two definition formats:

- **Time series** format¹, where the time steps *t ∈* T (seeNotation) are directly interpreted as date / time. 1 [https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-timeseries](https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-timeseries)
111

<u>8. Distributed energy resource modeling 8.1. Fundamental DER model</u>
- **Schedule** format², where input values *p*
*in* *t*are defined as daily and weekly recurring schedule. Therefore, *t ∈* P (seeNotation) is interpreted as weekly recurring time period.

Furthermore, the input power values *p* *in* *t*can be given as 1) absolute values or 2) per-unit values. Absolute values are directly interpreted as power values, whereas per-unit values are interpreted as *p* *in* *t∈* [0*,*1] in per-unit of the nominal power of each DER. For absolute-valued inputs in time series format the values are directly mapped to the DER power values as:

*el in el* <u>q</u> <u>d</u> *nm* *in* *pd,t*= *adpd,tqd,t*= *ad* *nm* *pd,t∀t ∈T* (8.1a) *p* *d* *p* *th* *d,t*= *a* *th* *dp* *in* *d,t∀t ∈T* (8.1b)

The scalars *pd,t*, *qd,t*and *p* *th* *d,t* denote the active power, reactive power and thermal power of DER *d ∈D* at time step *t ∈T*. The symbols *a* *el* *d* *,a* *th* *d* *∈{*0*,*1*}* denote whether DER *d* is connected to the electric grid *a* *el* *d* = 1 or the thermal grid *a* *th* *d* = 1. The scalars *p* *nm* *d*, *q* *dnm* and *th,nm* *p* *d* denote the nominal active power, nominal reactive power and nominal thermal power of DER *d*. The input power value is denoted with *p* *in* *d,t*. The symbols *D* and *T ⊂* T describe the set of DERs and time steps in the current scenario.

For per-unit input in time series format, the definition changes slightly to:

*el nm in el* <u>q</u> <u>d</u> *nm* *in* *pd,t*= *adpdpd,tqd,t*= *adqdnm* *nm* *pd,t∀t ∈T* (8.2a) *p* *d* *th th th,nm in* *pd,t*= *adp* *d* *pd,t∀t ∈T* (8.2b)

*th,nm* The scalar *p* *d* denotes the nominal thermal power of DER *d*.

For inputs in schedule format, the input values *p* *in* *d,tin* are given for time periods *t* *in* *∈* P. However, the nominal power time series values *pd,t*, *qd,t*, *p* *th* *d,t* are defined for time steps *t ∈* T. To this end, the input values are first transformed from schedule format to time-series format, where each time-series value *p* *in* *d,t* is obtained from the corresponding schedule value *p* *in* *d,tin*. This can be represented as *p* *in* *d,t* = *p* *in* *d,tin*(*t*), where *t* *in*

(*t*) : T *→* P denotes the mapping from
time steps to time periods. Then, *p* *in* *d,tin*(*t*) can be inserted into eqs. (8.1) and (8.2) to obtain the nominal power time series for active, reactive and thermal power.

##### 8.1.3 Flexible DER model

Flexible DERs are represented with state-space models, which encapsulate the system dynamics of the DERs into a standardized representation as:

*xd,t*0 = *x⁰*<u>d</u>*∀d ∈D* (8.3a) 2 [https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-schedules](https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-schedules)

<u>8. Distributed energy resource modeling 8.1. Fundamental DER model</u>
##### ∀d ∈D, ∀t ∈T /t

||x = A|x|+ B c|+ B d||(8.3b)|
|---|---|---|---|---|---|---|
|d dd d|d,t+1 d,t d,t − d,t d,t d,t|d d,t d d,t d,t + d,t|dc d,t d c d,t d,t|dd d,t d d d,t d d|N|dc d c|
|−|+||||||
|d,t|d,t|N|||d,t||

*y* = *C x* + *D c* + *D d ∀d ∈D, ∀t ∈T* (8.3c) *y ≤ y ≤ y ∀d ∈D, ∀t ∈T* (8.3d)

The vectors *y*, *x*, *c* and *d* are the output, state, control and disturbance vectors for DER *d* at time step *t*. The matrices *A*, *C* are the state and output matrix, and *B*, *D*, *B*, *D* are the control and feed-through matrices, on the control and disturbance vectors respectively. The vector *x⁰* is the initial state vector at the initial time step *t⁰* in *T*. The vectors *y* and *y* denote the lower and upper bounds on the output vector for each time step *t*. The symbol *t* denotes the final time step in *T*. Note that *x⁰* and *d* are fixed parameter vectors. Further, note that this representation of the state-space model assumes a time-discrete formulation of the model matrices.

Alternatively, a flexible DER model may initially be expressed in continuous-time formulation of the state-space model as:

||cnt|c,cnt|d,cnt|
|---|---|---|---|
|d|d d|d|d d|
|d|d|c d|d d|
|d d|d d|||
|||cnt||

*x*˙ = *A x* + *B c* + *B dd∀d ∈D* (8.4a)

*y* = *Cx* + *D c* + *D d ∀d ∈D* (8.4b)

The vectors *x*, *c*, *d*, *y* are the continuous-time state, control, disturbance and output vectors of DER *d*. The symbol () denotes the continuous-time instances of the respective matrices. The time-discrete state-space matrices can then be obtained from their continuous- time counterparts by application of zero-order hold discretization: *cnt*

|d|A ∆t|||
|---|---|---|---|
||cnt −1||c,cnt|
|dc|d cnt −1|d|d d,cnt|
|dd|d|d|d|

()

*A* =*ed∀d ∈D* (8.5a)

*B* = *A* (*A − I*)*B ∀d ∈D* (8.5b)

*B* = *A* (*A − I*)*B ∀d ∈D* (8.5c)

The symbols *e* and *I* denote the matrix exponential function and the identity matrix of appropriate size.

The active, reactive and thermal power are implicitly defined in the output vector *yt*in eq. (8.4). For notational convenience, the mapping from the output vector to the power vectors is expressed as:

||p,y||q,y||
|---|---|---|---|---|
|d,t|d d,t|d,t|d d,t||
|th|p ,y||||
|d,t|d d,t p,y q,y d d|p ,y d||th|
|d,t||p,y d|q,y d|t t t|
||p ,y||||
||d||||

*p* = *M y q* = *M y ∀d ∈D, ∀t ∈T* (8.6a) *th* *p* = *M y ∀d ∈D, ∀t ∈T* (8.6b)

*th* The matrices *M*, *M* and *M* are the mapping matrices for relating the output vector *y* to the active, reactive and thermal power vectors *p, q, p ∈* R *d*. If DER *d* is not connected to the electric grid, then *M, M* = 0, and if the DER is not connected to the *th* thermal grid, then *M* = 0.

<u>8. Distributed energy resource modeling 8.2. Fixed DERs</u>
#### 8.2 Fixed DERs

##### 8.2.1 Fixed loads

The fixed load model represents generic loads with uncontrollable active, reactive and thermal power demand. Fixed loads can be connected to either the electric grid or the thermal grid but not to both grid types simultaneously. The model formulation follows the fundamental fixed DER model in eqs. (8.1) and (8.2).

##### 8.2.2 Fixed EV chargers

EV charging stations with uncontrollable active and reactive power demand are described with the fixed EV charger model. This DER type can only be connected to the electric grid. The fixed EV charger model formulation follows the fundamental fixed DER model in eqs. (8.1) and (8.2) and relies on input data for the nominal active / reactive power demand time series. More specifically, the model does not include any form of mobility modeling. Instead, such mobility simulations should be referred to dedicated mobility simulation tools, e.g. the City Mobility Simulator (CityMoS) [162], [163]. For the study presented in chapter10, synthetic charging demand data was generated through a carpark-based vehicle flow and charging simulation.

##### 8.2.3 Fixed generators

The fixed generator model describes such energy systems with pre-determined power production schedule, i.e. fixed active, reactive and thermal power injections. Fixed generators can be connected to either the electric grid or the thermal grid but not to both grid types simultaneously. In addition to the fundamental fixed DER model in eqs. (8.1) and (8.2), the *mar* fixed generator model defines the marginal cost of production *c*. *d*

#### 8.3 Flexible DERs

##### 8.3.1 Flexible loads

The flexible load model describes generic loads with controllable active, reactive and thermal power demand. The model formulation assumes that the DSF is characterized in terms of

1) the maximum load shifting period and 2) the maximum power deviation. Similar to fixed loads, flexible loads can be connected to either the electric grid or the thermal grid but not to both grid types simultaneously.
##### Fundamental model

As a starting point, consider the differential equation of the consumed energy *ed*of the flexible load *d* as:

*bas* *e*˙*d*= *pd− pd*(8.7a)

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> The scalars *pd*and *p*
*bas* *d* denote the instantaneous power demand and baseline power demand of flexible load *d*. The baseline power demand refers to the projected nominal power time series of the load, which is defined according to eqs. (8.1) and (8.2). To this end, the flexible load model inherits the nominal power time series formulation from the fixed load model.

Assuming a constant time step length ∆*t*, the time-discrete version of eq. (8.7) is obtained as:

*ed,t*+1= *ed,t*+ ∆*t pd,t− p* *bas* *d,t∀t ∈T /t* *N* (8.8a)

The indices ()*t,*()*t*+1denote the current and the next time step respectively. The scalar ∆*t* denotes the time step interval.

The operational constraints are expressed as: *pu nm pu nm* *−e* *d* *|pd|*∆*t ≤ ed,t≤ e* *d* *|pd|*∆*t ∀t ∈T* (8.9a) *−,pu bas* +*,pu bas*

|||−p|p ≤−p|≤−p||p||∀t ∈T|(8.9b)|
|---|---|---|---|---|---|---|---|---|---|
|||d|d,t|d,t|d|d,t||||
||pu d||||pu d d,t|bas d,t|−,pu d nm d|nm +,pu d d|pu −,pu|
|+,pu d|||||||||d d|

*d d,t d,t d d,t*

The scalar *e* denotes the per-unit energy storage capacity of the flexible load, i.e. the maximum load shifting time period, where *e* = h. The scalar *p* denotes the nominal power demand of the flexible load *d*. The symbols *p* and *p* denote the per-unit minimum and maximum power demand, i.e. the upper and lower bound on the deviation from the baseline power demand. Note that *p*, *p* and *p* are negative values because MESMO represents loads with negative power values by convention, whereas *e*, *p* and *p* are positive values.

The flexible load model applies for both electric and thermal loads. Therefore, the power value *pd,t*can characterize both active and thermal power, depending on whether the load is connected to the electric grid or the thermal grid. Accordingly, the baseline power demand *p* *bas* *d,t* will characterize either the nominal active power time series or nominal thermal power time series based on eqs. (8.1) and (8.2). If the flexible load is connected to the electric grid, he reactive power value is defined through the mapping matrix (see eq. (8.12)), thus assuming a fixed power factor.

##### State-space model

The flexible load model is transformed into a state-space model according to eq. (8.3) by arranging the model variables into vectors and the model parameters into appropriate matrices. To this end, the state-space formulation is simply a representation of the differential equation for the consumed energy in eq. (8.8), where the model variables are arranged into the state-space vectors:

*based,t* *xd,t*= *ed,tcd,t*= *pd,tdd,t*= *pd,tyd,t*= *∀t ∈T* (8.10a) *pd,t*

The entries of the state-space matrices are derived accordingly from eqs. (8.8) and (8.9) as:

*Ad*= 1 *Bdc*= ∆*t Bdd*= ∆*t* (8.11a)

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u>

||1||0||0||
|---|---|---|---|---|---|---|
|d,t||d c|pu nm|d d|pu nm||
|0 d|d,t|d,t +|−d,pu dbas d d,t|d,t −|+ d,pudbas d d,t||
|||||||N|
|d|d,t||||||
 *C* = *D* = *D* = (8.11b)
0 1 0 *−e |p | e |p |* *x* = *e N y* = *y* = *∀t ∈T* (8.11c) *p p p p*

Note that *x⁰* = *e N* links the initial state to the final at time step *t*.

Lastly, the mapping matrices are defined as: h*nm*i *th*

||p,y|el|q,y|el q|p|,y|th|
|---|---|---|---|---|---|---|---|
||d|d|d|d p|d||d|
|||el th||||||
|el||d d|th||nm|||
|d|||d||d|dnm||

<u>d</u> *M* = 0 *a M* = 0 *anm M* = 0 *a* (8.12a) *d*

The symbols *a,a ∈{*0*,*1*}* denote whether flexible load *d* is connected to the electric grid *a* = 1 or the thermal grid *a* = 1. The scalars *p* and *q* denote the nominal active power and nominal reactive power of DER *d*.

##### MESMO implementation

The state-space form of the flexible load model has been implemented in MESMO as FlexibleLoadModel³. The corresponding model data definition is documented in the MESMO data reference⁴.

##### 8.3.2 Flexible generators

The flexible generator model describes energy systems with controllable power production schedule, i.e. fixed active, reactive and thermal power injections. The model formulation assumes that the flexible dispatch is simply constrained by maximum and minimum production limits. Flexible generators can be connected to either the electric grid or the thermal grid but not to both grid types simultaneously.

##### Fundamental model

The operational constraints of the flexible generator model are formulated as:

*−,pu bas* +*,pu bas* *p* *d* *pd,t≤ pd,t≤ p* *d* *pd,t∀t ∈T* (8.13a)

The scalar *p* *bas* *d,t* denotes the baseline power injection of flexible generator *d* at time step *t*. The baseline power demand refers to the projected nominal power time series of the generator, *−,pu* +*,pu* which is defined according to eqs. (8.1) and (8.2). The symbols *p* *d* and *p* *d* denote the per-unit minimum and maximum power injection, i.e. the upper and lower bound on the deviation from the baseline power production. Note that *pd,t*and *p* *bas* *d,t* are positive values because MESMO represents injections with positive power values by convention. Similarly *−,pu* +*,pu* *p* <u>d</u> and *p* <u>d</u> are positive values by definition. 3 mesmo.der_models.FlexibleLoadModel 4 [https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models](https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models)

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> The flexible generator model applies for both electric and thermal energy systems. Therefore, the power value *pd,t*can characterize both active and thermal power, depending on whether the generator is connected to the electric grid or the thermal grid. Accordingly, the baseline
*bas* power production *p* will characterize either the nominal active power time series or nominal *d,t* thermal power time series based on eqs. (8.1) and (8.2). If the flexible generator is connected to the electric grid, he reactive power value is defined through the mapping matrix (see eq. (8.16)), thus assuming a fixed power factor.

##### State-space model

The flexible load model is transformed into a state-space model according to eq. (8.3) by arranging the model variables into vectors and the model parameters into appropriate matrices as:

*xd,t*= [] *cd,t*= *pd,tdd,t*= [] *yd,t*= *pd,t∀t ∈T* (8.14a)

Since the flexible generator model does not include a differential equation nor disturbances, the state vector *xd,t*and disturbance vector *dd,t*do not contain any variables. The entries of the state-space matrices are derived from eq. (8.13) as:

(8.15a)

|A = []|B = []|||B = []|||
|---|---|---|---|---|---|---|
|d|dc|||dd|||
|d,t|d c|||d d|||
|0|+|+,pu|bas|−|−,pu|bas|
|d|d,t|d|d,t|d,t|d|d,t|

*C* = [] *D* = 1 *D* = [] (8.15b) h i h i *x* = [] *y* = *p p y* = *p p ∀t ∈T* (8.15c)

Lastly, the mapping matrices are defined as: h*nm*i *th*

|p,y|el|q,y|el q|p ,y|th|
|---|---|---|---|---|---|
|d|d|d|d p|d|d|
||el th|||||
|el|d d|th||nm||
|d||d||d|dnm|

<u>d</u> *M* = *a M* = *anm M* = *a* (8.16a) *d*

The symbols *a,a ∈{*0*,*1*}* denote whether flexible generator *d* is connected to the electric grid *a* = 1 or the thermal grid *a* = 1. The scalars *p* and *q* denote the nominal active power and nominal reactive power of DER *d*.

##### MESMO implementation

The state-space form of the flexible generator model has been implemented in MESMO as FlexibleGeneratorModel⁵. The corresponding model data definition is documented in the MESMO data reference⁶.

##### 8.3.3 Flexible EV chargers

EV charging stations with controllable active and reactive power demand are described with the flexible EV charger model. This DER type can only be connected to the electric grid. The 5 mesmo.der_models.FlexibleGeneratorModel 6 [https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models](https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models)

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> DSF of flexible EV chargers is characterized by the V2G capabilities of chargers and vehicles. V2G capabilities can be categorized into 1) smart charging / unidirectional V2G as well as 2) V2G charging / bidirectional V2G. To this end, smart charging refers to ability to control the charging power demand schedule, whereas V2G charging describes the ability to control the bidirectional exchange of electric power between the vehicle and the electric grid, i.e. both charging and discharging. Flexible EV chargers can be described as a superposition of flexible load, i.e. the smart charging component, and energy storage system, i.e. the V2G charging component. The operational flexibility in V2G-enabled EV charging arises from the control of charging and discharging power, subject to EV battery capacity limits, energy demand requirements and vehicle availability, where the latter are governed by user preference. This can be translated into constraints on the charged energy, the charging power and discharging power. For this purpose, the charged energy refers to the net energy which is supplied to the vehicle as a function of charging and discharging power schedules.
##### Vehicle-based model

As a starting point, the differential equation of the charged energy *ev*of vehicle *v* is expressed as:

<u>1</u> *e*˙*v*= *η* (8.17a)

|||p −||p||
|---|---|---|---|---|---|
|||dch ch v|dch|dch v||
||||d|||
|ch v|dch v||||d|
|d|||||dch|

*η*

The scalars *p* and *p* are the charging power and discharging power of vehicle *v ∈V*. The symbol *V* is the set of all vehicles *v* which charge at charging station *d*. The scalars *η* and *η* *ddch* are the charge and discharge efficiencies of charging station *d*. In the context of MESMO, each charging station refers to one DER *d*, where each charging station may be equipped with several chargers with the same characteristics *η* *ch* and *η* *dch*.

Assuming a constant time step length ∆*t*, the time-discrete version of eq. (8.17) is obtained as:

<u>1</u>*N* *∀t ∈T /t* (8.18a)

|e = e|+ ∆t|η p −|p|
|---|---|---|---|
|v,t+1|v,t|dch ch v,t|dch dch v,t|
||||d|
|t|t+1|||

*η*

The indices ()*,*() denote the current and the next time step respectively. The scalar ∆*t* denotes the time step interval.

The operational constraints can be formulated as:

*ch*

|0 ≤ p|≤ α|p||||
|---|---|---|---|---|---|
||dch v,t|v,t v dch,max v||||
|v,t||||arr|dep|
|v,t||||arr|dep|
|v,t min v|v,t|v max v|v min v|||

*v,t v,t* *ch,max* *v∀t ∈T* (8.19a) 0 *≤ p* *dch* *≤ α γ p* *dch,max* *∀t ∈T* (8.19b)

*α* = 0 *∀t ∈{t ∈T|t < t,t > t}* (8.19c)

*α* = 1 *∀t ∈{t ∈T|t ≤ t ≤ t}* (8.19d)

*β e ≤ e ≤ γ e* + (1 *− γ*)*e ∀t ∈T* (8.19e)

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> *βv,t*= 0 *∀t ∈{t ∈T|t < t*
*dep* *}* (8.19f)

*βv,t*= 1 *∀t ∈{t ∈T|t ≥ t* *dep* *}* (8.19g)

The scalars *αv,t*and *βv,t*are indicator variables for the arrival and departure of vehicle *v* at time step *t*. That means *αv,t*= 1 only when the vehicle have arrived and not yet departed at the charging station and *βv,t*= 1 only when the vehicle has departed from the charging station. The scalar *γv*denotes the participation in bidirectional V2G charging of vehicle *v*, *ch,max dch,max*

i.e. discharging of vehicle *v* is only permitted if *γv*= 1. The scalars *pv*and *pv* describe the maximum permitted charging and discharging power of vehicle *v* according to the technical limitations of the vehicle and the charger. The scalars *e*
*min* *v*and *e* *max* *v*are the minimum required charged energy and the maximum permitted charged energy of vehicle *v*. Note that *e* *min* *v*will only be enforced once the vehicle departs and *e* *max* *v*will only be different from *e* *min* *v*if the vehicle participates in bidirectional V2G.

##### Charging-station-based model

The above model description was from a vehicle perspective and may result and a high dimension of the decision variables. To reduce the computational burden, the V2G EV charging model is aggregated for each charging station in the following. To this end, the time-discrete differential equation of the total aggregated charged energy *e* *tot* *d,t* of all vehicles at charging station *d* is formulated as:

*tot tot ch*<u>1</u>*dch N* *ed,t*+1= *ed,t*+ ∆*t ηdchpd,t−* *dch* *pd,t∀t ∈T /t* (8.20a) *η* *d*

The scalars *p* *ch* *d,t* and *p* *dch* *d,t* are the total aggregated charging power and discharging power of all vehicles at charging station *s*. The scalars *η* *dch* and *η* *ddch* are the charge and discharge efficiencies.

Equation (8.20) is further reformulated to avoid a continuously increasing value of *e* *tot* *d,t*+1 when considering a large time horizon, which could cause numerical issues. To this end, the charged energy *ed,t*+1of all presently connected vehicles at charging station *d* is expressed as: <u>1</u>*N* *∀t ∈T /t* (8.21a)

|e = e|+ ∆t|η p −|p|− e|
|---|---|---|---|---|
|d,t+1|s,t|dch ch d,t|dch dch d,t|dep d,t|
||||d||
|dep|||||
|d,t|||||
||d,t+1||||

*η*

The scalar *e* is the charged energy of vehicles departing in time step *t*. Thus, the charged energy of departing vehicles is continuously “removed” from the charging station in order to keep the value of *e* within a reasonable order of magnitude.

##### The operational constraints are formulated as:

||ch|ch,max|||
|---|---|---|---|---|
||d,t|d,t|||
|ch,max|||ch,max|ch,max|
|d,t|||v,t v|d|
|||v∈V|||

0 *≤ p ≤ p ∀t ∈T* (8.22a)    X   *p* = min  *α p,p ∀t ∈T* (8.22b) *d*

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u>
*dch dch,max* *≤ pd,t≤ p* *d,t* *∀t ∈T* (8.22c)    X *dch,max dch,max*  *dch,max*  *p* *d,t* = min  *γvαv,tpv,p* *d* *∀t ∈T* (8.22d) *v∈Vd* X *dep min* *e* *d,t* = *δv,tev∀t ∈T* (8.22e) *v∈Vd* 0 *≤ ed,t≤ e* *max* *d,t∀t ∈T* (8.22f) X *e* *max* *d,t*= *αv,tγve* *max* *v*+ (1 *− γv*)*e* *min* *v∀t ∈T* (8.22g) *v∈Vd* *δ* *v,t*= 0 *∀t ∈{t ∈T|t ̸*= *t* *dep* *} ∀t ∈T* (8.22h)

*δ* *v,t*= 1 *∀t ∈{t ∈T|t* = *t* *dep* *} ∀t ∈T* (8.22i)

*ch,max dch,max* The scalars *p* *d* and *p* *d* describe the maximum permitted charging and discharging power at charging station *d* with respect to the number of provisioned chargers and other technical limitations. The scalar *δv,t*denotes whether vehicle *v* is departing in a particular time step *t*, i.e. *αv,t*= 1 only in the time step *t* in which the vehicle *v* is departing or disconnecting from the charging station. Other symbols have been defined above for eq. (8.19).

##### State-space model

The charging-station-based model is transformed into a state-space model by arranging the model variables into vectors and the model parameters into appropriate matrices. To this end, the state-space formulation is simply a representation of the differential equation for the aggregated charged energy in eq. (8.21), where the model variables are arranged into the state-space vectors:

||||p||i h|
|---|---|---|---|---|---|
||tot||d,t||dep|
|d,t|d,t|d,t|dch|d,t|d,t|
||tot d,t ch|−|d,t|+|max ch,max d,t|
|d,t|d,t dch d,t|d,t||d,t|d,t dch,max d,t|

*tot* *ch* *d,t dep* *xd,t*= *ed,tcd,t*=*dchdd,t*= *e ∀t ∈T* (8.23a) *p*       *e* 0 *e*    *y* = *p y* = 0 *y* =  *p*  *∀t ∈T* (8.23b) *p* 0 *p*

The entries of the state-space matrices are derived accordingly from eqs. (8.21) and (8.22) but are omitted here for the sake of brevity.

The mapping matrices are defined as: h*nm nm*i *th* *p,y el el q,y el* <u>qd</u> *el* <u>qd</u>*p,y th th* *M* *d* = 0 *−a* *d* *a* *d* *M* *d* = 0 *−a* *d pnm* *a* *d pnm* *M* *d* = 0 *−a* *d* *a* *d* *d d* (8.24a)

|el th|||
|---|---|---|
|el d d|th|nm|
|d|d|d dnm|

The symbols *a,a ∈ {*0*,*1*}* denote whether flexible EV charger *d* is connected to the electric grid *a* = 1 or the thermal grid *a* = 1. The scalars *p* and *q* denote the nominal active power and nominal reactive power of flexible EV charger *d*.

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u>
##### MESMO implementation

The state-space form of the proposed charging-station-based model has been implemented in MESMO as FlexibleEVChargerModel⁷. The corresponding model data definition is documented in the MESMO data reference⁸, where the following supplemental time series inputs⁹ are required based on the above model definition:

1. Maximum charging power time series: Maximum permitted charging power at the charging station. This should be determined based on the rated power of available chargers and the number of vehicles connected to chargers at each time step as:
   X *ch,max ch,max*  *ch,max*  *p* *d,t* = min  *αv,tpv,p* *d* *∀t ∈T* (8.25) *v∈Vd*

2. Maximum discharging power time series: Maximum permitted discharging power at the charging station. This should be determined based on the rated power of available chargers and the number of vehicles connected to chargers at each time step as:
   X *dch,max dch,max*  *dch,max*  *p* *d,t* = min  *γvαv,tpv,p* *d* *∀t ∈T* (8.26) *v∈Vd*

3. Maximum energy time series: Maximum value of aggregated charged energy across all vehicles. This should be determined based on the battery size or energy demand of all vehicles connected to chargers at each time step as:
X

|max d,t|v,t v max v|v min v|
|---|---|---|
|v∈V|||

*e* = *α γ e* + (1 *− γ*)*e ∀t ∈T* (8.27) *d*

4. Departing energy time series: Aggregated energy demand of all departing vehicles. This should be determined based on the required energy of all vehicles which are departing from the charging station at each time step as:
X *dep min* *e* *d,t* = *δv,tev∀t ∈T* (8.28) *v∈Vd*

##### 8.3.4 Flexible buildings

The flexible building model describes building-level energy systems with the ability to control their active, reactive and thermal power demand. In the context on MESMO, the flexible building model is focused on demand side flexibility in HVAC systems. Nevertheless, the model is suited to describe the complete building energy demand, considering uncontrollable electrical appliances along with controllable HVAC systems. 7 mesmo.der_models.FlexibleEVChargerModel 8 [https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models](https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models) 9 [https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-ev-chargers](https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-ev-chargers)

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> DSF potential in HVAC system arises from 1) the thermal inertia of the building and 2) supplementary TESSs or BESSs. This allows the load of the HVAC system to be shifted, by pre-cooling or pre-heating a building while maintaining an admissible interval of indoor air comfort constraints. Hence, the thermal building model expresses the relationship between the indoor air comfort, the load of the HVAC system, the weather conditions and the building occupancy. The implementation of the flexible building model in MESMO is based on the Control-oriented Building Model (CoBMo) [45]. The mathematical model formulation of CoBMo is outlined in the following based on [164].
##### Fundamental model

The thermal comfort is expressed in terms of the indoor air temperature. Hence, the thermal building model expresses the relationship between the indoor air temperature, the electric load of the HVAC system, the local weather conditions and the building occupancy. The indoor air temperature, i.e. zone temperature, within each zone is assumed to be uniformly distributed. As a starting point, the differential equation of the zone temperature *Tz*of zone *z* is expressed as: !

|||1|X|||||
|---|---|---|---|---|---|---|---|
||z th,z||s∈S|cnv,int s,z|inf z|occ z|hvac z|
|cnv,int|b||||b||th|
|s,z||z||||||
|inf z|||hvac z|||occ z||

<u>dT</u> ˙ ˙ ˙ ˙ = *· Q* + *Q* + *Q* + *Q* (8.29) *dt C* *z*

Where *Czth*is the thermal heat capacity of zone *z ∈Z*, which is obtained according to ISO 13790. The symbol *Z* is the set of all zones *z* in building *b ∈B* and *B* *th* is the set of all buildings *b*. The heat transfer towards zone *z* is composed of the the convective heat transfer *Q* ˙ from surfaces *s ∈S* towards zone *z*, heat transfer towards zone *z* due to infiltration *Q* ˙, heat transfer towards zone *z* due to occupancy gains *Q*˙ and heat transfer towards zone *z* from the HVAC systems *Q*˙, where *Sz*is the set of all surfaces adjacent to zone *z*.

##### Exterior surfaces

Exterior surfaces are modeled as two thermal resistances with a centered heat capacitance between the exterior and zone *z*. Each surface *s* is adjacent to exactly one zone *z*.

The heat balance for the exterior side of surface *s* is expressed as:

||cnv,ext|irr,ext|ems,sky|ems,gnd|cnd,ext||
|---|---|---|---|---|---|---|
|cnv,ext|s|s|s|s|s|irr,ext|
|s ems,sky s|irr,ext s||ems,sky s cnd,ext s|ems,gnd s||s|

*Q* ˙ + *Q*˙ *− Q*˙ *− Q*˙ = *Q*˙ (8.30)

˙ ˙ Where *Q* is the convective heat transfer from the exterior towards surface *s*, *Q* ˙ ˙ is the incident irradiation onto surface *s*, *Q* and *Q* are the emitted radiation from surface *s* towards the sky and the ground. Note that radiative heat exchange with the ˙ sky *Q* excludes any radiative heat exchange with the sun disc, which is modeled ˙ ˙ separately as irradiation *Q*. The symbol *Q* describes the conductive heat transfer from the exterior towards the core of the surface.

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> The balance equation for the interior side of surface *s* is expressed as:

||cnd,int|cnv,int|irr,int|
|---|---|---|---|
|cnd,int s cnv,int s irr,int s|s|s|s|

*Q* ˙ = *Q*˙ *− Q*˙ (8.31)

˙ On the interior side, *Q* is the conductive heat transfer from the core towards the interior ˙ side of the surface, *Q* is the convective heat transfer from the interior side of surface ˙ *s* towards zone *z* and *Q* is the incident irradiation reaching surface *s* through exterior windows adjacent to the same zone *z*.

The heat balance for the core of surface *s* is expressed as:

<u>dTs</u> *thm* ˙ *cnd,ext*˙*cnd,int* *Cs*= *Qs− Qs*(8.32) *dt*

Where *Csthm*is the heat capacity of surface *s*. If the heat capacity of surface *s* is neglectable ˙ *cnd,ext*˙*cnd,int* *Csthm*= 0, e.g. for windows, the term simplifies to *Qs*= *Qs*. ˙ *cnv,ext* The exterior convective term *Qs*is expressed as:

*Q* ˙ *cnv,ext* *s*= *Ash* *cnv,ext* *T* *amb* *− Ts* *ext* (8.33)

Where *As*is the surface area of surface *s* and *h* *cnv,ext* is the exterior convective heat transfer *cnv,ext* 2 *−*1 coefficient which is given according to ISO 6946 as *h* = 0*.*04 m K*/*W. The symbol *T* *amb* is the ambient temperature and *Tsext*is the temperature at the exterior side of surface *s*. ˙ *irr,ext* The exterior irradiation term *Qs*is expressed as:

*Q* ˙ *irr,ext* *s*= *Asαsq*˙*d, d* = *d*(*s*) (8.34) *irr,ext*

Where *αs*is the absorption coefficient of surface *s* assuming a uniform absorption across *irr,ext* the spectrum of the incident irradiation. The symbol *q*˙ *d* is the total incident irradiation onto a surface oriented towards direction *d* = *{N,E,S,W,H}*, i.e. vertically facing North *N*, East *E*, South *S*, West *W* or horizontally facing upwards *H*, depending on the respective surface’s orientation *d* = *d*(*s*).

˙ *ems,sky* The exterior sky emission term *Qs*describes the radiative heat loss through emission towards the sky. The term is expressed as:

||ems,sky s|s sky s|sky||
|---|---|---|---|---|
|||sky|||
|||s|||
|sky||sur,ext,lin|sky,lin|sky s|
|sky||s|||
|s sky s|s|ssky|||

*Q* ˙ = *A h T* *s* *ext* *− T* (8.35)

In this linear approximation, the symbol *h* is introduced as the sky heat transfer coefficient of surface *s*, whereas *T* is the sky temperature. The sky heat transfer coefficient *h* in turn is defined as: !3 <u>T + T</u> *h* = 4*σε F* (8.36) 2

Where *σ*, *εs*and *F* are the Stefan-Boltzmann constant, the surface emission coefficient of surface *s* for long-wave radiations and the view factor of surface *s* towards the sky. The

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u>
*sur,ext,lin sky,lin sky* temperatures *Ts*and *T* are linearization constants of *Tsext*and *T*. The term *sky sky sky* *Fs*is defined as *Fs*= 0*.*5 for *d*(*s*) *∈{N,E,S,W}* and *Fs*= 1 *d*(*s*) = *H*, where *d*(*s*) is the direction orientation of the surface. ˙ *ems,gnd* The exterior ground emission term *Qs*describes the radiative heat loss through emis- sion towards the ground as well as the built environment. The term is expressed similar to *Q* ˙ *s*as: *ems,sky*

*Q* ˙ *ems,gnd* *s*= *Ash* *gnd* *sTs* *ext* *− T* *amb* (8.37)

*gnd amb* Where *hs*is introduced as the ground heat transfer coefficient of surface *s*, whereas *T* *gnd* is the ambient temperature. The ground heat transfer coefficient *hs*in turn is defined as: !3 *sur,ext,lin amb,lin* *gnd*<u>Ts+ T</u> *hs*= 4*σεsFsgnd*(8.38) 2

*gnd sur,ext,lin* Where *Fs*is the view factor of surface *s* towards the ground. The temperatures *Ts* *amb,lin amb gnd* and *T* are linearization constants of *Tsext*and *T*. The term *Fs*is defined as *gnd gnd* *Fs*= 0*.*5 for *d*(*s*) *∈{N,E,S,W}* and *Fs*= 0 *d*(*s*) = *H*, where *d*(*s*) is the direction orientation of the surface. ˙ *cnv,int* The interior convective term *Qs*is expressed as:

*Q* ˙ *cnv,int* *s*= *Ash* *cnv,int* *sTs* *int* *− Tz*(8.39)

*cnv,int* Where *hs*, *Tz*and *Tsint*are the interior convective heat transfer coefficient, the zone air temperature and the temperature at the interior side of surface *s*. The interior heat transfer co- *cnv,int cnv,int* 2 *−*1 efficient *hs*is defined according to ISO 6946 as *hs*= 0*.*13 m K*/*W for *d*(*s*) *∈* *cnv,int* 2 *−*1 *{N,E,S,W}* and *hs*= 0*.*17 m K*/*W for *d*(*s*) = *H*, where *d*(*s*) is the direction orientation of the surface. ˙ *irr,int* The interior irradiation term *Qs*is expressed as:

*Q* ˙ *irr,int* *s*= *Asαsq*˙*z* *irr,int* *, d* = *d*(*s*) (8.40)

*irr,int* Where *q*˙*z*is the interior irradiation incident to all surfaces of zone *z*. The interior radiation *irr,int* *q*˙ *z*is in fact the irritation which has entered zone *z* by passing through adjacent windows and is assumed to be uniformly distributed to all surfaces. This term is expressed as: P*irr,ext* <u>w∈Wz</u> <u>A</u>*w*<u>τ</u>*w*<u>q˙</u> <u>d(w)</u> *q*˙ *zirr,int*= P (8.41) *s∈Sz* *As*

Where *τw*is the transmission coefficient of window *w*. The sets *Wz*and *Sz*contain all windows *w* and surfaces *s* that are adjacent to zone *z*. ˙ *cnd,ext*˙*cnd,int* Finally, the conductive terms *Qs*and *Qs*are defined:

*Q* ˙ *cnd,ext* *s*= *As*2*h* *cnd* *sTs* *ext* *− Ts* *cnd,int cnd int* (8.42) *Q* ˙ *s*= *As*2*hsTs− Ts*

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> Where *h* *cnd* *s*is the conductive heat transfer coefficient of surface *s* and *Ts*is the surface core temperature. For surfaces with a neglectable heat capacity, e.g. windows, the relationship simplifies to:
*Q* ˙ *ext,int* *s*= *Ash* *cnd* *sTs* *ext* *− Ts* *int* (8.43)

Equations (8.30) to (8.42) and (8.43) define an overdetermined equation system, such that the temperatures *Tsext*and *Tsint*can be eliminated. However, the final equations which represent the complete model are omitted for brevity.

##### Interior and adiabatic surfaces

Interior surfaces are modeled as two thermal resistances with a centered heat capacitance between the zone *z₁* and zone *z₂*. In principle, interior surfaces are modeled equivalently to exterior surfaces, where the heat balance for the interior side (eq. (8.31)) is applied for both sides of the surface. Adiabatic surfaces are modeled as a single thermal resistances between a heat capacitance and zone *z*. Adiabatic surfaces are modeled equivalently to exterior surfaces which are only the heat balance for the interior side (eq. (8.31)) is applied. For the sake of brevity, the full equations are omitted here.

##### Infiltration

˙ *inf* The heat transfer towards zone *z* due to infiltration *Qz*is defined as:

*Q* ˙ *inf* *z*= *VzC* *th,air* *n* *inf* *zT* *amb* *− Tz*(8.44)

*th,air inf* Where *Vz*is the volume of zone *z*, *C* is the heat capacity of air and *nz*is the infiltration rate.

##### Occupancy gains

Assuming perfect knowledge of the building occupancy schedule, the heat transfer towards zone *z* due to occupancy gains *Q*˙ *occ* *z*, i.e. internal gains, is expressed as:

*Q* ˙ *occ* *z*= *Azq*˙*z* *occ* (8.45)

Where *Az*is the area of zone *z* and *q*˙*zocc*is the specific thermal gain due to occupancy.

##### HVAC systems

HVAC systems are distinguished into 1) generic HVAC system, 2) air handling unit (AHU), 3) terminal units (TUs), 4) heating and chiller plant. The generic HVAC system provides thermal heating / cooling power to each zone *z*, i.e. it directly adds / removes thermal energy to / from the zone. This generic HVAC system is an auxiliary system type which helps to model

1) simplified HVAC systems in case that a detailed model is not required or 2) HVAC system types for which a detailed model has yet to be implemented. The air handling unit (AHU)
125

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> serves supply air, i.e. conditioned outdoor air at a fixed temperature and humidity level, to each zone *z*. A terminal unit (TU) serves supply air, i.e. re-conditioned zone air at a fixed temperature, to each zone *z*. Note that the TU takes in zone air, whereas the AHU draws fresh outdoor air. The heating and cooling demand of the AHU and TUs is provided in form of supply water, i.e. hot and chilled water, by the heating and chiller plant. The presented HVAC system models can in principal be amended for further system types, e.g. hydronic radiators, once appropriate linear models are formulated. The total heat transfer towards zone *z* from the HVAC systems *Q*˙
*hvac* *z*and the total electric demand of the HVAC systems *P* *hvac,el* is expressed as:

*Q* ˙ *hvac* *z*= *Q* ˙ *gen* *z*+ *Q* ˙ *ahu* *z*+ *Q* ˙ *tu* *z* X *hvac,el*˙ (8.46) *P* = *Pzgen,el*+ *Pzahu,el*+ *Pztu,el* *z∈Z*

˙ *gen*˙*ahu*˙*tu*˙*gen,el ahu,el tu,el* Where *Qz*, *Qz*, *Qz*, *Pz*, *Pz*and *Pz*are the heat transfer towards zone *z* and electric power demand for the generic HVAC system, the AHU and the TU respectively. ˙ *gen* The heat transfer towards zone *z* from the generic HVAC system *Qz*is expressed as:

*Q* ˙ *gen* *z*= *Q* ˙ *gen,heat* *z*+ *Q* ˙ *gen,cool* *z*(8.47)

˙ *gen,heat*˙*gen,cool* Where *Qz*and *Qz*are the thermal heating and cooling power provided to zone *z*. ˙ *gen,heat*˙*gen,cool* Note that *Qz≥* 0 and *Qz≤* 0

The electric demand of the generic HVAC system is expressed as:

|||gen,heat|gen,cool|
|---|---|---|---|
||zgen,el|z|z|
|gen,heat|gen,cool gen,el|||
||z|||
||||cool|
|gen,el||||
|z||||

*P* ˙ = *ηgen,heatQ*˙ + *ηgen,coolQ*˙ (8.48)

Where *η* and *η* are the efficiency factor for heating and cooling of the generic HVAC system and *P* is the electric power consumption of the generic HVAC system associated with thermal demand supplied at zone *z*. Note that *η* takes a negative value such that *P* is positive. The part-load behavior of the heating and chiller plant is neglected.

The AHU model considers a cooling coil, a heating coil, supply air fan, exhaust air fan as well as a heat recovery system. For dehumidification, the air flow is assumed to be cooled below its dew point temperature and humidity is removed from the air by condensation at the cooling coil, then the air is reheated to supply air temperature. A humidifier is not considered in the model.

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> The heat transfer towards zone *z* from the AHU *Q*˙
*ahu* *z*is expressed as:

|ahu||th,air ahu|||
|---|---|---|---|---|
|z|zahu,heat zahu,cool|th,air|zheat,lin ahu|zcool,lin|
|ahu,heat|||air||
|z ahu,cool|zahu,heat ahu,heat|zahu,cool|ahu,heat,rec||
|z|zahu,heat air|zahu,cool ahu,cool|ahu,cool,rec||

*Q* ˙ =*V*˙ *C T − T*

##### + V˙ C T − T

*Q* ˙ = *V*˙ + *V*˙ *ρ* (8.49) *·* ∆*h −* ∆*h*

*Q* ˙ = *V*˙ + *V*˙

##### · ρ ∆h − ∆h

˙ *ahu*˙*ahu,heat*˙*ahu,cool* Where *Qz*is the heat transfer from the AHU towards zone *z*, *Vz*and *Vz*is the air flow rate for heating and cooling from the AHU towards zone *z* and *C* *th,air* is the heat capacity of air. The symbols *T* *ahu* is the temperature of the conditioned supply air from the *lin,heat lin,cool* AHU and *Tz*as well as *Tz*are the linearization constants of the air temperature ˙ *ahu,heat*˙*ahu,cool* at zone *z* for heating and cooling. Further, *Qz*and *Qz*are the AHU heating and cooling demand to supply air for *z* at set point conditions and ∆*h* *ahu,heat* and ∆*h* *ahu,cool* are the specific heating and cooling power applied to the outdoor air in order to obtain AHU supply air conditions. The symbols ∆*h* *ahu,heat,rec* and ∆*h* *ahu,cool,rec* are the specific heating and cooling power that is recovered from the return air. Note that the definition of ∆*h* *ahu,cool,rec* and ∆*h* *ahu,heat,rec* is omitted in the following for the sake of brevity. Heat gains due to the supply fan units are neglected in this model. The specific cooling and heating power are calculated such that the supply air is conditioned to the desired temperature set point *T* *ahu* and absolute humidity *x* *ahu*. Depending on the ambient air temperature *T* *amb* and ambient absolute humidity *x* *amb*, ∆*h* *ahu,cool* and ∆*h* *ahu,heat* are defined as:

*x* *am,l* *≤ x* *ahu* : *ahu,cool* 0*,h* *ahu am,l am,l am,l*

||∆h|= min|T ,x|− h|T|,x||
|---|---|---|---|---|---|---|---|
||ahu,heat am,l ahu,cool ahu,heat|ahu|ahu ahu|am,l am,l ahu|am,l am,l|am,l||
|am,l|am,l|||||||
|||ahu|ahu ahu|ahu||||

∆*h* = max 0*,h T,x − h T,x* (8.50) *x > x* :

∆*h* = *h x* *ahu* *,φ* = 1 *− h T,x*

∆*h* = *h T* *ahu* *,x − h x,φ* = 1

Where *T* and *x* are the linearization constants of the ambient air temperature and the ambient absolute humidity. The symbol *x* is the absolute humidity at supply air set-point conditions and is defined as *x* = *x T,φ*, where *x* (*T,φ*) is the absolute humidity for a value pair of the dry-bulb temperature *T* and relative humidity *φ*. The functions *h*() and *x*() give the specific enthalpy of wet air.

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u>
*ahu,el* Finally, the the electric load due to the air supply to zone *z* through the AHU *Pz*is expressed as: <u>1</u>*ahu,heat*<u>1</u> ˙*ahu,cool* ˙

||P|Q||Q|||
|---|---|---|---|---|---|---|
||zahu,el|heat z|cool ahu,fan|z el,ahu,fan|||
|||zahu|||||
|heat ahu,fan|cool el,ahu,fan||||z ahu,cool,el||

*zahu,el*=*heat z cool z* *η η* (8.51) + *V*˙ ∆*p η* *cool* Where *η* and *η* are the heating and cooling efficiency, i.e. the COP, of the heating and chiller plant. Note that *η* takes a negative value such that *P* is positive. The symbols ∆*p* and *η* are the total pressure rise across all fans and the average electric efficiency coefficient of the fans. *tu* The heat transfer towards zone *z* from the TU *z Q*˙*z*is expressed as:

˙*tu*˙*tu,heat*˙*tu,cool* *Qz*= *Qz*+ *Qz* ˙*tu,heat*˙*tu,heat th,air tu,heat heat,lin* *Qz*= *VzC T − Tz* (8.52)

˙*tu,cool*˙*tu,cool th,air tu,cool cool,lin* *Qz*= *VzC T − Tz*

˙*tu,heat*˙*tu,cool* Where *Qz*and *Qz*are the heat transfer for heating and cooling from the TU towards zone *z*, *V*˙*ztu,heat*and *V*˙*ztu,cool*are the air flow rate for heating and cooling from the TU towards *th,air tu,heat tu,cool* zone *z* and *C* is the heat capacity of air. The symbols *T* and *T* are the *heat,lin* temperature of the conditioned supply for heating and cooling air from the TU and *Tz* *cool,lin* as well as *Tz*are the the linearization constants of the air temperature at zone *z* for heating and cooling. *tu,el* Finally, the the electric load due to the air supply to zone *z* through the TU *Pz*is expressed as:

||heat|tu,heat|cool tu,cool|tu,f|el,tu,f|||
|---|---|---|---|---|---|---|---|
||ztu,el|z|z|ztu||||
|heat tu,f|cool cool el,tu,f||||z tu,cool,el|||

*P* = *η Q*˙ + *η Q*˙ + *V*˙ ∆*p η* (8.53)

Where *η* and *η* are the heating and cooling efficiency, i.e. the COP, of the heating and chiller plant. Note that *η* takes a negative value such that *P* is positive. The symbols ∆*p* and *η* are the pressure rise across the fan and the average electric efficiency coefficient of the fan.

##### State-space model

The flexible building model is transformed into a state-space model according to eq. (8.3) by arranging the model variables into vectors and the model parameters into appropriate matrices. The state-space model is simply a vectorized representation of the differential equations for the zone temperature in eq. (8.29) and the surfaces in eq. (8.32), where the

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> model variables are arranged into the following vectors:

|⊺|⊺ ⊺||||
|---|---|---|---|---|
|z z∈Z|s s∈S||||
|gen,heat|⊺|gen,cool ⊺||⊺|
|z|z∈Z ⊺|z z∈Z ⊺|zahu,heat|z∈Z ⊺ ⊺|
|zahu,cool|z∈Z ztu,heat|z∈Z|ztu,cool|z∈Z|
|amb sky|⊺ dirr d∈{N,E,S,W,H}||⊺ zocc z∈Z|⊺|
|⊺|⊺|hvac,el|⊺||
|z z∈Z|zahu z∈Z||||

*x* = [*T*]*,* [*T*] h i h i h i *u* = *Q*˙*, Q*˙*, V*˙*,*

h i h i h i *V*˙*, V*˙*, V*˙ (8.54) h i *v* = *T,T, q*˙*,*[ ˙*q*] h h i i *y* = [*T*]*, V*˙*,P*

Note that the vectors *x*, *u*, *v*, *y* are the continuous-time state, control, disturbance and output vectors. The time-discrete form of the thermal building model is obtained by application of zero-order hold discretization according to eq. (8.5). The final discrete-time state-space model is expressed as:

|t+1|t|u t|v t|||
|---|---|---|---|---|---|
|t|t|u t|v t u|u v|v|

*x* = *Ax* + *B u* + *B v* (8.55) *y* = *Cx* + *D u* + *D v*

Where the matrices *A*, *C* are the state and output matrix, and *B*, *D*, *B*, *D* are the input and feed-through matrices, on the control and disturbance vectors respectively.

##### MESMO implementation

The flexible building model is implemented in MESMO as FlexibleBuildingModel¹⁰. The implementation relies on the CoBMo toolbox [45], which implements the detailed model equations formulated above. The CoBMo toolbox is included as a Git submodule in MESMO.

##### 8.3.5 Storage systems

The storage model describes TESSs or BESSs with controllable charging and discharging power. The model formulation assumes that the charging and discharging dispatch is constrained by 1) the storage capacity and 2) maximum and minimum charging / discharging limits. Storage systems can be connected to either the electric grid or the thermal grid but not to both grid types simultaneously.

##### Fundamental model

As a starting point, consider the differential equation of the charged energy *ed*of the storage system *d* as:

*ch*<u>1</u>*dch dch* *e*˙*d*= *ηdchpd− pd− ed,tnd*(8.56a) *dch* *η* *d* 10 mesmo.der_models.FlexibleBuildingModel

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u>

|ch|dch||
|---|---|---|
|d|d||
|dch dch|ddch|dch|
|d||d|
 The scalars *p* and *p* are the charging power and discharging power of storage system *d*. The scalars *η* and *η* are the charge and discharge efficiencies of storage system *d*. The symbol *n* denotes the self-discharge rate of the storage system, where *n* = 1*/*h. Assuming a constant time step length ∆*t*, the time-discrete version of eq. (8.56) is obtained as:
<u>1</u>*N* *ed,t*+1+ ∆*t ∀t ∈T /t* (8.57a)

|= e 1 − n|∆t|η p −|p|
|---|---|---|---|
|d,t|dch d|dch ch d,t|dch dch d,t|
||||d|
|t t+1||||

*η*

The indices ()*,*() denote the current and the next time step respectively. The scalar ∆*t* denotes the time step interval.

##### The operational constraints are expressed as:

*pu nm pu nm*

||−e||p |∆t ≤ e|≤ e||p |∆t|
|---|---|---|---|---|
||||ch d,t dch d,t|+,pu nm d d +,pu nm d d|
||pu||||
|pu|d|nm|||
|d|+,pu|d|||
||d||||

*d d d,t d d* *∀t ∈T* (8.58a) *ch* +*,pu nm* 0 *≤ p ≤ p p ∀t ∈T* (8.58b)

0 *≤ p ≤ p p ∀t ∈T* (8.58c)

The scalar *e* denotes the per-unit energy storage capacity of the storage system, where *e* = h. The scalar *p* denotes the nominal power demand of the storage system *d*. The symbol *p* denotes the per-unit maximum charging / discharging power. While the model formulation does not explicitly prohibit simultaneous charging and discharging, this is implicitly enforced through the energy cost minimization objective of the optimal operation problem, i.e. simultaneous charging and discharging would cause additional cost for charging / discharging losses.

|The total power demand / injection p||||of the storage system is obtained as:||
|---|---|---|---|---|---|
|||d,t|dch d|ch d,t||
||d,t|||||
||||||pu|
|nm +,pu|ch|dch|||d|
|d d|d|d||||
||||||d,t|

*d,t*

*p* = *p − p ∀t ∈T* (8.59a)

Note that *p* will take negative values for load, i.e. when the storage system is charging, and negative values for injection, i.e. when the storage system is discharging. The scalars *e*, *p*, *p*, *p* and *p* are positive values for storage systems by definition.

The storage model applies for both TESSs and BESSs. Therefore, the power value *p* can characterize both active and thermal power, depending on whether the storage is connected to the electric grid or the thermal grid. If the storage system is connected to the electric grid, he reactive power value is defined through the mapping matrix (see eq. (8.12)), thus assuming a fixed power factor.

##### State-space model

The storage model is transformed into a state-space model according to eq. (8.3) by arranging the model variables into vectors and the model parameters into appropriate matrices. To this end, the state-space formulation is simply a representation of the differential equation for the

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> consumed energy in eq. (8.57), where the model variables are arranged into the state-space vectors:
  *ched,t* *p* *d,t ch* *xd,t*= *ed,tcd,t*=*dchdd,t*= [] *yd,t*= *pd,t* *∀t ∈T* (8.60a) *p* *d,t dch* *p* *d,t*

The entries of the state-space matrices are derived accordingly from eqs. (8.57) and (8.58) as: " # *η* ∆*t*

|1 − n A =|∆t|B =||B = []||
|---|---|---|---|---|---|
|d|dch d|dc|dch 1|dd||
||||η|||
|d,t||d c|pu nm|d d|pu nm|
|0||+|+,pu d d nm|−|d d|
|d|d,t|d,t|d +,pu d nm|d,t||
||||d d|||
||||||N|
|d|d,t|||||

*−* ∆*t* (8.61a) *d* *dch*     1 0 0 *C* = 0 *D* = 1 0 *D* = [] (8.61b) 0 0 1     *−e |p | e |p |*   *x* = *e N y* =  *p p y* =  0 *∀t ∈T* (8.61c) 0 *p p*

Note that *x⁰* = *e N* links the initial state to the final at time step *t*.

Lastly, the mapping matrices are defined according to eq. (8.59) as: h*nm nm*i *th* *p,y el el q,y el* <u>qd</u> *el* <u>qd</u>*p,y th th* *M* *d* = 0 *−a* *d* *a* *d* *M* *d* = 0 *−a* *d pnm* *a* *d pnm* *M* *d* = 0 *−a* *d* *a* *d* *d d* (8.62a)

The symbols *a* *el* *d* *,a* *th* *d* *∈{*0*,*1*}* denote whether storage system *d* is connected to the electric

|el|d d|th|nm|
|---|---|---|---|
|d||d|d|

grid *a* *el* = 1 or the thermal grid *a* *th* = 1. The scalars *p* *nm* and *q* *dnm* denote the nominal active power and nominal reactive power of storage system *d*.

##### MESMO implementation

The state-space form of the storage model has been implemented in MESMO as Storag eModel¹¹. The corresponding model data definition is documented in the MESMO data reference¹².

##### 8.3.6 Cooling plants

The cooling plant model describes a flexible generator that injects thermal power in the form of chilled water to the thermal grid. Typically, the cooling plant acts as central source for thermal power in the DCS. The cooling plant essentially converts electric power into thermal power via a chiller cycle, i.e. an inverted heat pump cycle. To this end, cooling plants must connected to both the electric grid and the thermal grid. 11 mesmo.der_models.StorageModel 12 [https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models](https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models)

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u>
##### Fundamental model

The core components of the cooling plant are the chiller set and the cooling tower set, which are connected through the condenser water circuit [39, p. 35, Section 3.1]. Note chillers and cooling towers are referred to as sets here, since each cooling plant comprises multiple chillers and cooling towers. Each of the three components of the cooling plant consumes electric power in proportion to the thermal power production. Therefore, the efficiency for thermal power production from electric power, i.e. the inverse of the coefficient of performance (COP), can be derived based on cooling plant subsystem models. This has been extensively presented in [39, Sections 3.2.1 to 3.2.4], which forms the basis for the MESMO implementation. However, model is simplified here for the sake of brevity.

Therefore, the fundamental model for the cooling plant is expressed as:

*th cp* *pd*= *−η* *d* *pd*(8.63a)

The scalars *p* *th* *d* and *pd*denote the thermal power injection and the active power demand of *cp* the cooling plant *d*. The scalar *η* *d* is the total efficiency of cooling plant *d*, which is derived according to [39, Sections 3.2.1 to 3.2.4]. Note that the thermal power production is positive and the active power demand is negative by convention in MESMO.

The operational constraints of the cooling plant are expressed as:

|||th|+,pu th,nm|
|---|---|---|---|
|||d|d d|
|th,nm|+,pu|||
|d|d|||

0 *≤ p ≤ p p* (8.64a)

The scalars *p* and *p* are nominal thermal power production and the per-unit maximum power production of cooling plant *d*.

Note that the reactive power value of the cooling plant is defined through the mapping matrix (see eq. (8.12)), thus assuming a fixed power factor.

##### State-space model

The cooling plant model is transformed into a state-space model according to eq. (8.3) by arranging the model variables into vectors and the model parameters into appropriate matrices as:

*p* *th* *d,t* *xd,t*= [] *cd,t*= *pd,tdd,t*= [] *yd,t*= *∀t ∈T* (8.65a) *pd,t*

The entries of the state-space matrices are derived accordingly from eqs. (8.63) and (8.64) as:

(8.66a)

|A = []|B = []|||B = []|||
|---|---|---|---|---|---|---|
|d|dc|||dd|||
|d,t|d c|||d d|+,pu|th,nm|
|0 d|d,t +|+,pu d|nm d|d,t −|d|d|

0 *C* = [] *D* = *D* = [] (8.66b) 1

0 *p p* *x* = [] *y* = *y* = *∀t ∈T* (8.66c) *−p p* 0

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u> Lastly, the mapping matrices are defined as:
h*nm*i *th*

|p,y|q,y|q|p ,y|
|---|---|---|---|
|d|d|p|d|

<u>d</u> *M* = 0 1 *M* = 0*nm M* = 1 0 (8.67a) *d*

Note that this mapping requires that the cooling plant is connected to both the electric grid and the thermal grid.

##### MESMO implementation

The state-space form of the storage model has been implemented in MESMO as CoolingP lantModel¹³. The corresponding model data definition is documented in the MESMO data reference¹⁴.

##### 8.3.7 Heating plants

The heating plant model describes a flexible generator that injects thermal power in the form of hot water to the thermal grid. Currently, MESMO defines the heating plant as a heat-pump-based system. Therefore, the heating plant model is equivalent to the cooling plant model, except that thermal power is produced as hot water rather than chilled water. A future version of MESMO may revise this model to include a more comprehensive range of heating plant systems.

##### Fundamental model

The fundamental model for the heating plant is expressed as:

*th hp* *pd*= *−η pd*(8.68a) *d*

*th* The scalars *p* and *p* denote the thermal power injection and the active power demand of *d d* *hp* the heating plant *d*. The scalar *η* is the total efficiency of heating plant *d*, i.e. the inverse of *d* the COP of its heat pump. Note that the thermal power production is positive and the active power demand is negative by convention in MESMO.

The operational constraints of the heating plant are expressed as:

|||th|+,pu th,nm|
|---|---|---|---|
|||d|d d|
|th,nm|+,pu|||
|d|d|||

0 *≤ p ≤ p p* (8.69a)

The scalars *p* and *p* are nominal thermal power production and the per-unit maximum power production of heating plant *d*.

Note that the reactive power value of the heating plant is defined through the mapping matrix (see eq. (8.12)), thus assuming a fixed power factor. 13 mesmo.der_models.CoolingPlantModel 14 [https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models](https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models)

<u>8. Distributed energy resource modeling 8.3. Flexible DERs</u>
##### State-space model

The heating plant model is transformed into a state-space model according to eq. (8.3) by arranging the model variables into vectors and the model parameters into appropriate matrices as: *th* *p* *d,t* *xd,t*= [] *cd,t*= *pd,tdd,t*= [] *yd,t*= *∀t ∈T* (8.70a) *pd,t*

The entries of the state-space matrices are derived accordingly from eqs. (8.68) and (8.69) as:

(8.71a)

|A = []|B = []|||B = []|||
|---|---|---|---|---|---|---|
|d|dc|||dd|||
|d,t|d c|||d d|+,pu|th,nm|
|0 d|d,t +|+,pu d|nm d|d,t −|d|d|

0 *C* = [] *D* = *D* = [] (8.71b) 1

0 *p p* *x* = [] *y* = *y* = *∀t ∈T* (8.71c) *−p p* 0

Lastly, the mapping matrices are defined as: h*nm*i *th*

|p,y|q,y|q|p ,y|
|---|---|---|---|
|d|d|p|d|

<u>d</u> *M* = 0 1 *M* = 0*nm M* = 1 0 (8.72a) *d*

Note that this mapping requires that the heating plant is connected to both the electric grid and the thermal grid.

##### MESMO implementation

The state-space form of the storage model has been implemented in MESMO as HeatingP lantModel¹⁵. The corresponding model data definition is documented in the MESMO data reference¹⁶.

15 mesmo.der_models.CoolingPlantModel 16 [https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models](https://purl.org/mesmo/docs/0.5.0/data_reference.html#der-models)

## 9 Multi-energy system operation problem formulations

#### Contents

9.1 Fundamental problem types.......................... 135
9.2 Nominal operation problem........................... 136
9.2.1 Outline................................. 136

9.2.1 Outline.	136
9.2.2 Solution algorithm.. 137
Optimal operation problem.	138
9.3.1 Outline.	138
9.3.2 Optimization problem...	139
9.3.3 Distribution locational marginal prices..	140
9.3.4 Solution algorithm.. 147

9.3
**Outline and contributions**

This chapter presents the formal problem definitions for the nominal and optimal operation problems.Section9.1distinguishes the features of both problem types.Thereafter, the problems and their solution algorithms are defined in sections9.2and9.3.

Although the fundamental MES operation problems are well established, their representations have been significantly redeveloped here to coherently present their implementation in MESMO. A core contribution of the thesis in this chapter is the derivation of DLMPs for thermal grids. Combined with the derivation of DLMPs for electric grids based on [11], [34], this is utilized to form the complete set of DLMPs for the MES. This work was previously published by the author in [14], [41].

**9.1 Fundamental problem types** As outlined in section3.2, MES analysis can be divided into operation problems and planning problems. MESMO is currently catered towards operation problems rather than planning problems, such that both nominal operation problems and optimal operation problem formu- lations have been implemented. Nevertheless, planning problems are indirectly supported
135

<u>9. Multi-energy system operation problem formulations 9.2. Nominal operation problem</u> in terms of simulation-based scenario analysis, i.e. by defining a set of of nominal / optimal operation problems. An example of such a study is provided in chapter10. A future version of MESMO can be extended to support planning problems in a more comprehensive manner. The following introduces the mathematical formulations and solution algorithms for two operation problem types:
- The **nominal operation problem** describes a traditional simulation problem for the MES. In this case, a-priori projections for the DER power injection / load schedules are assumed and the electric grid and thermal grid states are simulated via non-linear power flow solution algorithms. This is outlined in section9.2.
- The **optimal operation problem** describes a numerical optimization problem for the optimal dispatch of DERs with regards to the operational constraints of the electric grid, thermal grid and DERs. The objective function defaults to the maximization of social welfare based on predefined wholesale energy prices and DER production costs and utility functions. In this case, linear approximate models are utilized for electric grid and thermal grid, whereas state-space models are taken for flexible DERs. The problem formulation is defined in section9.3.
Note that MESMO also supports the construction of custom problem formulations for MESs in a plug-and-play fashion, based on the modularized electric grid models, thermal grid models and DER models outlined in chapters6to8.

#### 9.2 Nominal operation problem

##### 9.2.1 Outline

The nominal operation problem defines a simulation of the MES, assuming a fixed dispatch schedule for all DERs. Therefore, this problem amounts to obtaining the non-linear power flow solution of both the electric grid and the thermal grid according to sections6.2and7.2. The goal is to obtain the state variables of the MES as a function of its control variables, i.e. the DER dispatch schedules. The state variables of the MES consist of the state variables of the electric grid and the thermal grid as:

|•Nodal voltage vector u|of the electric grid||
|---|---|---|
|•Branch power flow vector in “from” and “to” direction s|||
|•Active and reactive power losses p|||
|•Nodal pressure head vector h||of the thermal grid|
|•Branch volume flow vector q||of the thermal grid|
|•Pump power demand p|of the thermal grid||

*t* *f tt* *t, s* of the electric grid *ls* *t,qtls*of the electric grid *t* *th,b* *t* *pm* *t*

<u>9. Multi-energy system operation problem formulations 9.2. Nominal operation problem</u> Note that ()*t*denotes the value of state variable at time step *t*. Although the electric and thermal power flow have been modeled for a single steady-state instant in sections6.2 and7.2, the same relation applies independently for all time steps. To this end, temporal coupling in MES operation problems only arise from the DER models. Accordingly, the input variables consist of the input variables of the electric grid and the thermal grid as:
- DER apparent power injection vector *s*, which is decomposable into active power *p* and reactive power *q* as *s* = *p* + *jq* •DER thermal power injection vector *p*
*th*

Note that active power *p* and reactive power *q* compose the apparent power injection vector *s* as *s* = *p* + *jq*. Also, recall that by convention MESMO expresses load as negative power values and injection as positive power values.

##### 9.2.2 Solution algorithm

**Algorithm 3:** Solution algorithm for the nominal operation problem **begin** electric and thermal grid model initialization: Obtain electric grid model parameters: *A* *f/t* *, Y, Y* *f/t* *, H, A* *d*; Obtain thermal grid model parameters: *A* *th,b* *, r* *th* *, d* *th* *,η* *pm* *,* ∆*h* *ets* *, A* *th,d*;

**begin** DER model initialization: **for** *t ∈T* **do** h i Obtain active power: *pt*= *p* *nm* *d,t* *∀t ∈T*; h*d*i*∈D* *el* Obtain reactive power: *qt*= *q* *d,t* *nm* *∀t ∈T*; h*d∈D*i *el* *th th,nm* Obtain thermal power: *pt*= *p* *d,t* *∀t ∈T*; *d∈Dth*

**begin** power flow solution: **for** *t ∈T* **do** *f/t ls* Solve electric power flow via algorithm1to obtain *ut, st,st*; *th,b pm* Solve thermal power flow via algorithm2to obtain *ht, qt,pt*;

The nominal operation problem is defined in terms of the solution algorithm in algorithm3. The solution process begins by obtaining the parameters for electric and thermal grid models. Then, the DER active, reactive and thermal power vectors are obtained for each time step based on the nominal power schedule for the respective DER. Note that flexible DERs are treated as uncontrollable, i.e. in the same fashion as fixed DERs. Thus nominal operation schedules are expected to be defined for all DERs for the nominal operation problem. Based on the initialized models, The solution for the MES state variables is obtained by

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u> successively solving the electric power flow problem and the thermal power flow problem. Since temporal coupling exists only in terms of the DER schedules, each time step can be solved independently. This is leveraged in the MESMO implementation by executing the power flow solutions in parallel.
#### 9.3 Optimal operation problem

##### 9.3.1 Outline

The optimal operation problem can be interpreted as the combined social welfare maximiza- tion problem of all stakeholders of the MES. The problem is formulated as a centralized optimization in the following, which assumes that the district energy system operator exer- cises direct control of all DERs connected to the MES. In particular, the problem formulation suggests that the energy system operator is aware of the DERs’ operational constraints and can directly control their dispatch schedule such that energy system constraints are respected. This level of oversight is typically only realistic at the planning stage. However, the centralized formulation serves as the foundation for market-based mechanisms, which ultimately amount to reformulations of the original problem in terms of distributed or decentralized optimization. An example for translating the centralized MES operation into market-clearing problem based on the alternating direction method of multipliers (ADMM) as solution mechanism has been demonstrated in [41].

The optimal operation problem defines a numerical optimization problem with the DER dispatch schedules as decision variables and the operational limits of electric grid, thermal grid and DERs as constraints. Note that the electric grid, thermal grid and DER model equations are also included as constraints in this optimization problem. To keep the problem formulation in the convex domain, the linear electric grid model and linear thermal grid model formulation are utilized in the following, rather than the non-linear power flow equations as in the nominal operation problem.

As the solution of the optimal operation problem, solution are obtained for the state variables as well as the control variables of the MES. In this case, the state variables of the MES consist of the state variables of the DERs, the electric grid and the thermal grid as:

|•State vector x|of flexible DER d|||
|---|---|---|---|
|•Output vector y|of flexible DER d|||
|•Nodal voltage vector u •Branch power flow vector in “from” and “to” direction s •Active and reactive power losses p||of the electric grid||
|•Nodal pressure head vector h|||of the thermal grid|
|•Branch volume flow vector q|||of the thermal grid|
|•Pump power demand p||of the thermal grid||

*d,t*

*d,t*

*t* *f tt* *t, s* of the electric grid *ls* *t,qtls*of the electric grid

*t* *th,b* *t* *pm* *t*

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u> Note that ()*t*denotes the value of state variable at time step *t*. Although the electric and thermal power flow have been modeled for a single steady-state instant in sections6.3 and7.3, the same relation applies independently for all time steps. To this end, temporal coupling in MES operation problems only arise from the DER models. Accordingly, the control variables consist of the input variables of the DERs, the electric grid and the thermal grid as:
##### •DER control vector cd,t

- DER apparent power injection vector *s*, which is decomposable into active power *p* and reactive power *q* as *s* = *p* + *jq* •DER thermal power injection vector *p*
*th*

Note that active power *p* and reactive power *q* compose the apparent power injection vector *s* as *s* = *p* + *jq*. Also, recall that by convention MESMO expresses load as negative power values and injection as positive power values.

##### 9.3.2 Optimization problem

As outlined above, the optimal operation problem is formulated as the optimization problem for the maximization of the overall social welfare as. Subject to the operational constraints of the electric grid, thermal grid and DERs, the problem is expressed as:

||X|X|||||
|---|---|---|---|---|---|---|
||rf,el|sr|rf,th th,sr||||
|x ,c ,y|, t|t|t t||||
|p ,p ,q, p ,p ,q|t∈T −|t∈T rf||u|,p t|rf|t rf|u t u t|

min *c p* + *c p* (9.1a) *d,t d,t d,t* *th* *t t t* *th,sr* *t* *sr* *t tsr* *|u|,q* ++ *−* *|u |≤|u |* + *M* (*p − p*) + *M* (*q − q*) *≤|u |* : *µ, µ*

s.t.
*∀t ∈T* (9.1b) *f f f,*+

|f,rf||s |,p|t rf||s |,q t|rf f,+||st|
|---|---|---|---|---|---|---|
|t,rf||s |,p|rf||s |,q t|rf t,+|ts||
|sr t|⊺ t ls,rf|p ,p|t rf|p ,q t|rf|p t|
|tsr|⊺ t ls,rf|q ,p|t rf|q ,q t|rf|q t|
|−|rf h,p|th th,rf t|h t||||
|th,b,rf|q ,p|th th,rf t|th,b,+|q t|||

*|s |* + *M* (*p − p*) + *M* (*q − q*) *≤|s |* : *µ ∀t ∈T* (9.1c) *t t t,*+ *|s |* + *M* (*pt− p*) + *M* (*q − q*) *≤|s |* : *µ ∀t ∈T* (9.1d) *ls ls ls* *p −* 1 *p* = *p* + *M* (*p − p*) + *M* (*q − q*) : *λ ∀t ∈T* (9.1e) *ls ls ls* *q −* 1 *q* = *q* + *M* (*p − p*) + *M* (*q − q*) : *λ ∀t ∈T* (9.1f) *th −* *h ≤ h* + *M* (*p − p*) : *µ ∀t ∈T* (9.1g) *th,b th th,b,*+ *q* + *M* (*p − p*) *≤ q* : *µ ∀t ∈T* (9.1h)

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u>
*pm th pm*

|th,sr|⊺ th|th,pm|pm,rf|p ,p|th th,rf|p|
|---|---|---|---|---|---|---|
|t|t||||t|t|
||0 x||||||
|d,t|d d||||||
|d,t+1|d d,t|dc d,t c|dd d,t d|x d,t y||N|
|d,t|d d,t|d d,t|d d,t|d,t|||
|−|+|y|y||||
|d,t|d,t d,t p,y|d,t p|d,t|q,y|p||
|d,t th d,t|d d,t p ,y d d,t|d,t p d,t|d,t|d d,t|d,t||

*p − p* = *η p* + *M* (*p − p*) : *λ ∀t ∈T* (9.1i) 0 *x* 0 = *x* : *λ ∀d ∈D* (9.1j)

*x* = *A x* + *B c* + *B d* : *λ ∀d ∈D, ∀t ∈T /t* (9.1k)

*y* = *C x* + *D c* + *D d* : *λ ∀d ∈D, ∀t ∈T* (9.1l) + *−* *y ≤ y ≤ y* : *µ, µ ∀d ∈D, ∀t ∈T* (9.1m)

*p* = *M y* : *λ, q* = *M y* : *λ ∀d ∈D, ∀t ∈T* (9.1n) *th th* *p* = *M y* : *λ ∀d ∈D, ∀t ∈T* (9.1o)

Note that this formulation directly inserts the linear electric grid model and linear thermal grid model into the respective operational constraints, thereby replacing the dependent model variables and yielding a more compact problem formulation. The scalars *c* *rf,el* and *c* *rf,th* denote the marginal cost of electric power at the source node of the electric grid and the marginal cost of thermal power at the source node of the thermal grid. Note that the marginal cost of power is used rather than the energy price for more compact *src th,src* notation, i.e. avoiding conversion from power to energy. The scalars *pt*, *qtsrc*, *pt* describe the total active, reactive power demand at the source node of the electric grid and the thermal power demand at the source node of the thermal grid. The scalar *η* *th,pm* serves as a conversion factor to express the pump power demand in terms of thermal power for the thermal power balance, where is determined by the COP of the DHP or DCP. + *− f,*+*stt,*+ *− th,b,*+ + *− ls ls pm*

|u u|st|h q|y y|p q|p|
|---|---|---|---|---|---|
|t t||t t|d,t d,t|t t|t|

The vectors *µ, µ, µ, µ, µ, µ, µ, µ* and scalars *λ,λ,λ* are the dual variables, i.e. Lagrange multipliers, associated with the respective inequality and equality constraints.

The above formulation of the MES operation problem assumes that the DHP or DCP of the thermal grid is co-located with the electric grid source node, such that the thermal grid source node is not subjected to any electric grid constraints. Therefore, the operation of the thermal grid and the electric grid are coupled only through the DER operation. Note that this formulation is regarded the primal form of optimization problem.

##### 9.3.3 Distribution locational marginal prices

DLMPs are nodal energy prices that express the marginal cost of supplying load or the marginal utility of procuring generation at a particular grid node. For the MES operation problem, DLMPs are formulated based on the electric and thermal grid operation constraints of the the optimal operation problem. Based on the dual variables associated with these constraints, DLMPs can be formulated to essentially reflect the operational conditions into nodal price signals to incentivize the flexibility of DERs, e.g. by rescheduling loads. For example, DLMPs will increase at nodes which are served through a congested branch, therefore serving as an incentive to reduce load or increase generation at these nodes to alleviate the congestion.

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u> Since DLMPs are essentially a linear expression of the dual variables of the optimization problem, the fundamental understanding of duality theory in convex optimization is a pre- requisite for the the following definitions. A review of these fundamentals is omitted here for the sake of brevity and is instead referred to [165, p. 215, Chapter 5] for a comprehensive introduction and to [55, p. 33, Section 3.1] for a brief review in the context of DLMPs. The formulation of DLMPs for the optimal MES operation are derived in several steps in the following:
1. As a starting the, Lagrangian function is formulated for the primal problem in eq. (9.2). The Lagrangian function consists of the primal objective plus a weighted sum of the primal constraints, where the weighting factors are in fact the dual variables of the optimization problem. Therefore. the Lagrangian function serves as the fundamental link between primal and dual problems in the following.
2. Based on the Lagrangian function and the primal problem formulation, the Karush-Kuhn- Tucker (KKT) conditions are derived in eqs. (9.3) and (9.5). The KKT conditions express conditions for global optimality of a solution to the convex optimization problem [165, p. 243, Section 5.5.3]. In the case of strong duality, which is always assumed for convex optimization, the KKT conditions serve as optimality conditions for both the primal and the dual problem.
3. The dual problem is then derived from the KKT conditions and the Lagrangian function in eq. (9.6). The dual problem is a complementary formulation of the optimization problem, where constraints and objective are expressions of the dual variables. Note that the dual problem does not strictly need to be formulated for deriving the DLMPs but it is provided here for context.
4. Lastly, the DLMPs of the MES operation problem are derived in eqs. (9.7) and (9.8) based on the Lagrangian function and the KKT conditions.
##### Lagrangian function

The Lagrangian function represents the primal problem in terms of a reformulated objective function, where the original objective is augmented by a weighted sum of the primal con- straints. The weighted sum consists of the primal constraint expressions multiplied with the associated dual variables, i.e. the Lagrange multipliers, respectively. The dual variables are denoted with the “:”-symbol in eq. (9.1). The basic idea is that the optimization problem can be represented as the minimization of the Lagrangian function by finding appropriate values for the dual variables. This is directly linked to the interpretation of DLMPs as prices, which are essentially penalty factors which replace the grid constraints in the optimal operation problem of individual DERs.

For eq. (9.1), the Lagrangian function is obtained as:

|X|X||
|---|---|---|
|rf,el|sr|rf,th th,sr|
|t|t|t t|
|t∈T|t∈T||

*L* = *c p* + *c p*

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u> X
*−*⊺ + *µ* *u* *t|u* *−* *|−|u* *rf* *|− M* *|u|,p* (*pt− p* *rf* ) *− M* *|u|,q* (*qt− q* *rf* ) *t∈T* X +⊺ + *µ* *u* *t|u* *rf* *|* + *M* *|u|,p* (*pt− p* *rf* ) + *M* *|u|,q* (*qt− q* *rf* ) *−|u* + *|* *t∈T* X *f,*+⊺*f f* + *µ* *st* *|s* *f,rf* *|* + *M* *|s |,p* (*pt− p* *rf* ) + *M* *|s |,q* (*qt− q* *rf* ) *−|s* *f,*+ *|* *t∈T* X *t,*+⊺*t t* + *µ* *st* *|s* *t,rf* *|* + *M* *|s |,p* (*pt− p* *rf* ) + *M* *|s |,q* (*qt− q* *rf* ) *−|s* *t,*+ *|* *t∈T* X*ls* *ls ls* *p sr* ⊺ *ls,rf p,p rf p,q rf* + *λtpt−* 1 *pt− p − M* (*pt− p*) *− M* (*qt− q*) *t∈T* X*ls* *ls ls* *q* ⊺ *ls,rf q,p rf q,q rf* + *λtqtsr−* 1 *qt− q − M* (*pt− p*) *− M* (*qt− q*) *t∈T* X *−*⊺*th* + *µ* *h* *th* *−* *− h* *rf* *− M* *h,p* (*p* *th* *t− p* *th,rf* ) *t∈T* X*th,b,*+⊺ *th,b th* *q th,b,rf q,p th th,rf th,b,*+ + *µtq* + *M* (*pt− p*) *− q* *t∈T* X*pm* <u>1</u> *pm th* *p th,sr* ⊺ *th pm,rf p,p th th,rf* + *λt* *th,pm* *pt−* 1 *pt− p − M* (*pt− p*) *η* *t∈T* X 0⊺ + *λ* *x* *dxd,t*0 *− x⁰d* *d∈D* X X ⊺ + *λ* *x* *d,txd,t*+1*− Adxd,t− Bdccd,t− Bdddd,t* *t∈T /tNd∈D* X X ⊺ *y c d* + *λ* *d,t* *yd,t− Cdxd,t− Ddcd,t− Dddd,t* *t∈T d∈D* X X*−*⊺ *y −* + *µ* *d,t* *y* *d,t* *− yd,t* *t∈T d∈D* X X+⊺ *y* + + *µ* *d,t* *yd,t− y* *d,t* *t∈T d∈D* X X*th th* *p th p,y p p,y q q,y* + *λ* *d,t* *pd,t− M* *d* *yd,t*+ *λ* *d,t* *pf,t− M* *d* *yd,t*+ *λ* *d,t* *q* *f,t− Mdyd,t* *t∈T d∈D* (9.2)

Note that *L*, which denotes the Lagrangian function, is a scalar term.

##### KKT conditions

The KKT conditions describe requirements that a solution for the convex optimization problem must fulfill to be regarded a global optimum. In the context of duality, the fulfillment of the KKT conditions is also the requirement for the equivalence of primal and dual solutions. In

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u> fact, the optimization can be solved by solving the KKT conditions, although this only practical for small problem sizes. The fundamental KKT conditions are 1) the stationarity condition,
2) the primal feasibility condition and 3) the complementary slackness condition. Note that compared to [55, p. 34, Equation 3.6], this assumes that dual feasibility condition is included in the complementary slackness condition. To begin with, the stationarity condition states that the partial differential of the Lagrangian
*sr* function *L* with regards to the primal variables *xd,t t,qtsr*must

|||||, c, y|, p, p, q ,p|,p|
|---|---|---|---|---|---|---|
|||||d,t d,t|th t t|t th,sr t|
|p ⊺|u ⊺|u|⊺ |u|,p|st|⊺ |s |,p||
|t|t st ⊺|t |s |,p p t|⊺|p ,p|q q ,p t||
|q ⊺|u ⊺|u|⊺ |u|,q|st|⊺ |s |,q||
|t|t ⊺ ts|t |s |,q p t|p ,q|q ⊺ t|q ,q||
|p ⊺|h ⊺|h,p|||||
|t|t q t|⊺ q ,p|p t|th,pm|p ,p||
||p||||||
|rf,th|t|rf,el|p|q|||
|t|th,pm|t|t|t|||
|x ⊺|x ⊺|y|⊺||0||
|d|d,t|d,t|d||||
|x ⊺|x ⊺|y|⊺||N||
|d,t−1|d,t|d d,t|d||||
|x ⊺|y ⊺|||N|||
|d,t−1|d,t|d|||||
|x ⊺|y|⊺ c||N|||
|d,t|dc d,t|d|||||
|y ⊺|c||N||||
|d,t|d||||||
|y ⊺|y ⊺|y ⊺|||||
|d,t|d,t p p d,t d|d,t ,y p d,t|p,y q d d,t|q,y d|||

equate to zero. Based on *L* from eq. (9.2), the stationarity conditions yields:

*−|u|,p*+ *f,*+ *f* 0 = (*λ*) *− µ M* + *µ M* + *µ M* *∀t ∈T* (9.3a) *t,*+ *t ls ls ls ls* + *µ M − λ* 1 + *M − λ M* *−|u|,q*+ *f,*+ *f* 0 = (*λ*) *− µ M* + *µ M* + *µ M* *∀t ∈T* (9.3b) *t,*+ *t ls ls ls ls* + *µ M − λ M − λ* 1 + *M* *th − th* 0 = *λ − µ M* *∀t ∈T* (9.3c) *th,b,*+ *th,b th pm* <u>1</u> *pm th* + *µ M − λ* 1 + *M* *η* *pm* <u>λ</u> *ls ls* 0 = *c* +*,* 0 = *c* + *λ,* 0 = *λ ∀t ∈T* (9.3d) *η* 0 0 = *λ − λ Ad− λ C ∀d ∈D, t* = *t* (9.3e)

0 = *λ − λ A − λ C ∀d ∈D, ∀t ∈T /t* (9.3f)

0 = *λ − λ C ∀d ∈D, t* = *t* (9.3g)

0 = *− λ B − λ D ∀d ∈D, ∀t ∈T /t* (9.3h)

0 = *− λ D ∀d ∈D, ∀t* = *t* (9.3i) *−* + 0 = *λ − µ* + *µ* *∀d ∈D, ∀t ∈T* (9.3j) *th th* *− λ M − λ M − λ M*

The primal feasibility condition states that that primal equality constraints have to hold. For the primal problem stated in eq. (9.1), this yields that eqs. (9.1e), (9.1f), (9.1i) to (9.1l), (9.1n) and (9.1o) have to hold as:

*sr* ⊺ *ls,rf pls,p rf pls,q rf* *pt−* 1 *pt*= *p* + *M* (*pt− p*) + *M* (*qt− q*) *∀t ∈T* (9.4a) ⊺ *ls,rf qls,p rf qls,q rf* *qtsr−* 1 *qt*= *q* + *M* (*pt− p*) + *M* (*qt− q*) *∀t ∈T* (9.4b) <u>1</u> *pm th*

||th,sr|⊺ th|pm,rf|p ,p|th|th,rf|
|---|---|---|---|---|---|---|
|th,pm|t|t|||t||

*p −* 1 *p* = *p* + *M* (*p − p*) *∀t ∈T* (9.4c) *η*

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u>

|x = x⁰|∀d ∈D|||
|---|---|---|---|
|d,t|d|||
|d,t+1|d d,t|dc d,t|dd d,t|
|d,t|d d,t p,y|d c d,t|d d d,t q,y|
|d,t|d d,t|d,t|d d,t|
|th|p ,y|||
|d,t|d d,t|||

(9.4d)

*x* = *A x* + *B c* + *B d ∀d ∈D, ∀t ∈T /t* *N* (9.4e)

*y* = *C x* + *D c* + *D d ∀d ∈D, ∀t ∈T* (9.4f) *p* = *M y, q* = *M y ∀d ∈D, ∀t ∈T* (9.4g) *th* *p* = *M y ∀d ∈D, ∀t ∈T* (9.4h)

Lastly, the complementary slackness condition states that the dual variable of an inequality constraint must be zero, unless that constraint is active, i.e. constraint expression equates to the bound. Based on the inequality constraints eqs. (9.1b) to (9.1d), (9.1g), (9.1h) and (9.1m) the complementary slackness condition yields:

*− rf |u|,p rf |u|,q rf u−* 0 *≤− |u |−|u |− M* (*pt− p*) *− M* (*qt− q*) *⊥µt≥* 0 *∀t ∈T* (9.5a)

*rf |u|,p rf |u|,q rf* + *u*+ 0 *≤− |u |* + *M* (*pt− p*) + *M* (*qt− q*) *−|u | ⊥µt≥* 0 *∀t ∈T* (9.5b)

*f,rf |sf|,p rf |sf|,q rf f,*+ *stf,*+ 0 *≤− |s |* + *M* (*pt− p*) + *M* (*qt− q*) *−|s | ⊥µ ≥* 0 *∀t ∈T* (9.5c) *t,rf |s |,ptrf |s |,qtrf t,*+*t,*+ 0 *≤− |s |* + *M* (*pt− p*) + *M* (*qt− q*) *−|s | ⊥µts≥* 0 *∀t ∈T* (9.5d) *th −*

|−|rf|h,p|th|th,rf|h||
|---|---|---|---|---|---|---|
||||t||t||
|th,b,rf||q ,p|th t|th,rf|th,b,+|q t|
|−||y|||||
|d,t|d,t +|d,t y|||||
|d,t|d,t|d,t|||||

0 *≤− h − h − M* (*p − p*) *⊥µ ≥* 0 *∀t ∈T* (9.5e) *th,b th th,b,*+ 0 *≤− q* + *M* (*p − p*) *− q ⊥µ ≥* 0 *∀t ∈T* (9.5f) *−* 0 *≤− y − y ⊥µ ≥* 0 *∀d ∈D, ∀t ∈T* (9.5g) + 0 *≤− y − y ⊥µ ≥* 0 *∀d ∈D, ∀t ∈T* (9.5h)

##### Dual problem

The dual problem is an optimization problem for finding the largest lower bound to the solution of the primal problem. This assumes that the primal problem is a minimization problem, such that the dual problem is a maximization problem. To this end, the dual problem is obtained by first deriving the minimum of the Lagrangian function with regards to the primal variables. This term constitutes the objective of the dual problem, where the dual problem is a maximization with regards to dual variables. The constraints of the dual problem are constituted by the KKT stationarity condition as well the non-negativity of the dual variables of inequality constraints,

i.e. the dual feasibility condition, which is contained in the KKT complementary slackness condition. Based on the Lagrangian function eq. (9.2) and to the KKT stationarity condition eq. (9.3),
144

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u> the dual problem is derived as:
" X *−*⊺ *− rf |u|,p rf |u|,q rf* max *µtu|u |−|u |* + *M p* + *M q* *u− u*+ *sf,*+ *t,*+ *pls* *µt,µt,µt,µts,λt, t∈T* *qls − qth,b,*+ *ppm x*0 *λh* *t,µt,µt,λt,λd,* *− y*+ *pth p q* *λxd,t,λyd,t,µyd,t,µd,t,λt,λt,λt* X *u*+⊺ *rf |u|,p rf |u|,q rf* + + *µt|u |− M p − M q −|u |* *t∈T* X *stf,*+⊺ *f,rf |sf|,p rf |sf|,q rf f,*+ + *µ |s |− M p − M q −|s |* *t∈T* X *t,*+⊺ *t,rf |s |,ptrf |s |,qtrf t,*+ + *µts|s |− M p − M q −|s |* *t∈T* X*ls* *p ls,rf pls,p rf pls,q rf* + *λt−p* + *M p* + *M q* *t∈T* X*ls* *q ls,rf qls,p rf qls,q rf* + *λt−q* + *M p* + *M q* *t∈T* X *h−*⊺ *− rf h,pthth,rf* + *µth − h* + *M p* *t∈T* X*th,b,*+⊺ *q th,b,rf qth,b,pthth,rf th,b,*+ + *µtq − M p − q* *t∈T* X*pm* *p pm,rf ppm,pthth,rf* + *λt−p* + *M p* *t∈T* X X X *x*0⊺ *x* ⊺ + *− λdx⁰d− λd,tBdddd,t* *d∈D t∈T /tNd∈D* X X ⊺ *y d* *− λ Dddd,t* *d,t* *t∈T d∈D* # X X*−*⊺ X+⊺ *y − y* + + *µ y − µ y* (9.6a) *d,t d,t d,t d,t* *t∈T d∈D d∈D*

s.t. (9.3) (9.6b) *u−u*+ *f,*+ *t,*+ *µt≥* 0*, µt≥* 0*, µts≥* 0*, µts≥* 0 *∀t ∈T*
(9.6c) *h−qth,b,*+ *µt≥* 0*, µt≥* 0 *∀t ∈T* (9.6d) *y−y*+ *µ ≥* 0*, µ ≥* 0 *∀t ∈T* (9.6e) *d,t d,t*

Note that for strong duality, which holds for convex optimization problems, the duality gap is zero. Therefore the optimal solution of the dual problem is not only a lower bound for the objective of the primal problem but in fact is equivalent to the objective of the primal problem.

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u> Inversely, if the problem is non-convex, the duality gap is not guaranteed to be zero and in turn the derived DLMP values may not appropriately represent the constraints of the MES operation problem.
##### DLMP derivation

As stated in the outline section above, the DLMPs describe the marginal cost of supplying load or the marginal utility of procuring generation at a particular grid node. To this end, DLMPs can be interpreted as the sensitivity for a change of the MES operation cost, i.e. the overall social welfare, for change in the power demand or injection at a particular node. This is directly linked to the interpretation of the dual variables, which can be termed as the sensitivities for a change of the objective value for a change in the constraint expression value. For MES operation, the objective value is indeed the MES operation cost. Therefore, the DLMPs are obtained based on the dual variables, by translating the change in the power demand or injection into a change of the constraint expression value.

For the MES optimal operation problem stated in eq. (9.1), the grid operation limits of the electric grid and the thermal grid are stated in eqs. (9.1b) to (9.1d), (9.1g) and (9.1h). The *f tt − th,b* constraint expressions essentially equate to the variables *|ut|, |st|, |s |, h, qt*. Therefore, the constraint expressions are proportional to the change in power demand or injection based on the respective sensitivity matrices of the linear electric grid model and the linear thermal grid model in eqs. (6.40) and (7.28). At the same time, the KKT stationarity condition readily states that the partial differential of the Lagrangian function with respect to active power, reactive power and thermal power in eqs. (9.3a) to (9.3c). Hence the DLMP components can be derived as expressions of the dual variables for the respective constraints:

|p,e|rf,el||||
|---|---|---|---|---|
|t|t||||
|p,u|u,p ⊺|u u|||
|t||t t|||
|p,s|s ,p|⊺|s ,p ⊺||
|t||ts||ts|
|p,ls|p ,p|⊺ rf,el|q ,p|⊺|
|t||t|||
|th,e|rf,th||||
|t|t||||
|th,h|h,p ⊺|h|||
|t||t th,pm|||
|th,q|q|,p ⊺ q|||
|t||t|th,pm||
|th,pm|p ,p|⊺|||
|t|p,e p,u t t|th,pm p,s p,ls t t|||
|th,e|th,h th,q|th,pm|||
|t|t t|t|||

*π* = *c* 1 (9.7a) *−* + *π* = (*M*) *µ − µ* (9.7b) *f f,*+ *t t,*+ *π* = *− M µ − M µ* (9.7c) *ls ls* *π* = *− M c − M* 0 (9.7d)

*π* = *c* 1 (9.7e) *th −* <u>1</u> *π* = *M µ* (9.7f) *η* *th,b th th,b,*+ <u>1</u> *π* = *− M µ* (9.7g) *η* *pm pm* <u>1</u> *π* = *− M* (9.7h) *η*

For the electric grid, the vectors *π*, *π*, *π*, *π* denote the DLMP components for electric energy, voltage support, branch power congestion and active power loss. For the thermal grid, the vectors *π, π, π, π* denote the DLMP components for thermal energy, pressure head support, branch flow congestion and pumping losses. Note that

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u> for the active, reactive and thermal power balance constraints, the dual variables become *p* *lsppmrf,el*
*f q* *ls*

|λ = λ|= c|1 and λ|= 0 according to eq. (9.3d). Also note that the electric grid|
|---|---|---|---|
|t|t p|t|t|
||t|||

*t t t t* *p* DLMPs *π* and thermal grid DLMPs *πtth*are obtained clearly independent from each other, as the coupling of the grids only exists through the DERs.

The complete DLMP values for the electric grid and the thermal grid are obtained as summa- tion of the components as:

||p p,e|p,u|p,s|p,ls|
|---|---|---|---|---|
||t t th,e tth t|t th,h t|t th,q t|t th,pm t|
|p||N|||
|t|tth||||

*π* = *π* + *π* + *π* + *π* (9.8) *π* = *π* + *π* + *π* + *π*

*Nel th* The vectors *π ∈* R and *π ∈* R are the nodal DLMP vectors for active power and thermal power. Note that only active power is considered in the electric grid, although an equivalent formulation can be included for reactive power. A further discussion of the interpretation of the DLMP components for different operational scenarios is provided in chapter11.

##### 9.3.4 Solution algorithm

Algorithm4presents the complete solution algorithm for the optimal operation problem. The solution process begins by obtaining the parameters for electric and thermal grid models as well as the DER state-space models. Based on the initialized models, the optimal operation problem is defined through the optimization solver interfaces. The solution of the numerical optimization solver is then handled by a dedicated solver, such as Gurobi. Once the solver obtains a solution, the primal variable values, i.e. the state and control variables, as well as dual variable values retrieved. Lastly, the DLMP values are determined based on the dual variable values.

<u>9. Multi-energy system operation problem formulations 9.3. Optimal operation problem</u>
**Algorithm 4:** Solution algorithm for the optimal operation problem **begin** electric and thermal grid model initialization: Obtain electric grid model parameters: *A* *f/t* *, Y, Y* *f/t* *, H, A* *d*; Obtain thermal grid model parameters: *A* *th,b* *, r* *th* *, d* *th* *,η* *pm* *,* ∆*h* *ets* *, A* *th,d*;

**begin** Reference power flow solution:

|rf f/t,rf|ls,rf|rf rf|
|---|---|---|
|rf th,b,rf|pm,rf|th,rf|

Solve electric power flow via algorithm1to obtain *u, s,s, p, q*; Solve thermal power flow via algorithm2to obtain *h, q,p, p*;

**begin** Linear electric and thermal grid model initialization: Obtain linear electric grid model matrices: *|u|,p |u|,q |sf|,p |sf|,q |s |,pt|s |,qtpls,p pls,q qls,p qls,q* *M, M, M, M, M, M, M, M, M, M*; *h,pthqth,b,pthppm,pth* Obtain linear thermal grid model matrices: *M, M, M*;

**begin** DER model initialization: **for** *d ∈D* *el* *∪D* *th* **do** Obtain state-space model: *th*

|||c|d −|+|p,y|q,y|p ,y|
|---|---|---|---|---|---|---|---|
|d,t d|dc dd|d d|d d,t|d,t|d|d|d|

*x* 0*, A, B, B, C, D, D, y, y, M, M, M*;

**begin** solve optimization problem Define optimization problem by passing eq. (9.1) into the solver interface; Invoke numerical optimization solver, e.g. Gurobi, on the problem definition; Retrieve state and control variables from the solver interface:

|x, c, y|, p, p, q ,p||,p ,q|;|||
|---|---|---|---|---|---|---|
|d,t d,t|d,t th t|t t th,sr t|sr t tsr||||
|u u|st st|p|q h|q|p||
|t t||t|t t|t|t||
|x x|y y|y p|p q||||
|d d,t p,ls th,e t t|d,t d,t th,h t|d,t t th,q th,pm t t|t t|p,e t|p,u t|p,s t|

Retrieve dual variables from the solver interface: *−* + *f,*+ *t,*+ *ls ls − th,b,*+ *pm* *µ, µ, µ, µ,λ,λ, µ, µ,λ*, 0 *−* + *th* *λ, λ, λ, µ, µ, λ, λ, λ*; Obtain DLMP value via eqs. (9.7) and (9.8): *π*, *π*, *π*, *π, π, π, π, π*;

## Part III

# Results and discussion

## 10 Study of electric vehicle charging in Singapore

#### Contents

10.1 Test case.................................... 150
10.1.1Overview................................ 150
10.1.2Electric grid................................ 151
10.1.3EV chargers.............................. 152
10.1.4Scenarios................................ 156
10.2 Results...................................... 157
10.2.1Uncontrolled charging.......................... 157
10.2.2Smart charging............................. 159
10.2.3Peak-shaving.............................. 159
10.2.4Price-based charging.......................... 159
10.3 Discussion.................................... 163
**Outline and contributions**

This chapter presents a study of the impact of EV charging on the electric distribution system in Singapore, based on a synthetic test case developed from publicly available data items. The elements of the test case are introduced in section10.1, which is followed by the presentation of results and discussion in sections10.2and10.3.

The test case for this study relies on 1) a synthetic electric grid test case for Singapore, which was developed in [50], [51], and 2) the synthetic EV charging demand, which was developed as an original contribution of this thesis. The execution of the study via MESMO and interpretation of the results was conducted independently by the author.

**10.1 Test case**
**10.1.1 Overview** For the study of electric vehicle charging in Singapore, a test case is developed for the Geylang district of Singapore.The test case is based on synthetic electric grid data in
150

<u>10. Study of electric vehicle charging in Singapore 10.1. Test case</u> section10.1.2and synthetic private EV charger demand data in section10.1.3, where different EV charger operation scenarios are evaluated according to section10.1.4. Note that only private EV charging is considered in this test case, i.e. taxi, private hire, logistics and electric bus charging are excluded. The reliance of synthetic data is due to confidentiality concerns with regards to real-world data. To this end, the study serves merely as a demonstration for the type of analysis which can be conducted through MESMO but the presented results are expected to contain a significant modeling error. However, a similar study is being conducted by TUMCREATE and Agency for Science, Technology and Research (A*STAR) in Singapore, where a test case based on real-world electric grid data is developed in MESMO and the City Mobility Simulator (CityMoS) [162], [163] is utilized for EV charger demand modeling. The numerical model parameters are only selectively included for EV chargers in the following, for the sake of brevity. However, the complete test case data, including the synthetic grid definition, is available within the MESMO repository as test case “thesis_troitzsch_202 1_ev_study”.
##### 10.1.2 Electric grid

The synthetic electric grid model from [51] is used in this test case to demonstrate the district-scale modeling capabilities on the electric grid side. The following of serves as a brief overview for the methodology that was applied for the preparation of the grid model but the interested reader is referred to [51] for a higher level of detail. An overview of the synthetic grid layout for the Geylang district is provided in fig.10.1, where 66/22 kV substations are depicted with red nodes and 22/0.4 kV substations with blue nodes. Note that although depicted as direct connections between nodes, the grid lines are assumed to follow the street layout, i.e. being layed as underground cables.

The synthetic grid is derived based on information for 1) postal-code-clustered demand estimates and 2) 66/22 kV substation locations. Since every building block in Singapore is assigned an individual postal code, this serves as a relatively detailed input for generating the 22 kV-load clusters. The information is augmented with an estimations for representative underground cable types based supplier information as outline in [51]. A power system plan- ning approach is devised to obtain the mapping and line layout between 66/22 kV substations and 22/0.4 kV substations, i.e. transformers at 22 kV-load clusters. For the presented test case, the substation rating is assumed to be in 100 MVA-units for 66/22 kV transformers and 1 MVA-units for 22/0.4 kV transformers. That means, the minimum transformer rating for 22/0.4 kV is 1 MVA and an appropriate integer value of transformers is deployed depending on the aggregate peak load at each 22/0.4 kV substation, where a maximum utilization of

0.9, i.e. a safety factor of 1.11, is assumed for the transformer rating. The base load time series is homogeneously defined for all 22 kV-load clusters based on a representative load shape from the aggregate demand data for Singapore, which is published along with price data by the EMC at [166].
151

<u>10. Study of electric vehicle charging in Singapore 10.1. Test case</u>
Figure 10.1: Synthetic grid layout for the Geylang district in Singapore.

EV penetration, EV / charger parameters

|Historical carpark|V ehicle inflow|Representative|Carpark|Fixed / flexible|
|---|---|---|---|---|
|availability|modelling|inflow / outflow time series|charging simulation|charger model time series|

Figure 10.2: Workflow for EV charger demand modeling.

##### 10.1.3 EV chargers

##### Overview

Figure10.2highlights the main steps for the derivation of the EV charger models for private EV charging. First, historical carpark availability data is used to derive representative vehicle inflow and outflow time series for existing carparks in the study area through probabilistic

10. Study of electric vehicle charging in Singapore 10.1. Test case

|following.|modeling. Second, a carpark charging simulation is computed based on the representative vehicle inflow, outflow, EV penetration and EV / charger parameters. This serves to obtain the required input time series for the definition of fixed EV chargers and flexible EV chargers in MESMO according to sections8.2.2and8.3.3. Table10.1highlights the input data items that were utilized for EV charging demand mod- eling. In addition, the technical parameters for the EVs as well as chargers are defined in table10.2and EV penetration scenarios are introduced in table10.3. Note that the estimated aggregated private EV charging demand in table10.3is determined based on the private car population, average vehicle driving distance and EV energy consumption from table10.2. This value serves as a correction reference for the carpark charging simulation results in the Table 10.1: EV charging demand input data.|||
|---|---|---|---|
|Data item|Description||Source|
|Historical carpark availability|• Time series data of available carpark lots for indi- vidual carparks. Contains a selection of public residential, commer- • cial and mixed-use carparks in Singapore, particu- larly at public housing developments, government- operated general public carparks and large-scale mixed-use developments, e.g. malls with attached office blocks. • Recorded at 10 min interval ber 2018 and March 2020.|between Septem-|LTA Datamall API [167]|
|Carpark capacity|• List of total carpark lots and geographical locations for individual carparks. • The number of total carpark lots is estimated from the maximum recorded available lots per carpark. Table 10.2: EV and charger parameters.||LTA Datamall API [167]|
||Parameter Private car population (Singapore) Vehicle driving distance (Singapore), mean value|Value 520 000 48 km/d|Source [168], [169] [170]|
||Vehicle driving distance (Singapore), standard deviation|16 km/d|Assumed|
||EV energy consumption|170 W h/km|[171]|
||Charger efficiency|95 %|Assumed|
||Charger power factor|0.95|Assumed|
||Slow charger active power|7.4 kW|Assumed|
||Slow charger share|75 %|Assumed|
||Fast charger active power|50 kW|Assumed|
||Fast charger share|25 %|Assumed|

10. Study of electric vehicle charging in Singapore 10.1. Test case
Table 10.3: EV penetration scenarios.

##### Estimated total private EV charging

##### Penetration scenario demand (Singapore)

Baseline (0 % EVs)- 25 % EVs 1 060.8 MW h/d 75 % EVs 2 121.6 MW h/d 100 % EVs 4 243.2 MW h/d

##### Vehicle flow modeling

The historical carpark availability time series is provided as time series for each week of collected data. Data collected after March 2020 is discarded due to the assumed change in travel patterns due to the COVID-19 pandemic. Due to temporary failures of the API and the recording system, the data is incomplete and may contain erroneous values. To remove erroneous entries, the carpark availability data is filtered in three steps. First, negative values in each time series are removed. Second, carparks with a highly stagnant time series, i.e. those with no change in values in more than 25 % of all time steps, are removed from the data set. Third, highly volatile time series, i.e. those with average absolute value difference in adjacent time steps of more than 5 % of their maximum value range, are dropped from the data set. *veh,in veh,out* The vehicle inflow time series *nc,t*and vehicle outflow time series *nc,t*for each carpark *c* are obtained by taking the difference of adjacent time steps in the availability time series *lot,avl* *nc,t*. To this end, the vehicle inflow corresponds to negative differences and the vehicle outflow corresponds to positive differences in the availability time series as:

*veh,in lot,avl lot,avl rep lot,tot lot,avl* *nc,t*= max 0*,n* *c,t−*1 *− nc,t*+ *f* ∆*t ncnc,t*(10.1a)

*veh,out lot,avl lot,avl rep lot,tot lot,avl* *nc,t*= max 0*,nc,t− n* *c,t−*1 + *f* ∆*t ncnc,t*(10.1b)

*lot,avl lot,tot* The symbols *nc,t*and *n* denote the number of available lots at time step *t* and the total number of lots at carpark *c*. The scalar *f* *rep* denotes the static vehicle replacement factor and ∆*t* is the time step interval length. The static vehicle replacement factor addresses the concern that overlapping vehicle departures and arrivals within the same time step are not captured by taking the difference of the availability time series. For the presented study, the value *f* *rep* = 10 %*/*h is assumed for carparks in Singapore.

The vehicle inflow and outflow data is then aggregated into a representative time series for a single week for each carpark, i.e. grouping the values by weekly time-period (see definition of time-periods inNotation) and taking the mean value across all samples. Note that seasonality in the data is not captured because this is not of interest for the test case. Carpark time series with any missing values after aggregation, i.e. those with less than one week of recorded data, are dropped from the data set. The representative time series serve as an input to a Poisson process in the carpark simulation, rather than being directly interpreted as inflow and outflow values.

<u>10. Study of electric vehicle charging in Singapore 10.1. Test case</u>
##### Carpark charging simulation

|Determine EV|Assign EVs to|Charge EVs /|Clear departing|Departing energy|
|---|---|---|---|---|
|arrivals /|chargers|clear charged|EVs|time series|
|departures||EVs|||

|EV penetration,|Fixed charging|Maximum|Max. / min.|
|---|---|---|---|
|EV / charger parameters|power time series|charged energy time series|charging power time series|

Repeat for each timestep Representative inflow / outflow time series

Figure 10.3: EV carpark simulation.

The carpark charging simulation serves to determine the EV charging time series from the representative vehicle inflow and outflow time series. The relevant outputs of the charging simulation are the fixed charging power time series, i.e. for the fixed EV charger model according to section8.2.2, as well as maximum charging power / minimum charging power / maximum charged energy / departing energy time series, i.e. for the flexible EV charger model according to section8.3.3. As depicted in fig.10.3, the simulation is formulated as an iterative process consisting of the following steps:

1. Determine the inflow and outflow of EVs by inhomogeneous Poisson process based on the representative vehicle inflow and outflow time series and the EV penetration scenario.
2. Assign arriving EVs to free chargers or the the waiting vehicle queue if all chargers are occupied.
3. Determine the fixed charging power for the occupied chargers, then charge EVs and clear any EVs which have been fully charged to the parking vehicles queue. The maximum charging power / minimum charging power / maximum charged energy are also determined in this step.
4. Remove departing EVs from the parking vehicle queue and determine the departing energy time series.
The inflow and outflow of EVs are modeled as inhomogeneous Poisson processes, i.e. two Poisson processes with different vehicle arrival / departure probability in each time step. To this end, the representative vehicle inflow and outflow are interpreted as the rate parameters for the Poisson processes. Sampling from the Poisson processes, the vehicle inflow and outflow are obtained for each carpark. The inflow and outflow values are then scaled by the

10. Study of electric vehicle charging in Singapore 10.1. Test case EV population share depending on the penetration scenario from table10.3to determine the EV arrivals and departures. The energy demand of arriving vehicles is determined by sampling a normal distribution for the vehicle driving distance, based on the parameters in table10.2. The EVs from the arriving vehicles queue are assigned to free EV chargers. The number of EV chargers for each charger type, i.e. slow / fast, is defined based on charger projections in the carpark capacity data set (see table10.1. The charger assignment algorithm will allocate EVs to slow chargers first. Only if the slow chargers are filled up, then fast chargers are assigned. If there are more EVs arriving then there are free chargers, the unserved EVs are kept in the waiting vehicles queue and are assigned in later iterations, once chargers are freed up. In the next step, the fixed charging power is calculating by taking the total rated power of all occupied chargers for the current time step. At the same time, the maximum and minimum charging power are determined based on the number of EVs currently charging or in the parking vehicles queue, where the minimum charging power defaults to zero in the presented test case as no V2G is considered. The maximum charged energy is determined based on the total energy demand of vehicles charging or in the parking vehicles queue. The EVs are then charged for the current time step. If any EV is fully charged, it is moved to the parking vehicle queue. In the last step, departing vehicles are removed from the parking vehicles queue. This serves to determine the departing energy. The four steps steps of the carpark charging simulation are iterated until the complete time series for a full week are obtained.
##### 10.1.4 Scenarios

The following asses the impact of EV charging with respect to different EV charging operation scenarios as outlined in table10.4. While each EV operation strategy is characterized by a different objective, all scenarios are based on the same EV charger models from section10.1.3, where the different EV penetration levels are compared across all scenarios.

Table 10.4: Scenarios for the study of EV charging in Singapore.

##### Scenario Objective

1 Uncontrolled charging Minimize charging time 2 Smart charging Minimize grid impact 3 Peak-shaving Minimize aggregate DER demand 4 Price-based charging Minimize total DER energy cost

The different charging scenarios can be interpreted as follows:

- **Uncontrolled charging** describes a charging behavior without any intervention by the charging station operator. In this scenario, the EVs are charged as soon as possible
156

<u>10. Study of electric vehicle charging in Singapore 10.2. Results</u> after their arrival. Therefore, the charging demand is only governed by the arrival of EVs at the charging station.
- **Smart charging** is a hypothetical best-case scenario, where the electric grid operator assumes direct control of the charging process. In this case, the charging schedule is optimized with the objective of minimizing the aggregated peak utilization of all branches, i.e. the sum of the peak utilization experienced by all branches.
- **Peak-shaving** defines a peak minimization objective across the total aggregate charg- ing demand of all charging stations. This scenario assumes a district-scale charging station operator to control of the EV charging process but without any direct considera- tion of the electric grid utilization.
- **Price-based charging** describes a price-based charging scenario based on histor- ical wholesale electricity prices. In this case, each charging station operator would minimize their total energy costs, thereby rescheduling EV charging to cheap price periods. Importantly, this does not consider DLMPs, but only transmission-system-level prices. Also, no peak demand surcharge is considered in this hypothetical scenario. Representative wholesale electricity prices were obtained from the historical price data published by the EMC for Singapore’s wholesale market.
#### 10.2 Results

##### 10.2.1 Uncontrolled charging

For the uncontrolled charging scenario, fig.10.4in its lower portion depicts the cumulative distribution of substation transformer utilization in the test case area. The upper portion of fig.10.4describes the distribution of the transformer utilization with a box plot. The utilization level is calculated as the ratio of peak loading to the rated loading of the transformers. Recall from section10.1.2that 22/0.4 kV transformers are assumed to occur in 1 MVA- units. To this end, a large proportion, i.e. as much as 85 % of transformers experience between 0.1 to 0.3 utilization in the baseline scenario (0 % EVs) because load clusters can be significantly smaller than 1 MVA in the synthetic grid. In the baseline scenario, nearly 100 % of substations are loaded below 0.9, where the median utilization occurs at approx. 0.11 and the mean utilization at approx. 0.21. With increasing EV penetration, the share of substation transformers loaded below 0.9 falls to approx. 94 % for 25 % EVs and below 90 % for both 75 % and 100 % EVs. The median substation utilization increases to approx. 0.15 and remains constant across the higher penetration levels, since the substations with allocated charging demand occur consistently above the median level. The mean utilization increases proportionally to the EV penetration level, i.e. up to approx. 0.5. Note that the plot is truncated at the utilization level 1.0 for consistency, although higher-level EV penetration scenarios can cause significant overloading of selected transformers due to the highly localized nature of these loads.

Figure10.5highlights the utilization of electric grid lines in the test case, with a cumulative distribution in the bottom and a box plot at the top. In Singapore’s electric distribution system,

<u>10. Study of electric vehicle charging in Singapore 10.2. Results</u>
0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1

0.9
0.8
0.7
0.6
0.5

|0.5|||
|---|---|---|
|0.4||%DVHOLQHVFHQDULR|
|0.3||25% EVs (uncontrolled)|
|Cumulative proportion0.2||75% EVs (uncontrolled)|
|0.1||100% EVs (uncontrolled)|
|0|||
|0 0.1|0.2 0.3 0.4 Maximum transformer utilization [p.u.]|0.7 0.8 0.9|

0.5 0.6 1
Figure 10.4: Substation transformer utilization for uncontrolled charging.

0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1

0.9
0.8
0.7
0.6

|0.6|||
|---|---|---|
|0.5||%DVHOLQHVFHQDULR|
|0.4||25% EVs (uncontrolled)|
|Cumulative proportion0.3||75% EVs (uncontrolled)|
|0.2||100% EVs (uncontrolled)|
|0.1|||
|0 0.1|0.3 0.4 0.5 Maximum line utilization [p.u.]|0.7 0.8 0.9|

0.2 0.6 1
Figure 10.5: Line utilization for uncontrolled charging.

<u>10. Study of electric vehicle charging in Singapore 10.2. Results</u> grid lines are significantly oversized based on the preference for reliability of the government- owned transmission licensee, i.e. SP Group, which has been accounted for in the synthetic grid model from section10.1.2. To this end, 100 % of lines are loaded well below 0.4 with the median and mean utilization occurring at approx. 0.15. With increasing EV penetration levels, the line utilization mean and median increase proportionally up to approx. 0.23. The distribution of maximum nodal voltage drops is depicted with a histogram and a box plot in fig.10.6. The voltage drops is determined as the ratio between maximum voltage drop and nominal voltage at each node. Note that this does only consider the voltage at primary nodes at 22 kV-level and excludes voltages at the secondary side of 22/0.4 kV substations. The voltage drops remain well below 0.03 for all EV penetration scenarios. These low levels are in line with the relatively low utilization of grid lines based on fig.10.5and the electric line parameters in section10.1.2. Although the voltage drop mean and median increase proportionally to the EV penetration, their levels remain below 0.01 for all scenarios. Lastly, fig.10.7depicts the aggregate active power demand time series for the test case across different EV penetration levels. Note that even at 100 % EVs, the EV charging demand only accounts for less than 20 % of the peak demand. However, EV charging succeeds in creating highly localized substation overloading issues according to fig.10.4due to the highly concentrated occurence of the demand.
##### 10.2.2 Smart charging

Figure10.8depicts a comparison of the substation utilization for smart charging and uncon- trolled charging across the different EV penetration levels. For 25 % EVs, the smart charging increases the share of transformers loaded below 0.9 from approx. 94 % to approx. 99 % and the mean utilization is decreased by approx. 0.08. For higher penetration levels the benefit of smart charging reduces proportionally. At 100 % EVs, share of transformers loaded below

0.9 only increases by approx. 1 %, although mean utilization decreases by approx. 0.08, i.e. similar to 25 % EVs and 75 % EVs. This behavior is due to the very high peak load at local substations, i.e. even a significant flattening of demand peaks still leads to highly overloaded substations in the 100 % EV penetration scenario.
##### 10.2.3 Peak-shaving

Figure10.9depicts the impact of different operational objectives on the aggregated demand shape. Peak shaving leads to a noticeably flatten peak demand compared to smart charging. However, as shown in fig.10.10, peak shaving is not able to significantly lower the substation utilization compared to uncontrolled charging. The mean substation utilization decreases only by approx. 0.01 for peak shaving compared to 0.08 for smart charging.

##### 10.2.4 Price-based charging

Figure10.11highlights the impact of price-based charging onto the aggregated demand shape. In this case, large charging peaks occur during low price periods in the wholesale

<u>10. Study of electric vehicle charging in Singapore 10.2. Results</u>
0 0.005 0.01 0.015 0.02 0.025 0.03

0.15

|0.1|||
|---|---|---|
|)UHTXHQF\||%DVHOLQHVFHQDULR|
|0.05||25% EVs (uncontrolled) 75% EVs (uncontrolled) 100% EVs (uncontrolled)|
|0 0|0.01 Maximum voltage drop [p.u.]|0.02 0.025|

0.005 0.015 0.03
Figure 10.6: Node voltage drop for uncontrolled charging.

25% EVs (uncontrolled) (9FKDUJLQJ 200 Base load 150 100 50 0 75% EVs (uncontrolled) 200 150 100 50 0 Active power [MW] 100% EVs (uncontrolled) 200 150 100 50 0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Figure 10.7: Aggregated active power demand schedule for uncontrolled charging.

<u>10. Study of electric vehicle charging in Singapore 10.2. Results</u> 0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1 1
0.9
0.8
0.7
0.6
0.5
0.4
0.3 %DVHOLQHVFHQDULR
0.2 25% EVs (uncontrolled)
Cumulative proportion

0.1 25% EVs (smart charging) 0 00 0.1 0.1 0.2 0.2 0.3 0.3 0.4 0.4 0.5 0.5 0.6 0.6 0.7 0.7 0.8 0.8 0.9 0.9 11
Maximum transformer utilization [p.u.]

0.9
0.8
0.7
0.6
0.5
0.4
0.3 %DVHOLQHVFHQDULR
0.2 75% EVs (uncontrolled)
Cumulative proportion

0.1 75% EVs (smart charging) 0 00 0.1 0.1 0.2 0.2 0.3 0.3 0.4 0.4 0.5 0.5 0.6 0.6 0.7 0.7 0.8 0.8 0.9 0.9 11
Maximum transformer utilization [p.u.]

0.9
0.8
0.7
0.6
0.5
0.4
0.3 %DVHOLQHVFHQDULR
0.2 100% EVs (uncontrolled)
Cumulative proportion

0.1 100% EVs (smart charging) 0 0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1
Maximum transformer utilization [p.u.]

Figure 10.8: Substation transformer utilization for smart charging.

<u>10. Study of electric vehicle charging in Singapore 10.2. Results</u>
100% EVs (uncontrolled) (9FKDUJLQJ 200 Base load 150 100 50 0 100% EVs (smart charging) 200 150 100 50 0 Active power [MW] 100% EVs (peak shaving) 200 150 100 50 0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Figure 10.9: Aggregated active power demand schedule for peak-shaving.

0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1

0.9
0.8
0.7
0.6
0.5
0.4

|0.4|||
|---|---|---|
|0.3||100% EVs (uncontrolled)|
|0.2||100% EVs (smart charging)|
|Cumulative proportion0.1||100% EVs (peak shaving)|
|0|||
|0 0.1|0.2 0.3 0.4 Maximum transformer utilization [p.u.]|0.7 0.8 0.9|

0.5 0.6 1
Figure 10.10: Substation transformer utilization for peak-shaving.

<u>10. Study of electric vehicle charging in Singapore 10.3. Discussion</u>
100% EVs (uncontrolled) (9FKDUJLQJ 300 Base load 200 100 0 100% EVs (smart charging) 300 200 100 0 Active power [MW] 100% EVs (price based) 300 200 100 0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Figure 10.11: Aggregated active power demand schedule for price-based charging.

0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1

0.9
0.8
0.7
0.6
0.5
0.4

|0.4|||
|---|---|---|
|0.3||100% EVs (uncontrolled)|
|0.2||100% EVs (smart charging)|
|Cumulative proportion0.1||100% EVs (price based)|
|0|||
|0 0.1|0.2 0.3 0.4 Maximum transformer utilization [p.u.]|0.7 0.8 0.9|

0.5 0.6 1
Figure 10.12: Substation transformer utilization for price-based charging.

electricity price schedule. As depicted in fig.10.10, this leads to an increase in the mean substation utilization to approx. 0.73 from approx. 0.5 in the uncontrolled scenario and approx.

0.4 in the smart charging scenario. Note that the share of highly loaded transformers does not increase significantly, as the substations with EV demand are already highly overloaded in the uncontrolled scenario.
#### 10.3 Discussion

Recall that this study serves merely as a demonstration for the type of analysis which can be conducted with MESMO but the presented results are expected to contain a significant

<u>10. Study of electric vehicle charging in Singapore 10.3. Discussion</u> modeling error, due to reliance on synthetic input information. For the selected test case, the key takeaways are threefold:
- First, the overall system utilization remains very close to baseline utilization. The overutilization only affects a few substations in a very localized fashion, since the charging demand in the synthetic test case is concentrated at very few nodes. In this regard, the substation utilization can be taken as the key indicator for grid utilization based on section10.2.1, due to relatively low line loading and associated low voltage drops.
- Second, the in the selected test case smart charging had the highest impact at relatively low EV penetration levels according to section10.2.2but not at high penetration levels, due to the relatively high overloading of substations.
- Third, the results of section10.2.4highlight the importance of designing appropriate pricing mechanism or energy market frameworks for EV charging that take into account the grid limitations. This serves as a motivation for the study of combined thermal and electric grid operation in the following chapter11, where the suitability of distribution location marginal prices (DLMPs) to reflect operational limitations in the both thermal and the electric are discussed.
Importantly, EV charging does not create system-wide congestion in the synthetic test case. Since EV charging, if controlled appropriately, may introduce significant flexibility to the system, its deployment may be readily manageable with limited system upgrades in conjunction with market-based incentives for smart charging.

## 11 Study of combined thermal and electric grid operation

#### Contents

11.1 Test case.................................... 166
11.1.1Overview................................ 166
11.1.2Electric grid................................ 167
11.1.3Thermal grid.............................. 168
11.1.4Flexible buildings............................ 168
11.1.5Scenarios................................ 169
11.2 Results..................................... 170
11.2.1Baseline................................. 170

|11.2.2|Constrained branch flow in the thermal grid.||||..|.....|....|.. 172|
|---|---|---|---|---|---|---|---|---|
|11.2.3|Constrained node head in the thermal grid.||||..|.....|....|... 174|
|11.2.4|Constrained branch power in the electric grid.||||.|.....|....|.. 176|
|11.2.5|Constrained node voltage in the electric grid.||||.|.....|....|... 177|
|11.2.6|High-cost cooling plant in the thermal grid.||||..|.....|....|.. 179|
|11.2.7|Low-cost cooling plant in the thermal grid.||||...|.....|....|.. 179|
|11.2.8|Low-cost generator in the electric grid.||||.....|.....|....|.. 180|
|11.3 Discussion.||......|......|.....|......|.....|....|.. 182|

11.2.2Constrained branch flow in the thermal grid.............. 172
.

**Outline and contributions**

This chapter present a study of DLMPs in the context of a combined optimal operation of district-scale electric and thermal grids, based on a synthetic test case for Tanjong Pagar, Singapore. The focus was on examining and interpreting the behavior of DLMPs in comparison for different operational scenarios. The test case and the considered operational scenarios are described in section11.1.Then, results and discussion are presented in sections11.2and11.3.

The test case for this study was first developed as part of the Connecting District Energy and Power Systems in Future Singaporean New Towns (CONCEPT) project with participation of the author and relies on previous works published in [26], [52]. The author adapted the test

<u>11. Study of combined thermal and electric grid operation 11.1. Test case</u>
**Tanjong Pagar** **Port Terminal**

**Pulau Brani**

**Sentosa**

Figure 11.1: Test case area at the Tanjong Pagar Port Terminal. Figure taken from [39].

case to derive the thermal grid definition and developed the operational scenarios. A version of this test case was also utilized for the master theses [39], [40], which were supervised by the author. The execution of the study via MESMO and interpretation of the results was conducted independently by the author.

#### 11.1 Test case

##### 11.1.1 Overview

The following presents a study of combined thermal and electric grid operation, which highlights the ability of MESMO to describe operation problems of MESs. The test case is based on a greenfield urban planning project which is located at the Tanjong Pagar Port Terminal in Singapore. As part of Singapore’s ongoing urban redevelopment efforts, the port area is intended to be restructured into a high-density district with commercial, residential and retail occupancy. The test case, which was originally developed as part of the works [39], [40], [52], consists of a portion of this district as illustrated in fig.11.1.

Figure11.2highlights the district-scale energy systems which are part of the test case:

- 22 buildings, which have been modeled as flexible buildings according to section8.3.4. The building models are originally based on GIS building shapes and parameters from a test case of the City Energy Analyst (CEA) [26] as described in section11.1.4. All buildings are assumed be connected to both the electric grid and the thermal grid.
166

<u>11. Study of combined thermal and electric grid operation 11.1. Test case</u>
Thermal grid Electric grid 21

4 19 3 20

||16|20|||
|---|---|---|---|---|
|||||22|
|5|||||
|||17|1||
|10|14||||
|13 8|15|2|18||
|11|9||||
||||7 6||
|12|||||

##### Source

Figure 11.2: Test case layout with thermal grid, electric grid and flexible buildings.

- The electric distribution grid at 22 kV-level, which consists of 45 nodes and 33 lines. The grid layout is derived based on a minimum spanning tree for connecting all buildings to the 22 kV-substation, as described in section11.1.2.
- A district cooling system (DCS) and its associated thermal grid, which is assumed to congruent to electric grid, i.e. each thermal grid node coincides with an electric grid node. Further thermal grid model parameters are highlighted in section11.1.3.
The numerical values of the electric grid, thermal grid and flexible building model parameters are excluded in the following for the sake of brevity. However, the complete test case definition is available within the MESMO repository as test case “thesis_troitzsch_2021_dlmp_stu dy”.

##### 11.1.2 Electric grid

The synthetic electric grid definition for the test case is obtained by applying a simplified power system planning approach. As input serves GIS data of the street network and the building polygons at the test case site as shown in fig.11.3. In a first pre-processing step, the grid interconnection point of each building is determined by finding the shortest distance between any building’s centroid and the nearest street line, which is also highlighted in fig.11.3. This is based on the assumption that possible line paths are routed along the street network, as modern distribution grid lines are routed underground below streets. In the next step, a minimum spanning tree is obtained for the district such that all building interconnection points are linked to the source node. This is under the assumption that the source node is located at the bottom left according to fig.11.2. In the last step, the electric line types for each line segment are determined through a planning optimization based on [52]. To this end, the sizing of the electric lines is based on the peak load, i.e. the maximum nominal load

<u>11. Study of combined thermal and electric grid operation 11.1. Test case</u>
21

4 19 3 20

||16|20||
|---|---|---|---|
|5||||
|||17|1|
|10|14|||
|13 8|15|2|18|
|11|9|||
||||7 6|
|12||||

Figure 11.3: Street layout at the test case site.

of the 22 flexible buildings, which are described below in section11.1.4. The data for electric grid line types are derived from local supplier data based on the work of [50], [51].

##### 11.1.3 Thermal grid

The thermal grid is defined in an equivalent fashion to the electric grid. That means, building connection points and a minimum spanning tree are derived from the street layout GIS data according to fig.11.3. Then, the sizing of the distribution pipes is based on the peak load, i.e. the maximum nominal load of the 22 flexible buildings. The data for thermal grid pipe types is based on the work of [39].

##### 11.1.4 Flexible buildings

The flexible buildings are defined according to section8.3.4. The geometric information of zones and surfaces is derived from the GIS data for the buildings shapes in the test case. Based on the default Singapore database of CEA [26], the heat transfer coefficients, the absorption coefficients and the emissivity of each surface as well as the transmissivity of each window are derived. The thermal heat capacity and the infiltration rate of each zone are defined according to ISO 13790. Further, the HVAC system heating efficiency and cooling efficiency are calculated according to CEA, based on the building’s assumed system setup. The average annualized consumption of the buildings was cross-validated against historic values from Singapore’s building and construction authority (BCA) [172]. The occupancy schedule and the fixed base electric load schedule are also defined according to the occupancy type databases of CEA [26]. Weather data is obtained for Singapore database from the EnergyPlus weather data repository. The data comprises data items for the ambient temperature and the global horizontal irradiation. The incident irradiation for each surface direction is calculated as a function of the global horizontal irradiation and the local time

<u>11. Study of combined thermal and electric grid operation 11.1. Test case</u>
Thermal grid Electric grid 21

4 23 19 24 3 **C** 20 16 22 5 17 1 10 14 13 8 15 2 18 11 9 **B** **A** 7 6 12

##### Source

Figure 11.4: Test case layout with nodes of interest “A”, “B” and “C” highlighted.

through the PVLIB toolbox [173]. The sky temperature is defined by an approximation for tropical climate according to ISO 52016-1.

##### 11.1.5 Scenarios

Table11.1outlines the operational scenarios which are studied for the Tanjong Pagar test case in the following. The scenarios are selected to highlight and compare the features of distribution locational marginal prices (DLMPs) for both the thermal grid and the electric grid. These exemplary operational constraints are distinguished into the following types:

- **Branch flow limit** in the thermal grid, i.e. an upper bound on the volume flow rate across pipes in the thermal grid. For this study, the limit is imposed at branch “A-B”, i.e. the pipe connecting nodes “A” and “B” as highlighted in fig.11.4.
- **Node head limit** in the thermal grid, which describes an upper bound on the node head difference between primary and secondary side of distribution piping system. In reality, this would reflect to the operational capabilities of distribution pumps at ETSs. For this study, the constraint is applied at node “B” according to fig.11.4.
- **Branch power limit** in the electric grid, which define an upper bound on the current carrying capacity on electric grid lines. Similar to the branch flow limit, this is imposed at branch “A-B”, i.e. the line connecting nodes “A” and “B” as shown in fig.11.4.
- **Node voltage limit** in the electric grid, which describes an upper bound on the voltage drop in the electrical system. Technically, this would also include an upper bound on the voltage but the presented test case does not consider significant generation facilities and thus the voltage drop is assumed to remain positive. Similar to the node head limit, this constraint is applied at node “B” as depicted in fig.11.4.
169

11. Study of combined thermal and electric grid operation 11.2. Results

|Table 11.1: Scenarios for the study of combined thermal and electric grid operation.|||||||
|---|---|---|---|---|---|---|
|Scenario|Branch flow limit|Node head limit|limit Branch power|limit Node voltage|Additional cooling plant|generator Additional elec.|
|Baseline 1|||||||
|Constrained branch flow in the thermal grid 2|✓||||||
|Constrained node head in the thermal grid 3||✓|||||
|Constrained branch power in the electric grid 4|||✓||||
|Constrained node voltage in the electric grid 5||||✓|||
|High-cost cooling plant in the thermal grid 6|✓||||✓||
|Low-cost cooling plant in the thermal grid 7|✓||||✓||
|Low-cost generator in the electric grid 8|||✓|||✓|

Additionally, the presented study the considers the introduction of additional generation facilities in the thermal grid and electric in scenarios 6 to 8. In the thermal grid, additional generation is introduced in the form of a secondary cooling plant, which is connected as DER 23 at node “C” as depicted in fig.11.4. In scenario 6, the cooling plant is assumed to be “high-cost”, i.e. the COP of the secondary cooling plant is lower than the COP of the primary cooling plant at the source node. In scenario 7, a “low-cost” plant is considered, where the COP of the secondary cooling plant is higher than the COP of the primary cooling plant. In the electric grid, the additional generator is assumed to take the form of a solar PV plant as DER 24 at node “C” in scenario 8, where the marginal cost is assumed to be lower than the wholesale electric energy price. The deployment of additional generators is augmented with branch constraints in order to study the impact of the generation facilities on the DLMPs.

#### 11.2 Results

##### 11.2.1 Baseline

For the baseline scenario, no thermal or electric grid constraints are imposed according to table11.1. To this end, fig.11.5depicts the DLMPs and dispatch schedules for active and thermal power at DER 22 under nominal operation conditions. DER 22, i.e. flexible building 22, is connected at node “C” according to fig.11.4. This DER is selected as representative here in the following scenarios due to its location at the far end of the grid. Figure11.5depicts the thermal power DLMP and thermal power dispatch at the top and active power DLMP and active power dispatch at the bottom. The DLMPs are shown as a solid black line, where individual DLMP components are highlighted as color shade in the background of the plot. For the basline scenario, both thermal power and active power DLMPs are dominated by their energy component, i.e. the thermal energy or electric energy price at the source node

<u>11. Study of combined thermal and electric grid operation 11.2. Results</u>
Thermal power DLMP and dispatch schedule at DER 22

1.00 DLMP total
15 (Thrm. pw.)

0.75
Congest. 10 0.50 Head Pumping 5 0.25 Power [p.u.] Energy ����������������

0.00 Thrm. pw.
0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Active power DLMP and dispatch schedule at DER 22

1.00 DLMP total
75 (Active pw.)

0.75
Congest. 50 0.50 Voltage Loss 25 0.25 Power [p.u.] Price [S$/MWh] Energy

0.00 Active pw.
0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Figure 11.5: DLMPs and dispatch schedules at DER 22 for scenario 1 (Baseline).

of the respective grid. For the thermal grids, the source node energy price is determined by the electric energy prices multiplied with the efficiency of the primary cooling plant. Since the cooling plant efficiency is assumed to be constant, the thermal power’s energy DLMP component is proportional to the electric energy price, i.e. the active power’s energy DLMP component.

Recall that flexible buildings are connected to both the thermal grid and the electric grid at the same time. Therefore, the thermal power demand for space cooling can be supplied either directly from the thermal grid or from the building-level cooling plant by consuming electric power from the electric grid. In fig.11.5, the cooling demand is supplied from the thermal grid because the primary cooling plant has a higher COP than the building-level cooling plant. Therefore, thermal energy supply from the primary cooling plant incurs lower energy costs. The active power dispatch schedule is dominated by energy demand for pumps and fans for distribution of space cooling within the building, which is proportional to the thermal power dispatch schedule. Additionally, there is active power demand due to other appliances within the building, i.e. the fixed base load schedule.

Figure11.6depicts the nodal values of thermal power DLMPs across the thermal grid at 12:00, which is chosen as a representative time step here and in the following scenarios. The DLMP values are shown for the energy component in top left, for the pump component in the top right, for the head component in the bottom left and for the congestion component in the bottom right. Recall from above that the energy component reflects the cost of thermal power production at the primary cooling plant at the thermal grid source node. To this end, the value of the energy component is identical across all nodes of the network. The DLMP pump component expresses energy cost for distribution pumping due to thermal power consumption at the individual nodes. Therefore, the pump component increases proportionally to the

<u>11. Study of combined thermal and electric grid operation 11.2. Results</u> Thermal grid energy DLMP at 12:00 Thermal grid pump DLMP at 12:00
17.2
0.190
17.0
16.8 0.185
16.6 0.180 ���������������� ����������������
16.4
0.175
Thermal grid head DLMP at 12:00 Thermal grid congestion DLMP at 12:00

1.0 1.0
0.8 0.8
0.6 0.6
0.4 0.4 ���������������� ����������������
0.2 0.2
0.0 0.0
Figure 11.6: Thermal grid DLMPs at 12:00 for scenario 1 (Baseline).

hydraulic distance of nodes from the source node of the thermal grid. In the baseline scenario, the congestion and node head components take the value of zero, as the grid utilization does not reach branch flow or node head limits.

Figure11.7portrays the nodal values of active power DLMPs across the thermal grid at 12:00. The DLMP values are shown for the energy component in top left, for the loss component in the top right, for the voltage component in the bottom left and for the congestion component in the bottom right. In equivalence to the thermal grid and fig.11.6, the energy component takes the same value for all nodes, which corresponds to the active power price at the source node. The loss component increases proportionally to the distance from the source node of the electric grid. The congestion and voltage components take value of zero because the demand does not cause the electric grid reach any branch power or voltage limits.

##### 11.2.2 Constrained branch flow in the thermal grid

Figure11.8depicts the DLMPs and dispatch schedules for DER 22 in event of constrained branch flow in thermal grid. Recall that this scenario considers a tight branch flow limit across the pipe connecting nodes “A” and “B” as highlighted in fig.11.4. Therefore, the DLMP congestion component takes a value greater than zero for the time periods where the branch flow at “A-B” reaches the imposed limit. Note that the energy and pump components of the DLMP remain at the same values as in fig.11.5. The value of the congestion component reflects the additional costs incurred by flexible DERs to reshape their power dispatch in order

<u>11.2. Results</u>
Electric grid loss DLMP at 12:00

0.8
0.6
0.4 Price [S$/MWh]
0.2
0.0
Electric grid congestion DLMP at 12:00

1.0
0.8
0.6
0.4 Price [S$/MWh]
0.2
0.0
Figure 11.7: Electric grid DLMPs at 12:00 for scenario 1 (Baseline).

<u>11. Study of combined thermal and electric grid operation</u> Electric grid energy DLMP at 12:00
83.4
83.2
83.0
82.8 Price [S$/MWh]
82.6
Electric grid voltage DLMP at 12:00

1.0
0.8
0.6
0.4 Price [S$/MWh]
0.2
0.0
Thermal power DLMP and dispatch schedule at DER 22

15 10 5 ���������������� 0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00

Active power DLMP and dispatch schedule at DER 22

75 50 25 Price [S$/MWh] 0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00

##### flow in the thermal grid).

1.00 DLMP total
0.75
(Thrm. pw.) Congest.

0.50 Head
0.25
Pumping Power [p.u.] Energy

0.00 Thrm. pw.
00:00

1.00 DLMP total
0.75
(Active pw.) Congest.

0.50 Voltage
0.25 Power [p.u.]
Loss Energy

0.00 Active pw.
00:00

Figure 11.8: DLMPs and dispatch schedules at DER 22 for scenario 2 (Constrained branch

to respect the branch flow limit, e.g. the additional thermal losses incurred by pre-cooling the buildings. To this end, DER 22 exhibits a different load shape from fig.11.5.

<u>11. Study of combined thermal and electric grid operation 11.2. Results</u> Thermal grid energy DLMP at 12:00 Thermal grid pump DLMP at 12:00
17.2
0.190
17.0
16.8 0.185
16.6 0.180 ���������������� ����������������
16.4
0.175
Thermal grid head DLMP at 12:00 Thermal grid congestion DLMP at 12:00

1.0 1.25
0.8 1.00
0.6 0.75
0.4 0.50 ���������������� ����������������
0.2 0.25
0.0 0.00
Figure 11.9: Thermal grid DLMPs at 12:00 for scenario 2 (Constrained branch flow in the

thermal grid).

Figure11.9highlights the nodal values of the DLMP components in the thermal grid at 12:00 in scenario 2. In the bottom right, the congestion component is seen to take a value greater than zero only for the portion of the network which is directly affected by the tightened branch flow limit. The value is constant across all nodes in the affected area of the thermal grid. This is due to thermal power consumption at each node in this area contributing in the same proportion to further utilization at the constrained branch. The head component remains at the value of zero, whereas energy and pump components take the same values as in the baseline scenario in fig.11.6.

##### 11.2.3 Constrained node head in the thermal grid

This scenario considers a tightened node head limit at node “B” in the thermal grid, which is akin to deploying a low-rated distribution pump being at this node. As depicted in fig.11.10, this leads to the occurrence of positive values for the head component of the thermal power DLMP at DER 22 during the time period where the node head constraint is binding. The increase corresponds to the additional costs incurred by DERs to shift their demand to a different time period. Accordingly, the tightened constraint leads to a different dispatch schedule than in the baseline scenario in fig.11.5.

Figure11.11portrays the nodal DLMP values in the thermal grid for scenario 3. As in scenario 2, the values for the energy and pump components remain identical to the baseline

<u>11. Study of combined thermal and electric grid operation 11.2. Results</u>
Thermal power DLMP and dispatch schedule at DER 22

1.00 DLMP total
(Thrm. pw.) 15 0.75 Congest. 10 0.50 Head Pumping 5 0.25 Power [p.u.] Energy ����������������

0.00 Thrm. pw.
0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Active power DLMP and dispatch schedule at DER 22

1.00 DLMP total
75 (Active pw.)

0.75
Congest. 50 0.50 Voltage Loss 25 0.25 Power [p.u.] Price [S$/MWh] Energy

0.00 Active pw.
0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Figure 11.10: DLMPs and dispatch schedules at DER 22 for scenario 3 (Constrained node

head in the thermal grid).

|head in the thermal grid).|||
|---|---|---|
|Thermal grid energy DLMP at 12:00||Thermal grid pump DLMP at 12:00|
|Thermal grid head DLMP at 12:00||Thermal grid congestion DLMP at 12:00|

17.2
0.190
17.0
16.8 0.185
16.6 0.180 ���������������� ����������������
16.4
0.175
1.0
1.25
1.00 0.8
0.75 0.6
0.50 0.4 ���������������� ����������������
0.25 0.2
0.00 0.0
Figure 11.11: Thermal grid DLMPs at 12:00 for scenario 3 (Constrained node head in the

thermal grid).

<u>11.2. Results</u>
<u>11. Study of combined thermal and electric grid operation</u>
Thermal power DLMP and dispatch schedule at DER 22

15 10 5 ���������������� 0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00

Active power DLMP and dispatch schedule at DER 22

50 Price [S$/MWh] 0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00

##### power in the electric grid).

1.00 DLMP total
0.75
(Thrm. pw.) Congest.

0.50 Head
0.25 Power [p.u.]
Pumping Energy

0.00 Thrm. pw.
00:00

1.00 DLMP total
0.75
(Active pw.) Congest.

0.50 Voltage
Loss

0.25 Power [p.u.]
Energy

0.00 Active pw.
00:00

##### constraint is binding in this scenario.

##### 11.2.4 Constrained branch power in the electric grid

##### scheduling of the HVAC systems.

Figure 11.12: DLMPs and dispatch schedules at DER 22 for scenario 4 (Constrained branch

scenario in fig.11.6. At the same time, the head component takes a value greater than zero for affected portion of the network. Note that although the head limit is imposed at node “B”, the head component also increases at the portion of the thermal grid which is adjacent to node “B”. This is due to increased demand leading to an increased head drop at node “A”, which proportionally aggravates the head drop at node “B”. Notice that the node head component is constant across nodes that lie “adjacent” to node “B” as well as nodes that lie “behind” node “B”. The congestion component remains at zero value, as no branch flow

Figure11.12depicts the DLMPs and dispatch schedules for DER 22 in event of a tight branch power limit at branch “A-B” in the electric grid. Note that this is essentially equivalent to scenario 2 in the thermal grid. Therefore, the thermal power DLMPs remain identical to the baseline scenario, whereas the congestion component of the active power DLMPs take a value greater than zero for time steps with binding branch power limits. Note that DSF at the flexible buildings arises from the space cooling. To this end, the thermal power dispatch schedule is also affected by the congestion in the electric grid, due to the revised operation

Notice that the value of the congestion keeps increasing in proportion to the time period with binding branch flow constraints, which is unlike the results observed for the thermal grid in fig.11.5. This is due to the flexible buildings being able to consume thermal power from building-level cooling plants and thereby active power from the electric grid in place of thermal power. This imposes an upper bound for the thermal power DLMP values, as buildings will

<u>11. Study of combined thermal and electric grid operation 11.2. Results</u> Electric grid energy DLMP at 12:00 Electric grid loss DLMP at 12:00
83.4 0.8
83.2 0.6
83.0 0.4
82.8 Price [S$/MWh] 0.2
Price [S$/MWh]

82.6 0.0
Electric grid voltage DLMP at 12:00 Electric grid congestion DLMP at 12:00

1.0
12.5
0.8
10.0
0.6
7.5
0.4
5.0
Price [S$/MWh] Price [S$/MWh]

0.2 2.5
0.0 0.0
Figure 11.13: Electric grid DLMPs at 12:00 for scenario 4 (Constrained branch power in the

electric grid).

simply switch to active power consumption during high-price periods. However, in the face of congestion in the electric grid, the flexible buildings do not have any option for alternative active power supply. Therefore, the DLMP value keeps increasing.

Figure11.13highlights the electric grid DLMP component values at 12:00 for scenario 4. In this case, congestion component of the active power DLMP takes a value greater than zero at the nodes contributing to the congestion at branch “A-B”. The behavior is in fact directly equivalent to scenario 2 in thermal grid, thereby demonstrating the equivalence between branch flow dynamics in the thermal grid and branch power dynamics in the electric grid.

##### 11.2.5 Constrained node voltage in the electric grid

Scenario 5 considers a voltage limit at node “B” in the electric grid. This serves as a comparison for scenario 3 in the thermal grid. Figure11.14depicts the DLMP and power dispatch at DER in this scenario. Here, the voltage component takes a value greater than zero for the time periods where the voltage constraint is binding. Similar to scenario 4, the DLMP value keeps increasing to higher values as compared to scenario 3 in thermal grid because the flexible buildings are unable to switch to an alternative active power source.

Figure11.15portrays the nodal DLMP values across the electric grid for scenario 5. In this case, the observed results are equivalent to scenario 3 in the thermal grid, where the voltage

<u>11.2. Results</u>
<u>11. Study of combined thermal and electric grid operation</u>
Thermal power DLMP and dispatch schedule at DER 22

15 10 5 ���������������� 0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00

Active power DLMP and dispatch schedule at DER 22

50 Price [S$/MWh] 0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00

##### voltage in the electric grid).

Electric grid energy DLMP at 12:00

83.4
83.2
83.0
82.8 Price [S$/MWh]
82.6
Electric grid voltage DLMP at 12:00

12.5
10.0
7.5
5.0 Price [S$/MWh]
2.5
0.0
electric grid).

1.00 DLMP total
0.75
(Thrm. pw.) Congest.

0.50 Head
0.25 Power [p.u.]
Pumping Energy

0.00 Thrm. pw.
00:00

1.00 DLMP total
0.75
(Active pw.) Congest.

0.50 Voltage
0.25 Power [p.u.]
Loss Energy

0.00 Active pw.
00:00

0.8
0.6
0.4
0.2 Price [S$/MWh]
0.0
1.0
0.8
0.6
0.4 Price [S$/MWh]
0.2
0.0
Figure 11.14: DLMPs and dispatch schedules at DER 22 for scenario 5 (Constrained node

Electric grid loss DLMP at 12:00

Electric grid congestion DLMP at 12:00

Figure 11.15: Electric grid DLMPs at 12:00 for scenario 5 (Constrained node voltage in the

<u>11. Study of combined thermal and electric grid operation 11.2. Results</u>
Thermal power DLMP and dispatch schedule at DER 23

1.00 DLMP total
15 (Thrm. pw.)

0.75
Congest. 10 0.50 Head Pumping 5 0.25 Power [p.u.] Energy ����������������

0.00 Thrm. pw.
0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Active power DLMP and dispatch schedule at DER 23

1.00 DLMP total
75 (Active pw.)

0.75
Congest. 50 0.50 Voltage Loss 25 0.25 Power [p.u.] Price [S$/MWh] Energy

0.00 Active pw.
0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Figure 11.16: DLMPs and dispatch schedules at DER 23 for scenario 6 (High-cost cooling

plant in the thermal grid).

component takes a value for the portion of the electric grid which lies “behind” as well as “adjacent” to the affected node “B”. The remaining components stay equivalent to the baseline scenario.

##### 11.2.6 High-cost cooling plant in the thermal grid

In scenario 6, an additional cooling plant is introduced at node “C” as highlighted in fig.11.4. For this scenario, the secondary cooling plant is assumed to have a COP lower than the COP of the primary cooling plant at the source node. To this end, the secondary cooling plant is generally more expensive to operate and would not be dispatched under nominal conditions. Therefore, an additional branch flow constraint is introduced at branch “A-B” in the thermal grid in the same fashion as in scenario 2. Figure11.16depicts the DLMP and power dispatch schedule at the additional cooling plant, i.e. DER 23. As evident, the cooling plant is only dispatched during time periods with binding branch flow constraints, where the thermal power in the congested area of the thermal grid cannot be served by the primary cooling plant. To this end, the cooling plant is dispatched during periods where the value of the congestion component exceeds the additional cost incurred by operating the less efficient secondary cooling plant. Although not clearly visible in fig.11.4, this leads to slightly reduced thermal power DLMP values as compared to scenario 2.

##### 11.2.7 Low-cost cooling plant in the thermal grid

This scenario also considers an additional cooling plant being deployed at node “C” of the thermal grid. In this case, the COP of the secondary cooling plant is assumed to be greater than the COP of the primary cooling plant. To this end, the secondary cooling will always be

<u>11. Study of combined thermal and electric grid operation 11.2. Results</u>
Thermal power DLMP and dispatch schedule at DER 22

1.00 DLMP total
15 (Thrm. pw.)

0.75
Congest. 10 0.50 Head Pumping 5 0.25 Power [p.u.] Energy ����������������

0.00 Thrm. pw.
0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Active power DLMP and dispatch schedule at DER 22

1.00 DLMP total
75 (Active pw.)

0.75
Congest. 50 0.50 Voltage Loss 25 0.25 Power [p.u.] Price [S$/MWh] Energy

0.00 Active pw.
0 00:00 03:00 06:00 09:00 12:00 15:00 18:00 21:00 00:00

Figure 11.17: DLMPs and dispatch schedules at DER 22 for scenario 7 (Low-cost cooling

plant in the thermal grid).

deployed first to serve thermal power demand in thermal grid. Further, this scenario assumes the rated thermal power of the secondary cooling plant to be larger than the aggregated demand in the thermal grid. To this end, a reverse flow occurs at branch “A-B”. Since an additional branch flow constraint is introduced at branch “A-B” in thermal grid in the same fashion as in scenario 2, this leads to congestion as depicted in fig.11.17. Note that the value of the DLMP congestion component takes a negative value due to the reverse power flow being responsible for the for the congestion. In this case, the value of the congestion component corresponds to the lost revenue of secondary cooling plant.

Figure11.18highlights the nodal DLMP values in across the thermal grid for scenario 6. The congestion component takes a negative value in the affected portion of the thermal grid “behind” branch “A-B”. To this end, the behavior is inversely proportional to the constrained branch flow scenario in fig.11.9.

##### 11.2.8 Low-cost generator in the electric grid

This scenario considers that an additional electric generator in the form of a solar PV plant is deployed at node “C” in the electric grid, which is assumed to have sufficient generation capacity to serve all electric demand in the district. The marginal cost of the generator is set to 50 S$/MW/h. In this case, the generator will always be fully dispatched, since the marginal cost lies below the cost of electric power at the source node. At the same time, a tight electric branch power limit is imposed at branch “A-B” in the electric grid. Figure11.19highlights the resulting DLMP and dispatch schedule at DER 24, i.e. the solar PV plant. In similar fashion as in scenario 7, the congestion component takes a negative value due to the large reverse power flow across branch “A-B” causing congestion.

<u>11. Study of combined thermal and electric grid operation 11.2. Results</u> Thermal grid energy DLMP at 12:00 Thermal grid pump DLMP at 12:00
17.2
0.190
17.0
16.8 0.185
16.6 0.180 ���������������� ����������������
16.4
0.175
Thermal grid head DLMP at 12:00 Thermal grid congestion DLMP at 12:00

1.0 0.00
0.8 −0.25
−0.50

0.6
−0.75

0.4
−1.00 ���������������� ����������������

0.2
−1.25

0.0
Figure 11.18: Thermal grid DLMPs at 12:00 for scenario 7 (Low-cost cooling plant in the

thermal grid).

Active power DLMP and dispatch schedule at DER 24

1.00 DLMP total

|||1.00||DLMP total|
|---|---|---|---|---|
|75||0.75||(Active pw.) Congest.|
|50||0.50||Voltage|
|25||0.25|Power [p.u.]|Loss|
|Price [S$/MWh]||||Energy|
|0||0.00||Active pw.|
|00:00|03:00|00:00|||

06:00 09:00 12:00 15:00 18:00 21:00

Figure 11.19: DLMPs and dispatch schedules at DER 24 for scenario 8 (Low-cost generator

in the electric grid).

Notice that the total DLMP value falls approximately to the marginal cost of the generator. This is unlike in scenario 7 for the thermal grid, since the cooling plant does not have a distinct thermal power production cost, i.e. the production cost depends both on the COP as well as the price / DLMP value of active power at the corresponding node in the electric grid.

<u>11. Study of combined thermal and electric grid operation 11.3. Discussion</u> Electric grid energy DLMP at 12:00 Electric grid loss DLMP at 12:00
83.4 0.8
83.2 0.6
83.0 0.4
Price [S$/MWh]

82.8 Price [S$/MWh] 0.2
82.6 0.0
Electric grid voltage DLMP at 12:00 Electric grid congestion DLMP at 12:00

1.0 0
−5

0.8
−10

0.6
−15

0.4
−20 Price [S$/MWh] Price [S$/MWh]

0.2 −25
0.0 −30
Figure 11.20: Electric grid DLMPs at 12:00 for scenario 8 (Low-cost generator in the electric

grid).

#### 11.3 Discussion

The key purpose of the presented scenarios for combined thermal and electric grid operation is to serve as guidelines for the interpretation of DLMPs in both electric and thermal grids. Although DLMPs have been discussed extensively for the electric grid, the research works typically do not demonstrate a set of fundamental scenarios for the sake of brevity. While the above scenarios assume a centralized optimization by the district energy system operator, the results are also valid for a setup within a distributed optimization, where DER operators and grid operators are modeled as independent entities. Considering an district-scale grid operator which operates the combined thermal and electric grid and allocates prices for the electric and thermal consumption, an exemplary market procedure can be cast as follows:

1. DERs submit their instantaneous bids, energy requirements as well as their dispatch capabilities to the system operator;
2. The system operator forecasts its underlying electric / thermal power demand and solves the combined optimal operation problem in a day-ahead manner;
3. The system operator obtains the respective DLMPs for electric and thermal consump- tion and then passes them to the DERs;
182

<u>11. Study of combined thermal and electric grid operation 11.3. Discussion</u>
4. The DERs receive the price signals and solve the local DER operation problem. This results in an optimal dispatch which implicitly respects the operational constraints of the thermal and electric grids.
Note that such a market organization enables the individual market participants like DERs to make bids purely based on the locally available information. This essentially enables the price-based control for the system operator over DERs that act as price takers for both electric and thermal demand. In this case DLMP directly serve as incentive signals for the DERs for respecting the thermal and electric grid operation limits.

Another important takeaway from the presented scenarios is the apparent equivalence between thermal and electric grid DLMPs. As shown in scenarios 2 and 4, there is an equivalence between thermal branch flow congestion and electric current flow congestion, whereas scenarios 3 and 5 demonstrate the similarity between node head limitation in thermal grid and node voltage limitation in the electric grid. This is an important observation because it means that many operational and market organization methods which have been proposed for active electric distribution grids can be readily applied in the thermal grids.

## 12 Summary and conclusions

#### 12.1 Summary

This thesis has introduced the Multi-Energy System Modeling and Optimization (MESMO) framework as a software tool to facilitate the study of transactive energy frameworks for MESs. The key subjects of this work can be summarized as follows:

- Design of a software architecture for MESMO that caters to the relevant stakeholders, use cases and requirements, which were derived from formal software development principles. Preceding to this, the need for MESMO was identified based on a review of the state of the art in MES modeling as well as an assessment of the existing MES modeling and optimization software landscape.
- The development of convex models for all MES subsystems based on linear approxi- mate models, such that the optimal operation problem of the MES can be defined in a convex manner. An important contribution is the derivation of linear approximate models for the thermal grid, which were not readily available in existing MES modeling frameworks. Note that high-fidelity non-linear power flow models for electric grids and thermal grids were also defined, as these form the basis for linear approximate models and may be preferred for simulation-based studies, e.g. nominal operation problems. This was concluded by the development of formal definitions and solution algorithms for the nominal operation problem and the optimal operation problem.
- Study of the impact of EV charging on the electric distribution system in Singapore, based on a synthetic test case developed from publicly available data items. This included the comparison of different EV penetration scenarios as well as operational mitigation strategies for EV charging. To this end, the study defined a combination of nominal operation problems and optimal operation problems through MESMO.
- Study of DLMPs in the context of a combined optimal operation of district-scale electric and thermal grids, based on a synthetic test case for Tanjong Pagar, Singapore. The focus was on examining and interpreting the behavior of DLMPs in comparison to different operational scenarios, i.e. different operational becoming binding in the MES. This utilized the capability of MESMO to define, solve and obtain DLMP values for optimal operation problems.
184

<u>12. Summary and conclusions 12.2. Conclusions</u>
#### 12.2 Conclusions

To conclude this thesis, the following presents an overview of the main conclusions from the presented studies and an outlook for the future development of MESMO.

##### Study of EV charging in Singapore

In the first study of this thesis, the impact of electric vehicle charging was evaluated for a synthetic test case based in Singapore. Note that this study was based on synthetic model parameters and the results may not adequately present the reality. The key takeaways from the results can be summarized as follows:

- Based on the synthetic test case, EV charging, if deployed primarily at public car parks, primarily affects the utilization of substations in a locally limited fashion. This means that a limited number of substations are certain to require upgrades, particularly for higher EV penetration rates. At the same time, the utilization of grid lines and the nodal voltage drop are only marginally affected. Note, however, that this result assumes a significant spare capacity in the electric grid lines.
- Smart charging only marginally contributes to a reduction in utilization at the most affected substations. Therefore, mitigation of transformer upgrades is only reasonable for low EV penetration rates.
- Price-based charging can lead to significant over-utilization of the grid infrastructure if high participation of consumers in this scheme is assumed. This points to the importance of controlling the charging demand through incentive signals to augment the electric energy price. This result point to the need for incentive frameworks, e.g. transactive energy frameworks, for EV charging to mitigate grid upgrades.
##### Study of combined thermal and electric grid operation

The second study of this thesis focuses on the deployment of distribution locational marginal prices (DLMPs) for combined thermal and electric grids. The key outcomes of this study can are summarized as follows:

- The DLMP formulation derived for thermal grids in this thesis is demonstrated to translate operational constraints into incentive signals appropriately. Furthermore, through the branch flow congestion, branch power congestion, node head limit and node voltage limit scenarios, an equivalence is demonstrated to the behavior of DLMPs in the electric grid. These results are not surprising but represent a valuable guideline for the interpretation of DLMPs in MES.
- Although not included in this thesis, DLMPs are shown to serve as important funda- mental for designing district-scale market frameworks in [41], where an ADMM-based market-clearing of the same test case was shown to effectively converge towards the DLMP values obtained from the solution of the centralized problem.
185

<u>12. Summary and conclusions 12.2. Conclusions</u>
- An important lesson from this thesis’ work is the observation that operational issues in thermal grids can be treated with the same fundamental techniques as electric grids. This demonstrates the possibility of re-applying other market-based techniques from the electric energy sector to the thermal energy sectors or other commodity networks in MESs.
##### Outlook for MESMO

Beyond the work presented in this thesis, the development of MESMO is intended to con- tinue under a collaborative framework between TUMCREATE, the Chair of Renewable and Sustainable Energy Systems (ENS) at the Technical University of Munich and the Institute of High Performance Computing (IHPC) at the Agency for Science, Technology and Re- search (A*STAR). To this end, the following summarizes vital features that represent practical extensions for MESMO but have not yet been addressed in the current implementation:

- Implementation of a trust-region-algorithm-based update for the linear approximate models. The optimal operation problem is currently implemented such that a single linearization point is utilized for the linear approximate models for the thermal grid and the electric grid. However, this may incur a significant linearization error when DER dispatch schedules are far from the linearization reference point. Consequently, the trust-region algorithm can be utilized for an iterative update of the linear approximation based on the optimization results, which has been presented for electric grids in [34, Algorithm 1].
- Definition of a market-clearing problem in an integrated fashion. Currently, market- clearing problems can be defined with MESMO only in an external fashion, i.e. a custom setup is required for the market-clearing algorithm. For example, this is utilized in [41] for the market-clearing of a combined thermal and electric energy market, through ADMM as a market-clearing algorithm. To this end, a fully implemented market-clearing problem in MESMO would ease the implementation effort for such studies.
- The implementation of optimal planning problems in MESMO. At present, planning- scale problems are only indirectly supported through nominal operation problems. For example, the results from the study on EV charging in chapter10can hypothetically serve to inform investment decisions. However, for future versions of MESMO it is desirable to directly address optimization-based planning problems, such as the work presented by the author in [52]. This would make MESMO a more holistic tool for MES optimization.
186

## Bibliography

[1] CIGRÉ Conseil international des grands réseaux électriques and Comité d’études C6, *Planning and Optimization Methods for Active Distribution Systems*. Paris: CIGRÉ, 2014, ISBN: 978-2-85873-289-0.

[2] IEC International Electrotechnical Commission, *IEC 61850-7-420 - Communication* *networks and systems for power utility automation-Part 7-420: Basic communication* *structure-Distributed energy resources and distribution automation logical nodes*,

2019.
[3]A. Bernstein, L. Reyes-Chamorro, J.-Y. Le Boudec, and M. Paolone, “A composable method for real-time control of active distribution networks with explicit power setpoints. Part I: Framework,” *Electric Power Systems Research*, vol. 125, pp. 254–264, 2015. DOI:10.1016/J.EPSR.2015.03.023.

[4] F. Bünning, M. Wetter, M. Fuchs, and D. Müller, “Bidirectional low temperature district energy systems with agent-based control: Performance comparison and operation optimization,” *Applied Energy*, vol. 209, pp. 502–515, Jan. 2018, ISSN: 03062619. DOI:

10.1016/j.apenergy.2017.10.072.
[5] S. Buffa, M. Cozzini, M. D’Antoni, M. Baratieri, and R. Fedrizzi, “5th generation district heating and cooling systems: A review of existing cases in Europe,” *Renewable and* *Sustainable Energy Reviews*, vol. 104, pp. 504–522, Apr. 2019, ISSN: 13640321. DOI:

10.1016/j.rser.2018.12.059.
[6] F. Tahersima, P. P. Madsen, and P. Andersen, “An intuitive definition of demand flexi- bility in direct load control,” in *IEEE International Conference on Control Applications*, IEEE, 2013, pp. 521–526, ISBN: 978-1-4799-1559-0. DOI:10.1109/CCA.2013.666280

2.
[7] A. Dubey, A. Bose, M. Liu, and L. N. Ochoa, “Paving the Way for Advanced Distribution Management Systems Applications: Making the Most of Models and Data,” *IEEE* *Power and Energy Magazine*, vol. 18, no. 1, pp. 63–75, Jan. 2020, ISSN: 1540-7977, 1558-4216. DOI:10/ggrnsb.

[8] M. Vadari, “The Future of Distribution Operations and Planning: The Electric Utility Environment Is Changing,” *IEEE Power and Energy Magazine*, vol. 18, no. 1, pp. 18– 25, Jan. 2020, ISSN: 1540-7977, 1558-4216. DOI:10/gmcprr.

<u>Bibliography</u>

[9] K. Kok and S. Widergren, “A Society of Devices: Integrating Intelligent Distributed Resources with Transactive Energy,” *IEEE Power and Energy Magazine*, vol. 14, no. 3, May 2016, ISSN: 1540-7977. DOI:10.1109/MPE.2016.2524962.

[10] A. Adeyemi, M. Yan, M. Shahidehpour, S. Bahramirad, and A. Paaso, “Transactive energy markets for managing energy exchanges in power distribution systems,” *The* *Electricity Journal*, vol. 33, no. 9, p. 106 868, Nov. 2020, ISSN: 10406190. DOI:10.101 6/j.tej.2020.106868.

[11] S. Hanif, “Distribution Locational Marginal Price: Approximations, Solution Algorithm and Organization,” 2018. [Online]. Available:[http://mediatum.ub.tum.de/?id=1445693](http://mediatum.ub.tum.de/?id=1445693) (visited on Mar. 16, 2021).

[12] F. Rahimi, A. Ipakchi, and F. Fletcher, “The Changing Electrical Landscape: End-to- End Power System Operation Under the Transactive Energy Paradigm,” *IEEE Power* *and Energy Magazine*, vol. 14, no. 3, May 2016, ISSN: 1540-7977, 1558-4216. DOI:

10.1109/MPE.2016.2524966.
[13] K. Zhang, S. Troitzsch, S. Hanif, and T. Hamacher, “Coordinated Market Design for Peer-to-Peer Energy Trade and Ancillary Services in Distribution Grids,” *IEEE* *Transactions on Smart Grid*, 2020. DOI:10.1109/TSG.2020.2966216.

[14] S. Troitzsch, M. Grussmann, K. Zhang, and T. Hamacher, “Distribution Locational Marginal Pricing for Combined Thermal and Electric Grid Operation,” in *IEEE PES* *Innovative Smart Grid Technologies Conference Europe*, Oct. 2020. DOI:10.1109 /ISGT-Europe47291.2020.9248832.

[15] J. A. Taylor, *Convex Optimization of Power Systems.* West Nyack: Cambridge Univer- sity Press, 2015, ISBN: 978-1-139-92467-2. [Online]. Available:[https://doi.org/10.101](https://doi.org/10.101) 7/CBO9781139924672(visited on Jun. 23, 2021).

[16] J. Lofberg, “YALMIP: A toolbox for modeling and optimization in MATLAB,” in *IEEE* *International Conference on Robotics and Automation*, IEEE, 2004, pp. 284–289, ISBN: 0-7803-8636-1. DOI:10.1109/CACSD.2004.1393890.

[17] W. E. Hart, C. D. Laird, J.-P. Watson, *et al.*, *Pyomo-Optimization Modeling in Python*. Springer, 2017, ISBN: 978-3-319-58819-3. DOI:10.1007/978-3-319-58821-6.

[18] S. Diamond and S. Boyd. “CVXPY: A Python-Embedded Modeling Language for Convex Optimization.” arXiv:1603.00943 [math]. (Jun. 1, 2016), [Online]. Available: [http://arxiv.org/abs/1603.00943(visited](http://arxiv.org/abs/1603.00943(visited) on Mar. 21, 2021).

[19] I. Dunning, J. Huchette, and M. Lubin, “JuMP: A Modeling Language for Mathematical Optimization,” *Society for Industrial and Applied Mathematics*, vol. 59, no. 2, pp. 295– 320, 2017. DOI:10.1137/15M1020575.

[20] R. C. Dugan and T. E. McDermott, “An open source platform for collaborating on smart grid research,” in *2011 IEEE Power and Energy Society General Meeting*, San Diego, CA: IEEE, Jul. 2011, pp. 1–7. DOI:10.1109/PES.2011.6039829.

[21] DIgSILENT. “PowerFactory.” (2021), [Online]. Available:[https://www.digsilent.de/en/p](https://www.digsilent.de/en/p) owerfactory.html(visited on Mar. 19, 2021).

<u>Bibliography</u>

[22]R. D. Zimmerman, C. E. Murillo-Sanchez, and R. J. Thomas, “MATPOWER: Steady- State Operations, Planning, and Analysis Tools for Power Systems Research and Education,” *IEEE Transactions on Power Systems*, vol. 26, no. 1, pp. 12–19, Feb. 2011, ISSN: 0885-8950, 1558-0679. DOI:10.1109/TPWRS.2010.2051168.

[23] HOMER Energy. “HOMER-Hybrid Renewable and Distributed Generation System Design Software.” (2021), [Online]. Available:[https://www.homerenergy.com/(visited](https://www.homerenergy.com/(visited) on Mar. 25, 2021).

[24] S. Pfenninger and B. Pickering, “Calliope: A multi-scale energy systems modelling framework,” *Journal of Open Source Software*, vol. 3, no. 29, p. 825, Sep. 12, 2018, ISSN: 2475-9066. DOI:10.21105/joss.00825.

[25] J. Dorfner, K. Schönleber, M. Dorfner, *et al.*, *Urbs*, version 1.0.1, Zenodo, Jul. 2, 2019. DOI:10.5281/ZENODO.3265960.

[26] J. A. Fonseca, A. Schlueter, T.-A. Nguyen, and F. Marechal, “City Energy Analyst (CEA): Integrated framework for analysis and optimization of building energy systems in neighborhoods and city districts,” *Energy and Buildings*, vol. 113, pp. 202–226,

2016. DOI:10.1016/J.ENBUILD.2015.11.055.
[27] C. Coffrin, R. Bent, K. Sundar, Y. Ng, and M. Lubin, “PowerModels.jl: An Open-

Source Framework for Exploring Power Flow Formulations,” in *2018 Power Systems*

*Computation Conference (PSCC)*, Dublin, Ireland: IEEE, Jun. 2018, pp. 1–8, ISBN: 978-1-910963-10-4. DOI:10.23919/PSCC.2018.8442948.

[28] D. P. Chassin, K. Schneider, and C. Gerkensmeyer, “GridLAB-D: An open-source power systems modeling and simulation environment,” in *IEEE PES Transmission* *and Distribution Conference and Exposition*, 2008, ISBN: 978-1-4244-1903-6. DOI:

10.1109/TDC.2008.4517260.
[29] T. Morstyn, K. A. Collett, A. Vijay, *et al.*, “OPEN: An open-source platform for develop- ing smart local energy system applications,” *Applied Energy*, vol. 275, p. 115 397, Oct. 2020, ISSN: 03062619. DOI:10.1016/j.apenergy.2020.115397.

[30] S. Troitzsch, S. Hanif, K. Zhang, A. Trpovski, and T. Hamacher, “Flexible Distribution Grid Demonstrator (FLEDGE): Requirements and Software Architecture,” in *IEEE* *Power & Energy Society General Meeting (PESGM)*, Atlanta, GA, USA: IEEE, Aug. 2019, ISBN: 978-1-72811-981-6. DOI:10.1109/PESGM40551.2019.8973567.

[31] W. H. Kersting, *Distribution System Modeling and Analysis*, Fourth edition. Boca Raton: CRC Press, Taylor & Francis Group, 2018, 526 pp., ISBN: 978-1-4987-7213-6. [Online]. Available:[https://doi.org/10.1201/9781315120782](https://doi.org/10.1201/9781315120782).

[32] M. Bazrafshan and N. Gatsis, “Comprehensive modeling of three-phase distribution systems via the bus admittance matrix,” *IEEE Transactions on Power Systems*, vol. 33, no. 2, pp. 2015–2029, 2018. DOI:10.1109/TPWRS.2017.2728618.

<u>Bibliography</u>

[33] A. Bernstein, C. Wang, E. Dall’Anese, J.-Y. Le Boudec, and C. Zhao, “Load Flow in Multiphase Distribution Networks: Existence, Uniqueness, Non-Singularity and Linear Models,” *IEEE Transactions on Power Systems*, vol. 33, no. 6, pp. 5832–5843, Nov. 2018, ISSN: 0885-8950, 1558-0679. DOI:10.1109/TPWRS.2018.2823277.

[34] S. Hanif, K. Zhang, C. Hackl, M. Barati, H. B. Gooi, and T. Hamacher, “Decomposition and Equilibrium Achieving Distribution Locational Marginal Prices using Trust-Region Method,” *IEEE Transactions on Smart Grid*, 2018. DOI:10.1109/TSG.2018.2822766.

[35] Haestad Methods, *Advanced Water Distribution Modeling and Management*. Haestead Press, 2003, ISBN: 978-0-9714141-2-9.

[36] H. Song, *Engineering Fluid Mechanics*. Singapore: Springer Singapore, 2018, ISBN: 978-981-13-0173-5. DOI:10.1007/978-981-13-0173-5.

[37] ASHRAE American Society of Heating Refrigerating and Air-Conditioning Engineers, Ed., *District Cooling Guide*. Atlanta, GA: ASHRAE, 2013, ISBN: 978-1-936504-42-8. [Online]. Available:[https://app.knovel.com/hotlink/toc/id:kpDCG00004/district-cooling-](https://app.knovel.com/hotlink/toc/id:kpDCG00004/district-cooling-) guide/district-cooling-guide(visited on Jun. 27, 2021).

[38] ASHRAE American Society of Heating Refrigerating and Air-Conditioning Engineers, Ed., *District Heating Guide*. Atlanta, GA: ASHRAE, 2013, ISBN: 978-1-936504-43-5. [Online]. Available:[https://app.knovel.com/hotlink/toc/id:kpDHG00003/district-heating](https://app.knovel.com/hotlink/toc/id:kpDHG00003/district-heating) -guide/district-heating-guide(visited on Jun. 27, 2021).

[39] M. Grussmann, “Optimal dispatch of electric loads in flexible district cooling systems,”

2019.
[40] S. Spitzer, “Optimal planning of urban multi-energy systems with demand side flexible operation for a test case in Singapore,” 2020.

[41] S. Troitzsch, K. Zhang, T. Massier, and T. Hamacher, “Coordinated Market Clearing for Combined Thermal and Electric Distribution Grid Operation,” presented at the IEEE Power & Energy Society General Meeting (PESGM), Aug. 2021. DOI:10.36227 /techrxiv.13247246.

[42] F. Oldewurtel, “Stochastic model predictive control for energy efficient building climate control,” PhD Thesis, ETH Eidgenössische Technische Hochschule Zürich, 2011. DOI:

10.3929/ethz-a-007157625.
[43] D. C. T. Sturzenegger, “Model predictive building climate control-Steps towards practice,” PhD Thesis, ETH Zürich, 2014. DOI:10.3929/ETHZ-A-010379191.

[44] S. Troitzsch, “Model Predictive Control for Co-Optimization of Distribution Grid Con- gestion and Thermal Comfort in Office Buildings,” RWTH Aachen University, 2016.

[45] S. Troitzsch, T. Miori, and A. Vautrin, *CoBMo-Control-oriented Building Model*, version 0.3.0, Zenodo, Nov. 13, 2019. DOI:10.5281/ZENODO.3523539.

[46] A. Vautrin, S. Troitzsch, S. Ramachandran, and T. Hamacher, “Demand Controlled Ventilation for Electric Demand Side Flexibility,” in *Building Simulation Conference*, Sep. 2019. DOI:10.26868/25222708.2019.210968.

<u>Bibliography</u>

[47] T. Miori, “Optimization of integrated energy storage for implicit demand side flexibility,”

2019.
[48] Sherif Hashem, “Convex thermal modelling of hydronic radiators for model predictive control of HVAC systems to enable demand side flexibility,” 2019.

[49] C. Utama, “Demand Side Flexibility and Bidding Strategies for Flexible Loads in Air-Conditioned Buildings,” 2020.

[50] A. Trpovski, D. Recalde, and T. Hamacher, “Synthetic Distribution Grid Generation Using Power System Planning: Case Study of Singapore,” in *UPEC International* *Universities Power Engineering Conference*, 2018, ISBN: 978-1-5386-2910-9. DOI:

10.1109/UPEC.2018.8542054.
[51] A. Trpovski, “Synthetic Grid Generation Using Power System Planning-Case Study of the Power System in Singapore,” 2021.

[52] S. Troitzsch, B. K. Sreepathi, T. P. Huynh, *et al.*, “Optimal electric-distribution-grid planning considering the demand-side flexibility of thermal building systems for a test case in Singapore,” *Applied Energy*, vol. 273, p. 114 917, Sep. 2020, ISSN: 03062619. DOI:10.1016/j.apenergy.2020.114917.

[53] EMA Energy Market Authority, *Transmission Code*, 2014. [Online]. Available:https: //www.ema.gov.sg/cmsmedia/About-Us/transmission%20code.pdf(visited on Jun. 21,

2021).
[54] EMA Energy Market Authority, “Introduction to the National Electricity Market of Singapore,” 2010. [Online]. Available:[https://www.ema.gov.sg/cmsmedia/Handbook](https://www.ema.gov.sg/cmsmedia/Handbook) /NEMS_111010.pdf(visited on Jun. 21, 2020).

[55] K. Zhang, “Spot Pricing Principles in Distribution Grids: From Local Market Organiza- tion to Multi-regional Coordination,” 2020.

[56] S. Huang, Q. Wu, S. S. Oren, R. Li, and Z. Liu, “Distribution Locational Marginal Pricing Through Quadratic Programming for Congestion Management in Distribution Networks,” *IEEE Transactions on Power Systems*, vol. 30, no. 4, pp. 2170–2178, Jul. 2015, ISSN: 0885-8950, 1558-0679. DOI:10.1109/TPWRS.2014.2359977.

[57] S. Frank, I. Steponavice, and S. Rebennack, “Optimal power flow: A bibliographic survey I,” *Energy Systems*, vol. 3, no. 3, pp. 221–258, 2012. DOI:10.1007/s12667-01 2-0056-y.

[58] S. H. Low, “Convex relaxation of optimal power flow-Part I: Formulations and equivalence,” *IEEE Transactions on Control of Network Systems*, vol. 1, no. 1, pp. 15– 27, 2014. DOI:10.1109/TCNS.2014.2309732.

[59]Siemens. “PSS®SINCAL,” siemens.com Global Website. (2021), [Online]. Available: [https://new.siemens.com/global/en/products/energy/energy-automation-and-smart-](https://new.siemens.com/global/en/products/energy/energy-automation-and-smart-) grid/pss-software/pss-sincal.html(visited on Mar. 19, 2021).

<u>Bibliography</u>

[60] E. E. Pompodakis, G. C. Kryonidis, and M. C. Alexiadis, “A Comprehensive Load Flow Approach for Grid-Connected and Islanded AC Microgrids,” *IEEE Transactions* *on Power Systems*, vol. 35, no. 2, pp. 1143–1155, Mar. 2020, ISSN: 0885-8950, 1558-0679. DOI:10.1109/TPWRS.2019.2945011.

[61] M. Bazrafshan and N. Gatsis, “Convergence of the Z-Bus Method for Three-Phase Distribution Load-Flow with ZIP Loads,” *IEEE Transactions on Power Systems*, vol. 33, no. 1, pp. 153–165, Jan. 2018, ISSN: 0885-8950, 1558-0679. DOI:10.1109/TPWRS.2

017.2703835.
[62] S. Bolognani and S. Zampieri, “On the Existence and Linear Approximation of the Power Flow Solution in Power Distribution Networks,” *IEEE Transactions on Power* *Systems*, vol. 31, no. 1, pp. 163–172, Jan. 2016, ISSN: 0885-8950, 1558-0679. DOI:

10.1109/TPWRS.2015.2395452.
[63] C. Wang, A. Bernstein, J.-Y. Le Boudec, and M. Paolone, “Explicit Conditions on Existence and Uniqueness of Load-Flow Solutions in Distribution Networks,” *IEEE* *Transactions on Smart Grid*, vol. 9, no. 2, pp. 953–962, Mar. 2018, ISSN: 1949-3053, 1949-3061. DOI:10.1109/TSG.2016.2572060.

[64] S. Yu, H. D. Nguyen, and K. S. Turitsyn, “Simple certificate of solvability of power flow equations for distribution systems,” in *IEEE PES General Meeting*, Denver, CO, USA: IEEE, Jul. 2015, ISBN: 978-1-4673-8040-9. DOI:10.1109/PESGM.2015.7286371.

[65] M. Farivar and S. H. Low, “Branch flow model: Relaxations and convexification-Part I,” *IEEE Transactions on Power Systems*, vol. 28, no. 3, pp. 2554–2564, 2013. DOI:

10.1109/TPWRS.2013.2255317.
[66] S. H. Low, “Convex relaxation of optimal power flow-Part II: Exactness,” *IEEE* *Transactions on Control of Network Systems*, vol. 1, no. 2, pp. 177–189, 2014. DOI:

10.1109/TCNS.2014.2323634.
[67] B. Stott, J. Jardim, and O. Alsac, “DC Power Flow Revisited,” *IEEE Transactions* *on Power Systems*, vol. 24, no. 3, pp. 1290–1300, Aug. 2009, ISSN: 0885-8950, 1558-0679. DOI:10.1109/TPWRS.2009.2021235.

[68] K. Purchala, L. Meeus, D. Van Dommelen, and R. Belmans, “Usefulness of DC power flow for active power flow analysis,” in *IEEE Power Engineering Society General* *Meeting, 2005*, San Francisco, CA, USA: IEEE, 2005, pp. 2457–2462, ISBN: 978-0- 7803-9157-4. DOI:10.1109/PES.2005.1489581.

[69] F. Li and R. Bo, “DCOPF-Based LMP Simulation: Algorithm, Comparison With ACOPF, and Sensitivity,” *IEEE Transactions on Power Systems*, vol. 22, no. 4, pp. 1475–1485, Nov. 2007, ISSN: 0885-8950. DOI:10.1109/TPWRS.2007.907924.

[70] S. Bolognani and F. Dorfler, “Fast power system analysis via implicit linearization of the power flow manifold,” in *Allerton Conference on Communication, Control, and* *Computing*, Monticello, IL: IEEE, Sep. 2015, pp. 402–409, ISBN: 978-1-5090-1824-6. DOI:10.1109/ALLERTON.2015.7447032.

<u>Bibliography</u>

[71] K. Christakou, J.-Y. LeBoudec, M. Paolone, and D.-C. Tomozei, “Efficient Computation of Sensitivity Coefficients of Node Voltages and Line Currents in Unbalanced Radial Electrical Distribution Networks,” *IEEE Transactions on Smart Grid*, vol. 4, no. 2, pp. 741–750, Jun. 2013, ISSN: 1949-3053, 1949-3061. DOI:10.1109/TSG.2012.2221

751.
[72] T. Licklederer, T. Hamacher, M. Kramer, and V. S. Peric, “Thermohydraulic model ´ of Smart Thermal Grids with bidirectional power flow between prosumers,” *Energy*, vol. 230, p. 120 825, Sep. 2021, ISSN: 03605442. DOI:10.1016/j.energy.2021.120825.

[73] H. Lund, S. Werner, R. Wiltshire, *et al.*, “4th Generation District Heating (4GDH),” *Energy*, vol. 68, pp. 1–11, Apr. 2014, ISSN: 03605442. DOI:10.1016/j.energy.2014.02

.089.
[74] M. Ancona, L. Branchini, A. De Pascale, and F. Melino, “Smart District Heating: Distributed Generation Systems’ Effects on the Network,” *Energy Procedia*, vol. 75, pp. 1208–1213, Aug. 2015, ISSN: 18766102. DOI:10.1016/j.egypro.2015.07.157.

[75] R. Zarin Pass, M. Wetter, and M. Piette, “A thermodynamic analysis of a novel bidirectional district heating and cooling network,” *Energy*, vol. 144, pp. 20–30, Feb. 2018, ISSN: 03605442. DOI:10.1016/j.energy.2017.11.122.

[76] M. Wirtz, L. Kivilip, P. Remmen, and D. Müller, “5th Generation District Heating: A novel design approach based on mathematical optimization,” *Applied Energy*, vol. 260,

p. 114 158, Feb. 2020, ISSN: 03062619. DOI:10.1016/j.apenergy.2019.114158.
[77] T. Blacha, M. Mans, P. Remmen, and D. Müller, “Dynamic Simulation Of Bidirectional Low-Temperature Networks-A Case Study To Facilitate The Integration Of Renewable Energies,” presented at the Building Simulation, Rome, Italy, 2019, pp. 3491–3498. DOI:10.26868/25222708.2019.210670.

[78] C. Utama, S. Troitzsch, and J. Thakur, “Demand-side flexibility and demand-side bid- ding for flexible loads in air-conditioned buildings,” *Applied Energy*, vol. 285, p. 116 418, Mar. 2021, ISSN: 03062619. DOI:10.1016/j.apenergy.2020.116418.

[79] C. Dötsch, J. Taschenberger, and I. Schönberg, *Leitfaden Nahwärme*, ser. UMSICHT- Schriftenreihe 6. Stuttgart: Fraunhofer-IRB-Verl, 1998, ISBN: 978-3-8167-5186-1.

[80] H. Lund, P. A. Østergaard, D. Connolly, and B. V. Mathiesen, “Smart energy and smart energy systems,” *Energy*, vol. 137, pp. 556–565, Oct. 2017, ISSN: 03605442. DOI:10.1016/j.energy.2017.05.123.

[81] IEA International Energy Agency, *The Future of Cooling-Opportunities for energy-* *efficient air conditioning*, 2018. [Online]. Available:[https://www.iea.org/reports/the-fut](https://www.iea.org/reports/the-fut) ure-of-cooling(visited on Jun. 27, 2021).

[82] T. Sommer, M. Sulzer, M. Wetter, A. Sotnikov, S. Mennel, and C. Stettler, “The reservoir network: A new network topology for district heating and cooling,” *Energy*, vol. 199, p. 117 418, May 2020, ISSN: 03605442. DOI:10.1016/j.energy.2020.117418.

<u>Bibliography</u>

[83] SP Group, *Supply Conditions for District Cooling Service*. [Online]. Available:http s://www.spgroup.com.sg/wcm/connect/spgrp/c92a842f- 868b- 4547- a6e6- 0c2 9394bd7dc/%5BInfo%5D+Supply+Conditions+for+District+Cooling+Service.pdf ?MOD=AJPERES(visited on Jun. 27, 2021).

[84] E. Todini and L. A. Rossman, “Unified Framework for Deriving Simultaneous Equation Algorithms for Water Distribution Networks,” *Journal of Hydraulic Engineering*, vol. 139, no. 5, pp. 511–526, May 2013, ISSN: 0733-9429, 1943-7900. DOI:10.1061/(ASCE)H

Y.1943-7900.0000703.
[85] ISO International Organization for Standardization, *ISO 15118-1 - Road vehicles -* *Vehicle to grid communication interface-Part 1: General information and use-case* *definition*, 2019.

[86] IEEE Institute of Electrical and Electronics Engineers, *IEEE Std 1547-2018: IEEE* *Standard for Interconnection and Interoperability of Distributed Energy Resources* *with Associated Electric Power Systems Interfaces*, 2018. DOI:10.1109/IEEESTD.20

18.8332112.
[87] IEC International Electrotechnical Commission. “IEC 60050 - International Electrotech- nical Vocabulary.” (2021), [Online]. Available:[https://www.electropedia.org/(visited](https://www.electropedia.org/(visited) on Jun. 15, 2021).

[88] C. Greer, D. A. Wollman, D. E. Prochaska, *et al.*, “NIST Framework and Roadmap for Smart Grid Interoperability Standards, Release 3.0,” National Institute of Standards and Technology, NIST SP 1108r3, Oct. 2014, NIST SP 1108r3. DOI:10.6028/NIST.S

P.1108r3.
[89] M. F. Akorede, H. Hizam, and E. Pouresmaeil, “Distributed energy resources and benefits to the environment,” *Renewable and Sustainable Energy Reviews*, vol. 14, no. 2, pp. 724–734, Feb. 2010, ISSN: 13640321. DOI:10.1016/j.rser.2009.10.025.

[90] P. Palensky and D. Dietrich, “Demand side management: Demand response, intelligent energy systems, and smart loads,” *IEEE Transactions on Industrial Informatics*, vol. 7, no. 3, pp. 381–388, 2011. DOI:10.1109/TII.2011.2158841.

[91] T. Reindl. “Update of the Solar Photovoltaic (PV) Roadmap for Singapore.” (2020), [Online]. Available:[http://www.seris.sg/doc/publications/Update-of-the-Solar-Roadm](http://www.seris.sg/doc/publications/Update-of-the-Solar-Roadm) ap-for-Singapore-(March-2020).pdf(visited on Jul. 24, 2020).

[92] EMA Energy Market Authority, *Singapore Electricity Market Outlook*, 2020. [Online]. Available:[https://www.ema.gov.sg/cmsmedia/PPD/Singapore-Electricity-Market-Ou](https://www.ema.gov.sg/cmsmedia/PPD/Singapore-Electricity-Market-Ou) tlook-2020.pdf(visited on Jul. 2, 2021).

[93] P. D. Lund, J. Lindgren, J. Mikkola, and J. Salpakari, “Review of energy system flexibility measures to enable high levels of variable renewable electricity,” *Renewable* *and Sustainable Energy Reviews*, vol. 45, pp. 785–807, 2015. DOI:10.1016/j.rser.201

5.01.057.
194

<u>Bibliography</u>

[94] D. S. Callaway and I. A. Hiskens, “Achieving controllability of electric loads,” *Proceed-* *ings of the IEEE*, vol. 99, no. 1, pp. 184–199, 2011. DOI:10.1109/JPROC.2010.2081

652.
[95] C. Goldman, N. Hopper, R. Bharvirkar, B. Neenan, and P. Cappers, *Estimating De-* *mand Response Market Potential Among Large Commercial and Industrial Customers:* *A Scoping Study*, 2007. [Online]. Available:[https://escholarship.org/uc/item/87z9q754](https://escholarship.org/uc/item/87z9q754) (visited on Jul. 3, 2021).

[96] MOT Ministry of Transport. “Speech by Minister for Transport Mr Ong Ye Kung at the Committee of Supply Debate 2021 on Singapore Green Plan 2030.” (2021), [Online]. Available:[http://www.mot.gov.sg/news-centre/news/Detail/speech-by-minister-for-tr](http://www.mot.gov.sg/news-centre/news/Detail/speech-by-minister-for-tr) ansport-mr-ong-ye-kung-at-the-committee-of-supply-debate-2021-on-singapore-g reen-plan-2030/(visited on Jul. 3, 2021).

[97] Aoxia Chen and P. K. Sen, “Advancement in battery technology: A state-of-the-art review,” in *2016 IEEE Industry Applications Society Annual Meeting*, Portland, OR, USA: IEEE, Oct. 2016, pp. 1–10, ISBN: 978-1-4799-8397-1. DOI:10.1109/IAS.2016.7 731812.

[98] A. J. Crawford, D. Wu, V. V. Viswanathan, *et al.*, “Washington Clean Energy Fund: Energy Storage System Consolidated Performance Test Results,” PNNL-29378, 1602252, Feb. 17, 2020, PNNL–29 378, 1 602 252. DOI:10.2172/1602252.

[99] E. Namor, F. Sossan, R. Cherkaoui, and M. Paolone, “Control of Battery Storage Systems for the Simultaneous Provision of Multiple Services,” *IEEE Transactions on* *Smart Grid*, vol. 10, no. 3, pp. 2799–2808, May 2019, ISSN: 1949-3053, 1949-3061. DOI:10.1109/TSG.2018.2810781.

[100] H. Hao, D. Wu, J. Lian, and T. Yang, “Optimal Coordination of Building Loads and Energy Storage for Power Grid and End User Services,” *IEEE Transactions on Smart* *Grid*, vol. 9, no. 5, pp. 4335–4345, Sep. 2018, ISSN: 1949-3061. DOI:10.1109/TSG.2

017.2655083.
[101] H. Jouhara, A. Zabnie ˙ nska-Góra, N. Khordehgah, D. Ahmad, and T. Lipinski, “Latent ´ thermal energy storage technologies and applications: A review,” *International Journal* *of Thermofluids*, vol. 5-6, p. 100 039, Aug. 2020, ISSN: 26662027. DOI:10.1016/j.ijft.2

020.100039.
[102] Y. Parag and B. K. Sovacool, “Electricity market design for the prosumer era,” *Nature* *Energy*, vol. 1, no. 4, p. 16 032, Apr. 2016, ISSN: 2058-7546. DOI:10.1038/nenergy.2

016.32.
[103] S. Troitzsch, S. Hanif, and T. Hamacher, “Distributed Robust Reserve Scheduling in Congested Distribution Systems,” in *IEEE Power & Energy Society General Meeting* *(PESGM)*, Portland, OR: IEEE, Aug. 2018, ISBN: 978-1-5386-7703-2. DOI:10.1109 /PESGM.2018.8586650.

<u>Bibliography</u>

[104] S. Hanif, H. B. Gooi, T. Massier, T. Hamacher, and T. Reindl, “Distributed Congestion Management of Distribution Grids Under Robust Flexible Buildings Operations,” *IEEE* *Transactions on Power Systems*, vol. 32, no. 6, pp. 4600–4613, Nov. 2017, ISSN: 1558-0679. DOI:10.1109/TPWRS.2017.2660065.

[105] EMA Energy Market Authority, *Clarification on Eligibility Criteria for Participation in* *the Demand Response Programme*, 2016. [Online]. Available:[https://www.ema.gov.s](https://www.ema.gov.s) g/cmsmedia/Electricity/Demand_Response/Demand%20Response%20Clarification %20Information%20Paper.pdf(visited on Jul. 4, 2021).

[106] Y. Xiao, X. Wang, P. Pinson, and X. Wang, “Transactive Energy Based Aggregation of Prosumers as a Retailer,” *IEEE Transactions on Smart Grid*, pp. 1–1, 2020, ISSN: 1949-3053, 1949-3061. DOI:10.1109/TSG.2020.2976130.

[107] P. Mancarella, “MES (multi-energy systems): An overview of concepts and evaluation models,” *Energy*, vol. 65, pp. 1–17, Feb. 2014, ISSN: 03605442. DOI:10.1016/j.energ

y.2013.10.041.
[108] D. Pudjianto, C. Ramsay, and G. Strbac, “Virtual power plant and system integration of distributed energy resources,” *IET Renewable Power Generation*, vol. 1, no. 1,

p. 10, 2007, ISSN: 17521416. DOI:10.1049/iet-rpg:20060023.
[109] N. Naval and J. M. Yusta, “Virtual power plant models and electricity markets-A review,” *Renewable and Sustainable Energy Reviews*, vol. 149, p. 111 393, Oct. 2021, ISSN: 13640321. DOI:10.1016/j.rser.2021.111393.

[110] B. Mathiesen, H. Lund, D. Connolly, *et al.*, “Smart Energy Systems for coherent 100% renewable energy and transport solutions,” *Applied Energy*, vol. 145, pp. 139–154, May 2015, ISSN: 03062619. DOI:10.1016/j.apenergy.2015.01.075.

[111] E. Guelpa, A. Bischi, V. Verda, M. Chertkov, and H. Lund, “Towards future infrastruc- tures for sustainable multi-energy systems: A review,” *Energy*, vol. 184, pp. 2–21, Oct. 2019, ISSN: 03605442. DOI:10.1016/j.energy.2019.05.057.

[112] L. Kriechbaum, G. Scheiber, and T. Kienberger, “Grid-based multi-energy systems- modelling, assessment, open source modelling frameworks and challenges,” *Energy,* *Sustainability and Society*, vol. 8, no. 1, p. 35, Dec. 2018, ISSN: 2192-0567. DOI:

10.1186/s13705-018-0176-x.
[113] R. Suciu, L. Girardin, and F. Maréchal, “Energy integration of CO2 networks and power to gas for emerging energy autonomous cities in Europe,” *Energy*, vol. 157, pp. 830–842, Aug. 2018, ISSN: 03605442. DOI:10.1016/j.energy.2018.05.083.

[114] M. Minsky, “Matter, Mind and Models,” Mar. 1, 1965. [Online]. Available:[https://dspac](https://dspac)

e.mit.edu/handle/1721.1/6119(visited on Jul. 6, 2021).
[115] H.-K. Ringkjøb, P. M. Haugan, and I. M. Solbrekke, “A review of modelling tools for energy and electricity systems with large shares of variable renewables,” *Renewable* *and Sustainable Energy Reviews*, vol. 96, pp. 440–459, Nov. 2018, ISSN: 13640321. DOI:10.1016/j.rser.2018.08.002.

<u>Bibliography</u>

[116] C. Klemm and P. Vennemann, “Modeling and optimization of multi-energy systems in mixed-use districts: A review of existing methods and approaches,” *Renewable and* *Sustainable Energy Reviews*, vol. 135, p. 110 206, Jan. 2021, ISSN: 13640321. DOI:

10.1016/j.rser.2020.110206.
[117] J. Després, N. Hadjsaid, P. Criqui, and I. Noirot, “Modelling the impacts of vari- able renewable sources on the power sector: Reconsidering the typology of energy modelling tools,” *Energy*, vol. 80, pp. 486–495, Feb. 2015, ISSN: 03605442. DOI:

10.1016/j.energy.2014.12.005.
[118] P. Mancarella, G. Andersson, J. Pecas-Lopes, and K. Bell, “Modelling of integrated multi-energy systems: Drivers, requirements, and opportunities,” in *2016 Power Sys-* *tems Computation Conference (PSCC)*, Genoa, Italy: IEEE, Jun. 2016, pp. 1–22, ISBN: 978-88-941051-2-4. DOI:10.1109/PSCC.2016.7541031.

[119] I. van Beuzekom, M. Gibescu, and J. Slootweg, “A review of multi-energy system planning and optimization tools for sustainable urban development,” in *2015 IEEE* *Eindhoven PowerTech*, Eindhoven, Netherlands: IEEE, Jun. 2015, pp. 1–7, ISBN: 978-1-4799-7693-5. DOI:10.1109/PTC.2015.7232360.

[120] A. Herbst, F. Toro, F. Reitze, and E. Jochem, “Introduction to Energy Systems Mod- elling,” *Swiss Journal of Economics and Statistics*, vol. 148, no. 2, pp. 111–135, Apr. 2012, ISSN: 2235-6282. DOI:10.1007/BF03399363.

[121] D. Recalde, A. Trpovski, S. Troitzsch, K. Zhang, S. Hanif, and T. Hamacher, “A Review of Operation Methods and Simulation Requirements for Future Smart Distribution Grids,” in *IEEE PES Innovative Smart Grid Technologies Conference Asia*, May 2018, ISBN: 978-1-5386-4291-7. DOI:10.1109/ISGT-Asia.2018.8467850.

[122] NEPLAN. “NEPLAN – power system analysis.” (2021), [Online]. Available:[https://ww](https://ww)

w.neplan.ch/(visited on Mar. 22, 2021).
[123] Fischer-Uhrig Engineering. “STANET.” (2021), [Online]. Available:[http://stafu.de/en/h](http://stafu.de/en/h) ome.html(visited on Mar. 22, 2021).

[124] EPA Environmental Protection Agency. “EPANET.” (2021), [Online]. Available:https: //www.epa.gov/water-research/epanet(visited on Mar. 22, 2021).

[125] ETAP. “ETAP | Electrical Power System Analysis Software.” (2021), [Online]. Available: [https://etap.com(visited](https://etap.com(visited) on Mar. 19, 2021).

[126] S. Bruno, S. Lamonaca, G. Rotondo, U. Stecchi, and M. La Scala, “Unbalanced Three-Phase Optimal Power Flow for Smart Grids,” *IEEE Transactions on Industrial* *Electronics*, vol. 58, no. 10, pp. 4504–4513, Oct. 2011, ISSN: 0278-0046, 1557-9948. DOI:10.1109/TIE.2011.2106099.

[127] C. E. Murillo-Sanchez, R. D. Zimmerman, C. Lindsay Anderson, and R. J. Thomas, “Secure Planning and Operations of Systems With Stochastic Sources, Energy Stor- age, and Active Demand,” *IEEE Transactions on Smart Grid*, vol. 4, no. 4, pp. 2220– 2229, Dec. 2013, ISSN: 1949-3053, 1949-3061. DOI:10.1109/TSG.2013.2281001.

<u>Bibliography</u>

[128] L. Thurner, A. Scheidler, F. Schafer, *et al.*, “Pandapower-An Open-Source Python Tool for Convenient Modeling, Analysis, and Optimization of Electric Power Systems,” *IEEE Transactions on Power Systems*, vol. 33, no. 6, pp. 6510–6521, Nov. 2018, ISSN: 0885-8950, 1558-0679. DOI:10.1109/TPWRS.2018.2829021.

[129] R. Lincoln, *PYPOWER*, Mar. 20, 2021. [Online]. Available:[https://github.com/rwl](https://github.com/rwl) /PYPOWER(visited on Mar. 21, 2021).

[130] D. Lohmeier, D. Cronbach, S. R. Drauz, M. Braun, and T. M. Kneiske, “Pandapipes: An Open-Source Piping Grid Calculation Package for Multi-Energy Grid Simulations,” *Sustainability*, vol. 12, no. 23, p. 9899, Nov. 26, 2020, ISSN: 2071-1050. DOI:10.3390 /su12239899.

[131] D. M. Fobes, S. Claeys, F. Geth, and C. Coffrin, “PowerModelsDistribution.jl: An open-source framework for exploring distribution power flow formulations,” *Electric* *Power Systems Research*, vol. 189, p. 106 664, Dec. 2020, ISSN: 03787796. DOI:

10.1016/j.epsr.2020.106664.
[132] D. Atabay, “An open-source model for optimal design and operation of industrial energy systems,” *Energy*, vol. 121, pp. 803–821, Feb. 2017, ISSN: 03605442. DOI:

10.1016/j.energy.2017.01.030.
[133] S. Hilpert, C. Kaldemeyer, U. Krien, S. Günther, C. Wingenbach, and G. Plessmann, “The Open Energy Modelling Framework (oemof) - A new approach to facilitate open science in energy system modelling,” *Energy Strategy Reviews*, vol. 22, pp. 16–25, Nov. 2018, ISSN: 2211467X. DOI:10.1016/j.esr.2018.07.001.

[134] K. Hunter, S. Sreepathi, and J. F. DeCarolis, “Modeling for insight using Tools for En- ergy Model Optimization and Analysis (Temoa),” *Energy Economics*, vol. 40, pp. 339– 349, Nov. 2013, ISSN: 01409883. DOI:10.1016/j.eneco.2013.07.014.

[135] Sustainable Energy Planning Research group at Aalborg University. “EnergyPLAN,” EnergyPLAN. (), [Online]. Available:[https://www.energyplan.eu/(visited](https://www.energyplan.eu/(visited) on Mar. 25,

2021).
[136] EMD International. “energyPRO.” (2021), [Online]. Available:[https://www.emd.dk/ene](https://www.emd.dk/ene) rgypro/(visited on Mar. 25, 2021).

[137] IEA International Energy Agency. “IEA-ETSAP | Times.” (2021), [Online]. Available: [https://iea-](https://iea-) etsap.org/index.php/etsap- tools/model- generators/times(visited on Mar. 25, 2021).

[138] ISO International Organization for Standardization, *ISO/IEC/IEEE 12207: Systems* *and software engineering-Software life cycle processes*, 2017. [Online]. Available: [https://doi.org/10.1109/IEEESTD.2017.8100771(visited](https://doi.org/10.1109/IEEESTD.2017.8100771(visited) on Apr. 29, 2021).

[139] ISO International Organization for Standardization, *ISO/IEC/IEEE 24748-1: Systems* *and software engineering-Life cycle management-Part 1: Guidelines for life cycle* *management*, 2018. [Online]. Available:[https://doi.org/10.1109/IEEESTD.2018.8526](https://doi.org/10.1109/IEEESTD.2018.8526) 560(visited on Apr. 29, 2021).

<u>Bibliography</u>

[140] L. Bass, P. Clements, and R. Kazman, *Software Architecture in Practice*, 3rd ed, ser. SEI Series in Software Engineering. Upper Saddle River, NJ: Addison-Wesley, 2013, 589 pp., ISBN: 978-0-321-81573-6.

[141]S. McConnell, *Code Complete*. Microsoft Press, 2004, ISBN: 0-7356-1967-0.

[142] K. E. Wiegers and J. Beatty, *Software Requirements*, Third edition. Redmond, Wash- ington: Microsoft Press, s division of Microsoft Corporation, 2013, 637 pp., ISBN: 978-0-7356-7966-5.

[143] ISO International Organization for Standardization and IEC International Electrotech- nical Commission, *ISO/IEC 25010 - Systems and software engineering-Systems* *and software Quality Requirements and Evaluation (SQuaRE) - System and software* *quality models*, 2011.

[144] R. C. Martin, *Clean Architecture: A Craftsman’s Guide to Software Structure and* *Design*, ser. Robert C. Martin Series. London, England: Prentice Hall, 2018, 404 pp., ISBN: 978-0-13-449416-6.

[145]M. Richards, *Software Architecture Patterns*. 2015, ISBN: 978-1-4919-2424-2.

[146] F. Buschmann, Ed., *Pattern-Oriented Software Architecture: A System of Patterns*. Chichester; New York: Wiley, 1996, 457 pp., ISBN: 978-0-471-95869-7.

[147] J. Vlissides, R. Johnson, R. Helm, and E. Gamma, *Design Patterns: Elements of* *Reusable Object-Oriented Software*. Addison-Wesley, 1994, ISBN: 0-201-63361-2.

[148]Object Management Group, *Unified Modeling Language, v2.5.1*, 2017.

[149] S. Brown. “The C4 model for visualising software architecture.” (2021), [Online]. Available:[https://c4model.com/(visited](https://c4model.com/(visited) on May 10, 2021).

[150] S. Brown, *Software Architecture for Developers-Visualise, Document and Explore* *Your Software Architecture*. Leanpub, Aug. 29, 2015, vol. 2. [Online]. Available:https: //leanpub.com/visualising-software-architecture(visited on May 10, 2021).

[151] The Open Group, *Open Agile Architecture: A Standard of The Open Group*. ’s- Hertogenbosch: Van Haren Publishing, 2020, ISBN: 978-94-018-0726-5. [Online]. Available:[https://pubs.opengroup.org/architecture/o-aa-standard/(visited](https://pubs.opengroup.org/architecture/o-aa-standard/(visited) on May 10,

2021).
[152] The YAML Project. “The Official YAML Web Site.” (2020), [Online]. Available:https://y aml.org/(visited on May 11, 2021).

[153] Dheepak Krishnamurthy, Paulo Meira, and Max Zangs, *OpenDSSDirect.py*, DSS Extensions, 2021. [Online]. Available:[https://github.com/dss-extensions/OpenDSSDir](https://github.com/dss-extensions/OpenDSSDir) ect.py(visited on May 18, 2021).

[154] K. Reitz and T. Schlusser, *The Hitchhiker’s Guide to Python: Best Practices for* *Development*. Sebastopol, California: O’Reilly Media, Inc, 2016, 321 pp., ISBN: 978-1- 4919-3317-6. [Online]. Available:[https://docs.python-guide.org/(visited](https://docs.python-guide.org/(visited) on Jun. 5,

2021).
199

<u>Bibliography</u>

[155]

[156]

[157]

[158]

[159]

[160]

[161]

[162]

[163]

[164]

[165]

[166]

[167]

[168]

[169]

S. Chacon and B. Straub, *Pro Git*, Second edition. New York, NY: Apress, 2014, 426 pp., ISBN: 978-1-4842-0077-3. [Online]. Available:[https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2) (visited on Jun. 6, 2021). Georg Brandl, *Sphinx*, sphinx-doc, Jun. 5, 2021. [Online]. Available:[https://github.co](https://github.co) m/sphinx-doc/sphinx(visited on Jun. 5, 2021).
K. Beck, *Test-Driven Development: By Example*, ser. The Addison-Wesley Signature Series. Boston: Addison-Wesley, 2003, 220 pp., ISBN: 978-0-321-14653-3. Vincent Driessen. “A successful Git branching model,” nvie.com. (2010), [Online]. Available:[http://nvie.com/posts/a-successful-git-branching-model/(visited](http://nvie.com/posts/a-successful-git-branching-model/(visited) on May 15,
2021).
T. Preston-Werner. “Semantic Versioning 2.0.0,” Semantic Versioning. (2013), [Online]. Available:[https://semver.org/(visited](https://semver.org/(visited) on Jun. 6, 2021).
R. H. Howell, W. J. Coad, and H. J. Sauer, *Principles of Heating, Ventilating and Air* *Conditioning*, 5. 2013, vol. 222, ISBN: 978-1-936504-57-2. DOI:10.1016/s0016-0032 (36)91011-6.
P. Klingel, *Modellierung von Wasserverteilungssystemen*. Wiesbaden: Springer Fachme- dien Wiesbaden, 2018, ISBN: 978-3-658-21269-8. DOI:10.1007/978-3-658-21270-4.
D. Zehe, S. Nair, A. Knoll, and D. Eckhoff, “Towards CityMoS: A coupled city-scale mobility simulation framework,” in *5th GI/ITG KuVS Fachgespräch Inter-Vehicle Com-* *munication (FG-IVC 2017)*, Erlangen, Germany: FAU Erlangen-Nuremberg, Apr. 2017.
M. Gallet, T. Massier, and D. Zehe, “Developing a Large-Scale Microscopic Model of Electric Public Bus Operation and Charging,” in *2019 IEEE Vehicle Power and* *Propulsion Conference (VPPC)*, Hanoi, Vietnam: IEEE, Oct. 2019, pp. 1–5, ISBN: 978-1-72811-249-7. DOI:10.1109/VPPC46532.2019.8952361.
S. Troitzsch and T. Hamacher, “Control-oriented Thermal Building Modelling,” in *IEEE* *PES General Meeting*, Aug. 2020. DOI:10.1109/PESGM41954.2020.9281503.
S. P. Boyd and L. Vandenberghe, *Convex Optimization*. Cambridge, UK; New York: Cambridge University Press, 2004, 716 pp., ISBN: 978-0-521-83378-3. EMC Energy Market Company. “Price Information.” (2021), [Online]. Available:https: //www.emcsg.com/marketdata/priceinformation(visited on Jul. 21, 2021). LTA Land Transport Authority Singapore. “DataMall.” (2021), [Online]. Available:https: //datamall.lta.gov.sg/(visited on Jun. 21, 2021). LTA Land Transport Authority. “Annual Mileage for Private Motor Vehicles,” Data.gov.sg. (2020), [Online]. Available:[https://data.gov.sg/dataset/annual-mileage-for-private-mo](https://data.gov.sg/dataset/annual-mileage-for-private-mo) tor-vehicles(visited on Jul. 15, 2021). LTA Land Transport Authority. “Current Vehicle Growth Rate to Continue until 31 January 2022.” (2020), [Online]. Available:[https://www.lta.gov.sg/content/ltagov/en/n](https://www.lta.gov.sg/content/ltagov/en/n) ewsroom/2020/8/news-releases/current-vehicle-growth-rate-to-continue-until-31-ja nuary-2022.html(visited on Jul. 15, 2021).
200

<u>Bibliography</u>

[170] LTA Land Transport Authority, *Annual Vehicle Statistics*, 2020. [Online]. Available: [https://www.lta.gov.sg/content/dam/ltagov/who_we_are/statistics_and_publications](https://www.lta.gov.sg/content/dam/ltagov/who_we_are/statistics_and_publications) /statistics/pdf/MVP01-1_MVP_by_type.pdf(visited on Jul. 15, 2021).

[171] EV Database. “Energy consumption of full electric vehicles,” EV Database. (2021), [Online]. Available:[https://ev-database.org/cheatsheet/energy-consumption-electric-](https://ev-database.org/cheatsheet/energy-consumption-electric-) car(visited on Jul. 15, 2021).

[172] BCA Building Construction Authority Singapore, *BCA Building Energy Benchmarking* *Report 2018*, 2018. [Online]. Available:[https://www.bca.gov.sg/GreenMark/others](https://www.bca.gov.sg/GreenMark/others) /BCA_BEBR_Abridged_FA_2018.pdf.

[173] W. F. Holmgren, C. W. Hansen, and M. A. Mikofski, “Pvlib python: A python package for modeling solar energy systems,” *Journal of Open Source Software*, vol. 3, no. 29,

p. 884, 2018. DOI:10.21105/joss.00884.
201
