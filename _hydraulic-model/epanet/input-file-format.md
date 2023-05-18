---
title:  "EPANET: Input File Format"
sequence: 002
---

## 概览

The input file for command line EPANET is organized in sections, where each section begins with a keyword enclosed in brackets.

<table>
    <caption>EPANET Input File Format</caption>
    <thead>
    <tr>
        <th>
            <p><em>Network</em></p>
            <p><em>Components</em></p>
        </th>
        <th>
            <p><em>System</em></p>
            <p><em>Operation</em></p>
        </th>
        <th>
            <p><em>Water</em></p>
            <p><em>Quality</em></p>
        </th>
        <th><em>Options</em></th>
        <th>
            <p><em>Network</em></p>
            <p><em>Map/Tags</em></p>
        </th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
            <p>[TITLE]</p>
            <p>[JUNCTIONS]</p>
            <p>[RESERVOIRS]</p>
            <p>[TANKS]</p>
            <p>[PIPES]</p>
            <p>[PUMPS]</p>
            <p>[VALVES]</p>
            <p>[EMITTERS]</p>
        </td>
        <td>
            <p>[CURVES]</p>
            <p>[PATTERNS]</p>
            <p>[ENERGY]</p>
            <p>[STATUS]</p>
            <p>[CONTROLS]</p>
            <p>[RULES]</p>
            <p>[DEMANDS]</p>
        </td>
        <td>
            <p>[QUALITY]</p>
            <p>[REACTIONS]</p>
            <p>[SOURCES]</p>
            <p>[MIXING]</p>
        </td>
        <td>
            <p>[OPTIONS]</p>
            <p>[TIMES]</p>
            <p>[REPORT]</p>
        </td>
        <td>
            <p>[COORDINATES]</p>
            <p>[VERTICES]</p>
            <p>[LABELS]</p>
            <p>[BACKDROP]</p>
            <p>[TAGS]</p>
        </td>
    </tr>
    </tbody>
</table>

The order of sections is not important.
However, whenever a node or link is referred to in a section
it must have already been defined in the `[JUNCTIONS]`, `[RESERVOIRS]`,
`[TANKS]`, `[PIPES]`, `[PUMPS]`, or `[VALVES]` sections.
Therefore, it is recommended that these sections be placed first,
right after the `[TITLE]` section.
**The network map and tags sections**（上表当中的第五列） are not used by command line EPANET
and can be eliminated from the file.

> section的顺序不重要

Each section can contain one or more lines of data.
**Blank lines** can appear anywhere in the file and 
**the semicolon** (`;`) can be used to indicate that what follows on the line is a comment, not data.
**A maximum of 255 characters** can appear on a line.
The `ID` labels used to identify **nodes**, **links**, **curves** and **patterns**
can be any combination of up to 31 characters and numbers.

> 每一个section的要求

在每一行数据当中，

- 空行：可以出现在任何地方
- 分号：后面的数据是注释，不用考虑
- 一行字符的最大数量：255
- ID的最大字符数：31

```text
[TITLE]
EPANET TUTORIAL

[JUNCTIONS]
;ID   Elev   Demand
;------------------
2     0      0
3     710    650
4     700    150
5     695    200
6     700    150

[RESERVOIRS]
;ID   Head
;---------
1     700

[TANKS]
;ID  Elev  InitLvl  MinLvl  MaxLvl  Diam  Volume
;-----------------------------------------------
7    850   5        0       15      70    0

[PIPES]
;ID  Node1  Node2  Length  Diam  Roughness
;-----------------------------------------
1    2      3      3000    12    100
2    3      6      5000    12    100
3    3      4      5000    8     100
4    4      5      5000    8     100
5    5      6      5000    8     100
6    6      7      7000    10    100

[PUMPS]
;ID  Node1  Node2  Parameters
;---------------------------------
7    1      2      HEAD  1

[PATTERNS]
;ID   Multipliers
;-----------------------
1       0.5  1.3  1  1.2

[CURVES]
;ID  X-Value  Y-Value
;--------------------
1    1000     200

[QUALITY]
;Node InitQual
;-------------
1     1

[REACTIONS]
Global Bulk -1
Global Wall 0

[TIMES]
Duration           24:00
Hydraulic Timestep 1:00
Quality Timestep   0:05
Pattern Timestep   6:00

[REPORT]
Page      55
Energy    Yes
Nodes     All
Links     All

[OPTIONS]
Units           GPM
Headloss        H-W
Pattern         1
Quality         Chlorine mg/L
Tolerance       0.01

[END]
```

## Network Components

### TITLE

Attaches a descriptive title to the network being analyzed.

**Format**

Any number of lines of text.

**Remarks**

- The `[TITLE]` section is optional.

### JUNCTIONS

Defines junction nodes contained in the network.

**Format**

One line for each junction containing:

- ID label
- Elevation, 单位：米(m)
- Base demand flow (flow units) (optional)
- Demand pattern ID (optional)

**Remarks**

- A `[JUNCTIONS]` section with at least one junction is required.
- If no demand pattern is supplied then the junction demand follows the Default Demand Pattern specified in the `[OPTIONS]` section or Pattern 1 if no default pattern is specified.
  If the default pattern (or Pattern 1) does not exist, then the demand remains constant.
- Demands can also be entered in the `[DEMANDS]` section and include multiple demand categories per junction.

```text
[JUNCTIONS]
;ID    Elev.   Demand   Pattern
;------------------------------
J1     100     50       Pat1
J2     120     10              ;Uses default demand pattern
J3     115                     ;No demand at this junction
```

### PIPES

Defines all pipe links contained in the network.

**Format**

One line for each pipe containing:

- ID label of pipe
- ID of start node
- ID of end node
- Length, 单位：米(m)
- Diameter, 单位：毫米(mm)
- Roughness coefficient
- Minor loss coefficient
- Status (`OPEN`, `CLOSED`, or `CV`)

**Remarks**

- Roughness coefficient is unitless for the Hazen-Williams and Chezy-Manning head loss formulas and has units of millifeet (mm) for the Darcy-Weisbach formula.
  Choice of **head loss formula** is supplied in the `[OPTIONS]` section.
- Setting status to `CV` means that the pipe contains a check valve restricting flow to one direction.
- If **minor loss coefficient** is `0` and pipe is `OPEN` then these two items can be dropped from the input line.

**Example**

```text
[PIPES]
;ID   Node1  Node2   Length   Diam.   Roughness  Mloss   Status
;-------------------------------------------------------------
 P1    J1     J2     1200      12       120       0.2    OPEN
 P2    J3     J2      600       6       110       0      CV
 P3    J1     J10    1000      12       120
```

### PUMPS

Defines all pump links contained in the network.

**Format**

One line for each pump containing:

- ID label of pump
- ID of start node
- ID of end node
- Keyword and Value (can be repeated)

**Remarks**

Keywords consists of:

- **POWER** – power value for constant energy pump, hp (kW)
- **HEAD** - ID of curve that describes **head versus flow** for the pump
- **SPEED** - relative speed setting (normal speed is 1.0, 0 means pump is off)
- **PATTERN** - ID of time pattern that describes how speed setting varies with time

Either **POWER** or **HEAD** must be supplied for each pump. The other keywords are optional.

**Example**

```text
[PUMPS]
;ID    Node1    Node2    Properties
;---------------------------------------------
Pump1   N12      N32     HEAD Curve1
Pump2   N121     N55     HEAD Curve1  SPEED 1.2
Pump3   N22      N23     POWER 100
```

### RESERVOIRS

Defines all reservoir nodes contained in the network.

**Format**:

One line for each reservoir containing:

- ID label
- Head, ft (m)
- Head pattern ID (optional)

**Remarks**:

- Head is the hydraulic head (elevation + pressure head) of water in the reservoir.
- A **head pattern** can be used to make the reservoir head vary with time.
- At least one reservoir or tank must be contained in the network.

**Example**:

```text
[RESERVOIRS]
;ID    Head    Pattern
;---------------------
R1     512               ;Head stays constant
R2     120     Pat1      ;Head varies with time
```

### TANKS

Defines all tank nodes contained in the network.

**Format:**

One line for each tank containing:

- ID label
- Bottom elevation, (m)
- Initial water level, (m)
- Minimum water level, (m)
- Maximum water level, (m)
- Nominal diameter, (m)
- Minimum volume, (cubic meters)
- Volume curve ID (optional)

**Remarks**:

- Water surface elevation equals bottom elevation plus water level.
- Non-cylindrical tanks can be modeled by specifying a curve of volume versus water depth in the `[CURVES]` section.
- If a volume curve is supplied the diameter value can be any non-zero number
- Minimum volume (tank volume at minimum water level) can be zero for a cylindrical tank or if a volume curve is supplied.
- A network must contain at least one tank or reservoir.

**Example**:

```text
[TANKS]
;ID   Elev.  InitLvl  MinLvl  MaxLvl  Diam  MinVol  VolCurve
;-----------------------------------------------------------
;Cylindrical tank
T1    100     15       5       25     120    0
;Non-cylindrical tank with arbitrary diameter
T2    100     15       5       25      1     0      VC1
```

## System Operation

### CONTROLS

Defines simple controls that modify links based on a single condition.

**Format**:

One line for each control which can be of the form:

| 1    | 2      | 3      | 4   | 5         | 6      | 7           | 8     |
|------|--------|--------|-----|-----------|--------|-------------|-------|
| LINK | linkID | status | IF  | NODE      | nodeID | ABOVE/BELOW | value |
| LINK | linkID | status | AT  | TIME      | time   |             |       |
| LINK | linkID | status | AT  | CLOCKTIME | time	  | AM/PM       |       |

where:

- `linkID` = a link ID label
- `status` = `OPEN` or `CLOSED`, **a pump speed setting**, or **a control valve setting**
- `nodeID` = a node ID label
- `value` = a **pressure** for a **junction** or a **water level** for a **tank**
- `time` = a time since the start of the simulation in decimal hours or in `hours:minutes` format
- `time` = a 12-hour clock time (`hours:minutes`)

Remarks:

- Simple controls are used to change **link status or settings**
  based on **tank water level**, **junction pressure**, **time into the simulation or time of day**.
- See the notes for the `[STATUS]` section for conventions used in specifying **link status and setting**,
  particularly for **control valves**.

### CURVES

Defines data curves and their X,Y points.

**Format**:

One line for each X,Y point on each curve containing:

- Curve ID label
- X value
- Y value

Remarks:

- Curves can be used to represent the following relations:
  - Head v. Flow for pumps
  - Efficiency v. Flow for pumps
  - Volume v. Depth for tanks
  - Headloss v. Flow for General Purpose Valves
- **The points of a curve must be entered in order of increasing X-values (lower to higher)**.
- If the input file will be used with the Windows version of EPANET,
  then adding a comment which contains the curve type and description, separated by a colon,
  directly above the first entry for a curve will ensure that these items appear correctly in EPANET's Curve Editor.
  Curve types include **PUMP**, **EFFICIENCY**, **VOLUME**, and **HEADLOSS**.

**Example**:

```text
[CURVES]
;ID   Flow    Head
;PUMP: Curve for Pump 1 C1 0 200
C1    1000    100
C1    3000    0

;ID   Flow    Effic.
;EFFICIENCY:
E1    200     50
E1    1000    85
E1    2000    75
E1    3000    65
```

### DEMANDS

Supplement to `[JUNCTIONS]` section for defining multiple water demands at junction nodes.

**Format**:

One line for each category of demand at a junction containing:

- Junction ID label
- Base demand (flow units)
- Demand pattern ID (optional)
- Name of demand category preceded by a semicolon (optional)

**Remarks**:

- Only use for **junctions** whose demands need to be changed or supplemented from entries in `[JUNCTIONS]` section.
- Data in this section replaces any demand entered in `[JUNCTIONS]` section for the same junction.
- Unlimited number of **demand categories** can be entered per junction.
- If no demand pattern is supplied
  then the junction demand follows the **Default Demand Pattern** specified in the `[OPTIONS]` section or
  Pattern 1 if no default pattern is specified.
  If the default pattern (or Pattern 1) does not exist, then the demand remains constant.

Example:

```text
[DEMANDS]
;ID    Demand   Pattern   Category
;---------------------------------
J1     100      101       ;Domestic
J1     25       102       ;School
J256   50       101       ;Domestic
```

### PATTERNS

Defines time patterns.

**Format**:

One or more lines for each pattern containing:

- Pattern ID label
- One or more multipliers

**Remarks**:

Multipliers define how some base quantity (e.g., demand) is adjusted for each time period.

- All patterns share the same time period interval as defined in the `[TIMES]` section.
- Each pattern can have a different number of time periods.
- When the simulation time exceeds the pattern length the pattern wraps around to its first period.
- Use as many lines as it takes to include all multipliers for each pattern.

**Example**:

```text
[PATTERNS]
;Pattern P1
P1    1.1    1.4    0.9    0.7
P1    0.6    0.5    0.8    1.0
;Pattern P2
P2    1      1      1      1
P2    0      0      1
```

### RULES

Defines rule-based controls that modify **links** based on a combination of conditions.

**Format**:

Each rule is a series of statements of the form:

| 1        | 2           |
|----------|-------------|
| RULE     | ruleID      |
| IF       | condition_1 |
| AND      | condition_2 |
| OR       | condition_3 |
| AND      | condition_4 |
| etc.     |             |
| THEN     | action_1    |
| AND      | action_2    |
| etc.     |             |
| ELSE     | action_3    |
| AND      | action_4    |
| etc.     |             |
| PRIORITY | value       |

where:

- `ruleID` = an ID label assigned to the rule
- `conditon_n` = a condition clause
- `action_n` = an action clause
- `Priority` = a priority value (e.g., a number from `1` to `5`)

**Remarks**:

- Only the `RULE`, `IF` and `THEN` portions of a rule are required; the other portions are optional.
- When mixing `AND` and `OR` clauses, the `OR` operator has higher precedence than `AND`, i.e.,

```text
IF A or B and C
```

is equivalent to

```text
IF (A or B) and C.
```

If the interpretation was meant to be

```text
IF A or (B and C)
```

then this can be expressed using two rules as in

```text
IF A THEN ...
IF B and C THEN ...
```

- The `PRIORITY` value is used to determine which rule applies
  when two or more rules require that conflicting actions be taken on a link.
  A rule without a priority value always has a lower priority than one with a value.
  For two rules with the same priority value, the rule that appears first is given the higher priority.

**Example**:

```text
[RULES]
RULE 1
IF TANK 1 LEVEL ABOVE 19.1
THEN PUMP 335 STATUS IS CLOSED
AND PIPE 330 STATUS IS OPEN

RULE 2
IF SYSTEM CLOCKTIME >= 8 AM
AND SYSTEM CLOCKTIME < 6 PM
AND TANK 1 LEVEL BELOW 12
THEN PUMP 335 STATUS IS OPEN

RULE 3
IF SYSTEM CLOCKTIME >= 6 PM
OR SYSTEM CLOCKTIME < 8 AM
AND TANK 1 LEVEL BELOW 14
THEN PUMP 335 STATUS IS OPEN
```

#### Condition Clause Format

A condition clause in a Rule-Based Control takes the form of:

| 1      | 2   | 3         | 4        | 5     |
|--------|-----|-----------|----------|-------|
| object | id  | attribute | relation | value |

where:

- `object` = a category of network object
- `id` = the object’s ID label
- `attribute` = an attribute or property of the object
- `relation` = a relational operator
- `value` = an attribute value

Some example conditional clauses are:

```text
JUNCTION 23 PRESSURE > 20
TANK T200 FILLTIME BELOW 3.5
LINK 44 STATUS IS OPEN
SYSTEM DEMAND >= 1500
SYSTEM CLOCKTIME = 7:30 AM
```

The `Object` keyword can be any of the following:

| 1         | 2     | 3      |
|-----------|-------|--------|
| NODE      | LINK  | SYSTEM |
| JUNCTION  | PIPE  |        |
| RESERVOIR | PUMP  |        |
| TANK      | VALVE |        |

When `SYSTEM` is used in a condition no ID is supplied.

The following **attributes** can be used with `Node`-type objects:

- DEMAND
- HEAD
- PRESSURE

The following **attributes** can be used with `Tank`s:

- `LEVEL`
- `FILLTIME` (hours needed to fill a tank)
- `DRAINTIME` (hours needed to empty a tank)

These **attributes** can be used with `Link`-Type objects:

- `FLOW`
- `STATUS` (`OPEN`, `CLOSED`, or `ACTIVE`)
- `SETTING` (**pump speed** or **valve setting**)

The SYSTEM object can use the following **attributes**:

- `DEMAND` (**total system demand**)
- `TIME` (hours from the start of the simulation expressed either as a **decimal number** or in `hours:minutes` format)
- `CLOCKTIME` (24-hour clock time with `AM` or `PM` appended)

Relation operators consist of the following:

| 1    | 2       |
|------|---------|
| `=`  | `IS`    |
| `<>` | `NOT`   |
| `<`  | `BELOW` |
| `>`  | `ABOVE` |
| `<=` | `>=`    |


#### Action Clause Format

An action clause in a Rule-Based Control takes the form of:

| 1      | 2   | 3              | 4   | 5     |
|--------|-----|----------------|-----|-------|
| object | id  | STATUS/SETTING | IS  | value |

where:

- `object` = `LINK`, `PIPE`, `PUMP`, or `VALVE` keyword
- `id` = the object's ID label
- `value` = a status condition (`OPEN` or `CLOSED`), **pump speed setting**, or **valve setting**

Some example action clauses are:

```text
LINK 23 STATUS IS CLOSED
PUMP P100 SETTING IS 1.5
VALVE 123 SETTING IS 90
```



### STATUS

Defines **initial status of selected links** at the start of a simulation.

**Format**:

One line per link being controlled containing:

- Link ID label
- Status or setting

**Remarks**:

- Links not listed in this section have a default status of `OPEN` (for **pipes** and **pumps**) or `ACTIVE` (for valves).
- The `status` value can be `OPEN` or `CLOSED`.
  For control valves (e.g., `PRV`s, `FCV`s, etc.) this means that the valve is either fully opened or closed,
  not active at its control setting.
- The `setting` value can be a **speed setting for pumps** or **valve setting for valves**.
- The **initial status of pipes** can also be set in the `[PIPES]` section.
- **Check valves** cannot have their status be preset.
- Use `[CONTROLS]` or `[RULES]` to change **status or setting** at some future point in the simulation.
- If a `CLOSED` or `OPEN` control valve is to become `ACTIVE` again,
  then its **pressure or flow setting** must be specified in the **control or rule** that re-activates it.

**Example**:

```text
[STATUS]
; Link   Status/Setting
;----------------------
  L22     CLOSED         ;Link L22 is closed
  P14     1.5            ;Speed for pump P14
  PRV1    OPEN           ;PRV1 forced open
                         ;(overrides normal operation)
```

## Options

### OPTIONS

Defines various simulation options.

**Formats**:

<table>
  <tbody>
  <tr>
    <th class="w3-center">UNITS</th>
    <td>
      CFS/GPM/MGD/IMGD/AFD/<br/>
      LPS/LPM/MLD/CMH/CMD
    </td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">HEADLOSS</th>
    <td>H-W/D-W/C-M</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">HYDRAULICS</th>
    <td>USE/SAVE</td>
    <td>filename</td>
  </tr>
  <tr>
    <th class="w3-center">QUALITY</th>
    <td>NONE/CHEMICAL/AGE/TRACE</td>
    <td>id</td>
  </tr>
  <tr>
    <th class="w3-center">VISCOSITY</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">DIFFUSIVITY</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">SPECIFIC GRAVITY</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">TRIALS</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">ACCURACY</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">HEADERROR</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">FLOWCHANGE</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">UNBALANCED</th>
    <td>STOP/CONTINUE/CONTINUE</td>
    <td>n</td>
  </tr>
  <tr>
    <th class="w3-center">PATTERN</th>
    <td>id</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">DEMAND MODEL</th>
    <td>DDA/PDA</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">MINIMUM PRESSURE</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">REQUIRED PRESSURE</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">PRESSURE EXPONENT</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">DEMAND MULTIPLIER</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">EMITTER EXPONENT</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">TOLERANCE</th>
    <td>value</td>
    <td></td>
  </tr>
  <tr>
    <th class="w3-center">MAP</th>
    <td>filename</td>
    <td></td>
  </tr>
  </tbody>
</table>

```text
                                                                         ┌─── LPS
                                                                         │
                                                                         ├─── LPM
                                                                         │
                              ┌─── Units of Measurement ───┼─── UNITS ───┼─── MLD
                              │                                          │
                              │                                          ├─── CMH
                              │                                          │
                              │                                          └─── CMD
                              │
                              │                                                              ┌─── H-W: Hazen-Williams
                              │                                                              │
                              │                            ┌─── pipe ───────┼─── HEADLOSS ───┼─── D-W: Darcy-Weisbach
                              │                            │                                 │
                              │                            │                                 └─── C-M: Chezy-Manning
                              ├─── component ──────────────┤
                              │                            │                                ┌─── PATTERN (Default Pattern)
                              │                            │                ┌─── demand ────┤
                              │                            └─── junction ───┤               └─── DEMAND MULTIPLIER
                              │                                             │
                              │                                             └─── emitter ───┼─── EMITTER EXPONENT
                              │
                              │                            ┌─── VISCOSITY (Relative Viscosity)
                              ├─── fluid ──────────────────┤
                              │                            └─── SPECIFIC GRAVITY
                              │
           ┌─── Hydraulics ───┤                                                               ┌─── DDA
           │                  │                                                               │
           │                  │                            ┌─── DEMAND MODEL ─────────────────┤           ┌─── MINIMUM PRESSURE
           │                  │                            │                                  │           │
           │                  │                            │                                  └─── PDA ───┼─── REQUIRED PRESSURE
           │                  │                            │                                              │
           │                  │                            │                                              └─── PRESSURE EXPONENT
           │                  │                            │
           │                  │                            ├─── run ──────────────────────────┼─── TRIALS (Maximum Trials)
           │                  │                            │
           │                  ├─── solve ──────────────────┤                                  ┌─── ACCURACY
           │                  │                            │                                  │
           │                  │                            ├─── convergence ──────────────────┼─── HEADERROR (Max. Head Error)
           │                  │                            │                                  │
           │                  │                            │                                  └─── FLOWCHANGE (Max. Flow Change)
           │                  │                            │
OPTIONS ───┤                  │                            │                                  ┌─── STOP
           │                  │                            │                                  │
           │                  │                            └─── UNBALANCED (If Unbalanced) ───┼─── CONTINUE
           │                  │                                                               │
           │                  │                                                               └─── CONTINUE n
           │                  │
           │                  │                                               ┌─── SAVE
           │                  └─── result ─────────────────┼─── HYDRAULICS ───┤
           │                                                                  └─── USE
           │
           │                                                             ┌─── NONE
           │                                                             │
           │                                                             ├─── CHEMICAL
           │                  ┌─── QUALITY ──────────────────────────────┤
           │                  │                                          ├─── AGE
           │                  │                                          │
           └─── Quality ──────┤                                          └─── TRACE
                              │
                              ├─── DIFFUSIVITY (Relative Diffusivity)
                              │
                              └─── TOLERANCE (Quality Tolerance)
```

**Definitions**:

**UNITS** sets the units in which flow rates are expressed where:

- **CFS** = cubic feet per second
- **GPM** = gallons per minute
- **MGD** = million gallons per day
- **IMGD** = Imperial MGD
- **AFD** = acre-feet per day
- **LPS** = liters per second
- **LPM** = liters per minute
- **MLD** = million liters per day
- **CMH** = cubic meters per hour
- **CMD** = cubic meters per day

For **CFS**, **GPM**, **MGD**, **IMGD**, and **AFD** other input quantities are expressed in US Customary Units.
If flow units are in liters or cubic meters then Metric Units must be used for all other input quantities as well.
The default flow units are **GPM**.

> 在EPANET中，默认的 flow units 是 GPM（加仑每分钟）；在项目的监测数据中（安徽安庆），水表的单位是 CMH（立方米/小时）

**HEADLOSS** selects a formula to use for computing head loss for flow through a pipe.
The choices are the Hazen-Williams (**H-W**), Darcy-Weisbach (**D-W**), or Chezy-Manning (**C-M**) formulas.
The default is **H-W**.

> 水头损失，默认使用 H-W

**HYDRAULICS** option allows you to either **SAVE** the current hydraulics solution to a file or
**USE** a previously saved hydraulics solution.
This is useful when studying factors that only affect water quality behavior.

> hydraulic solution 何去何从

**QUALITY** selects the type of water quality analysis to perform.
The choices are **NONE**, **CHEMICAL**, **AGE**, and **TRACE**.
In place of **CHEMICAL** the actual name of the chemical can be used followed by its concentration units
(e.g., **CHLORINE mg/L**).
If **TRACE** is selected it must be followed by the ID label of the node being traced.
The default selection is **NONE** (no water quality analysis).

In lieu of **Chemical**, you can  enter the actual name of the chemical being modeled (e.g., **Chlorine**).

> 水质分析

**VISCOSITY** is the kinematic viscosity of the fluid being modeled
relative to that of water at 20 deg. C (1.0 centistoke).
The default value is **1.0**.

> 水质分析-运动粘性系数

**DIFFUSIVITY** is the molecular diffusivity of the chemical being analyzed relative to that of chlorine in water.
The default value is **1.0**.
Diffusivity is only used when mass transfer limitations are considered in pipe wall reactions.
A value of `0` will cause EPANET to ignore mass transfer limitations.

> 水质分析-分子扩散系数

**SPECIFIC GRAVITY** is the ratio of the density of the fluid being modeled to that of water at 4 deg. C (unitless).

> 水质分析-相对密度。某种液体，它相对于水在4摄氏度的时候的密度。

<p>
    同一种物质，随着温度、压强的变化，其密度也会有所变化。
    以水为例，水在4℃的时候密度达到最大值，随着温度的升高，其密度也会越来越小。
    因此，确定水在4℃时的密度为其标准密度。
</p>
<p>
    4℃时的水的密度\(\rho_{w}=1000kg/m^{3}\)，
    固体和流体的密度\(\rho\)的比重\(s\)就是以水的密度为标准的，
    用公式表示如下：
</p>
<p>
    \[
    s(比重) = \frac{\rho(流体的密度kg/m^{3})}{\rho_{w}(水的密度1000kg/m^{3})}
    \]
</p>

**TRIALS** are the maximum number of trials used to solve network hydraulics
at each hydraulic time step of a simulation.
The default is `200`.

> 水力计算-尝试计算的次数

**ACCURACY** prescribes the convergence criterion that determines when a hydraulic solution has been reached.
The trials end when **the sum of all flow changes** from the previous solution
divided by **the total flow in all links** is less than this number.
The default is **0.001**.

> 水力计算-收敛-精度

**HEADERROR** augments **ACCURACY** option.
Sets the maximum head loss error that any network link can have for hydraulic convergence to occur.
A link's head loss error is the difference between the head loss found as a function of computed flow in the link
(such as by the Hazen-Williams equation for a pipe) and the difference in computed heads for the link's end nodes.
The units of this parameter are feet (US) or meters (SI).
The default value of `0` indicates that no head error limit applies.

> 水力计算-收敛-最大的水头损失误差

**FLOWCHANGE** augments the **ACCURACY** option.
Sets the largest change in flow that any network element
(link, emitter, or pressure driven demand) can have for hydraulic convergence to occur.
It is specified in whatever flow units the project is using.
The default value of `0` indicates that no flow change limit applies.

> 水力计算-收敛-最大的流量变化范围

**UNBALANCED** determines what happens if a hydraulic solution cannot be reached
within the prescribed number of **TRIALS** at some hydraulic time step into the simulation.
“**STOP**” will halt the entire analysis at that point.
“**CONTINUE**” will continue the analysis with a warning message issued.
“**CONTINUE n**” will continue the search for a solution for another “n” trials
with the status of all links held fixed at their current settings.
The simulation will be continued at this point with a message issued about whether convergence was achieved or not.
The default choice is “STOP”.

> 水力计算-收敛失败

**PATTERN** provides the ID label of a **default demand pattern** to be applied to all **junctions**
where no demand pattern was specified.
If no such pattern exists in the `[PATTERNS]` section
then by default the pattern consists of a single multiplier equal to `1.0`.
If this option is not used, then the global default demand pattern has a label of “1”.

**DEMAND MULTIPLIER** is used to adjust the values of baseline demands
for **all junctions** and **all demand categories**.
For example, a value of 2 doubles all baseline demands, while a value of 0.5 would halve them.
The default value is 1.0.

<p>
<strong>DEMAND MODEL</strong> determines nodal demand model – Demand Driven Analysis (<strong>DDA</strong>) or
Pressure Driven Analysis (<strong>PDA</strong>).
DDA assumes a nodal demand at a given point in time is a fixed value <span>\(D\)</span>.
This sometimes results in hydraulic solutions with negative pressures (a physical impossibility).
PDA assumes the demand delivered, <span>\(d\)</span>, is a function of nodal pressure, <span>\(p\)</span>, as follows:
</p>

<p>
\[
d = D \left[ \frac{p - P_{min}}{P_{req} - P_{min}} \right]^{P_{exp}}
\]
</p>
<p>
where <span>\(D\)</span> is the full demand required, 
<span>\(P_{min}\)</span> is the pressure below which demand is zero,
<span>\(P_{req}\)</span> is the pressure required to deliver the full required demand
and <span>\(P_{exp}\)</span> is an exponent.
The units of the pressures are psi (US) or meters (SI).
When <span>\(p &lt; P_{min}\)</span> demand is 0 and when
<span>\(p &gt; P_{req}\)</span> demand equals <span>\(D\)</span>.
The default value is <strong>DDA</strong>.
</p>

> 选择DEMAND MODEL是DDA，还是PDA

<p><strong>MINIMUM PRESSURE</strong> specifies the value for <span>\(P_{min}\)</span>. Default value is <code>0.0</code>.</p>
<p><strong>REQUIRED PRESSURE</strong> specifies the value for <span>\(P_{req}\)</span>. Default value is <code>0.1</code>.</p>
<p><strong>PRESSURE EXPONENT</strong> specifies the value for <span>\(P_{exp}\)</span>. Default value is <code>0.5</code>.</p>
<p>
<strong>EMITTER EXPONENT</strong> specifies the power to which the pressure at a junction is raised
when computing the flow issuing from an emitter. The default is `0.5`.
</p>

**MAP** is used to supply the name of a file containing coordinates of the network's nodes
so that a map of the network can be drawn.
It is not used for any hydraulic or water quality computations.

**TOLERANCE** is the difference in water quality level
below which one can say that one parcel of water is essentially the same as another.
The default is `0.01` for all types of quality analyses (chemical, age (measured in hours),
or source tracing (measured in percent)).

**Remarks**:

- All options assume their default values if not explicitly specified in this section.
- Items offset by slashes (`/`) indicate allowable choices.

**Example**:

```html
[OPTIONS]
UNITS        CFS
HEADLOSS     D-W
QUALITY      TRACE   Tank23
UNBALANCED   CONTINUE   10
```

### TIMES

Defines various time step parameters used in the simulation.

**Format**:

<table>
<tbody>
<tr>
  <th class="w3-center">DURATION</th>
  <td>Value (units)</td>
</tr>
<tr>
  <th>HYDRAULIC TIMESTEP</th>
  <td>Value (units)</td>
</tr>
<tr>
  <th>QUALITY TIMESTEP</th>
  <td>Value (units)</td>
</tr>
<tr>
  <th>RULE TIMESTEP</th>
  <td>Value (units)</td>
</tr>
<tr>
  <th>PATTERN TIMESTEP</th>
  <td>Value (units)</td>
</tr>
<tr>
  <th>PATTERN START</th>
  <td>Value (units)</td>
</tr>
<tr>
  <th>REPORT TIMESTEP</th>
  <td>Value (units)</td>
</tr>
<tr>
  <th>REPORT START</th>
  <td>Value (units)</td>
</tr>
<tr>
  <th>START CLOCKTIME</th>
  <td>Value (AM/PM)</td>
</tr>
<tr>
  <th>STATISTIC</th>
  <td>NONE/AVERAGED/MINIMUM/MAXIMUM/RANGE</td>
</tr>
</tbody>
</table>

```text
         ┌─── total ────┼─── DURATION
         │
         │              ┌─── hydraulic ───┼─── HYDRAULIC TIMESTEP
         │              │
         ├─── input ────┼─── quality ─────┼─── QUALITY TIMESTEP
         │              │
         │              │                 ┌─── PATTERN TIMESTEP
         │              └─── pattern ─────┤
         │                                └─── PATTERN START
TIMES ───┤
         │              ┌─── START CLOCKTIME
         ├─── solve ────┤
         │              └─── RULE TIMESTEP
         │
         │                                ┌─── REPORT TIMESTEP
         │              ┌─── report ──────┤
         │              │                 └─── REPORT START
         │              │
         └─── output ───┤                 ┌─── NONE
                        │                 │
                        │                 ├─── AVERAGED
                        │                 │
                        └─── STATISTIC ───┼─── MINIMUM
                                          │
                                          ├─── MAXIMUM
                                          │
                                          └─── RANGE
```

Definitions:

**DURATION** is the duration of the simulation. Use `0` to run a single period snapshot analysis. The default is `0`.

**HYDRAULIC TIMESTEP** determines how often a new hydraulic state of the network is computed.
If greater than either the **PATTERN** or **REPORT** time step it will be automatically reduced.
The default is **1 hour**.

**QUALITY TIMESTEP** is the time step used to track changes in water quality throughout the network.
The default is `1/10` of the hydraulic time step.

**RULE TIMESTEP** is the time step used to check for changes in system status due to activation of rule-based controls
between hydraulic time steps.
The default is `1/10` of the hydraulic time step.

**PATTERN TIMESTEP** is the interval between time periods in all time patterns. The default is **1 hour**.

**PATTERN START** is the time offset at which all patterns will start.
For example, a value of 6 hours would start the simulation with each pattern in the time period
that corresponds to hour 6.
The default is `0`.

**REPORT TIMESTEP** sets the time interval between which output results are reported. The default is 1 hour.

**REPORT START** is the length of time into the simulation at which output results begin to be reported.
The default is `0`.

**START CLOCKTIME** is the time of day (e.g., 3:00 PM) at which the simulation begins.
The default is 12:00 AM midnight.

**STATISTIC** determines what kind of statistical post-processing should be done
on the time series of simulation results generated.
**AVERAGED** reports a set of time-averaged results, 
**MINIMUM** reports only the minimum values, 
**MAXIMUM** the maximum values,
and **RANGE** reports the difference between the minimum and maximum values.
**NONE** reports the full time series for all quantities for all nodes and links and is the default.

**Remarks**:

- Units can be **SECONDS** (**SEC**), **MINUTES** (**MIN**), **HOURS**, or **DAYS**. The default is hours.
- If units are not supplied, then time values can be entered as `decimal hours` or in `hours:minutes` notation.
- All entries in the `[TIMES]` section are optional. Items offset by slashes (`/`) indicate allowable choices.

**Example**:

```text
[TIMES]
DURATION           240 HOURS
QUALITY TIMESTEP   3 MIN
REPORT START       120
STATISTIC          AVERAGED
START CLOCKTIME    6:00 AM
```


## Network Map/Tags

### BACKDROP

Identifies a backdrop image and dimensions for the network map.

**Format**:

- `DIMENSIONS`: `LLx LLy URx URy`
- `UNITS`: `FEET`/`METERS`/`DEGREES`/`NONE`
- `FILE`: `filename`
- `OFFSET`: `X Y`

**Definitions**:

**DIMENSIONS** provides the X and Y coordinates of the lower-left and upper-right corners of the map's bounding rectangle.
Defaults are the extents of the nodal coordinates supplied in the `[COORDINATES]` section.

**UNITS** specifies the units that the map's dimensions are given in. Default is `NONE`.

`FILE` is the name of the file that contains the backdrop image.

**OFFSET** lists the X and Y distance that the upper-left corner of the backdrop image is offset from
the upper-left corner of the map's bounding rectangle. Default is **zero** offset.

**Remarks**:

- The `[BACKDROP]` section is optional and is not used at all when EPANET is run as a console application.
- Only Windows Enhanced Metafiles and bitmap files can be used as backdrops.

### COORDINATES

Assigns map coordinates to network nodes.

**Format**

One line for each node containing:

- Node ID label
- X-coordinate
- Y-coordinate

**Remarks**

- Include one line for each node displayed on the map.
- The coordinates represent the distance from the node to an arbitrary origin at the **lower left of the map**.
  Any convenient units of measure for this distance can be used.
- There is no requirement that all nodes be included in the map, and their locations need not be to actual scale.
- A `[COORDINATES]` section is optional and is not used at all when EPANET is run as a console application.

**Example**

```text
[COORDINATES]
;Node     X-Coord.     Y-Coord
;-------------------------------
  1       10023        128
  2       10056        95
```

## Reference

- [Input File Format](https://epanet22.readthedocs.io/en/latest/back_matter.html#input-file-format)

