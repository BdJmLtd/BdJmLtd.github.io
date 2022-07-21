---
title:  "EPANET: Input File Format"
categories: hydraulic
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
**The network map and tags sections**（上表当中的第四列） are not used by command line EPANET
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
- Status (OPEN, CLOSED, or CV)

**Remarks**

- Roughness coefficient is unitless for the Hazen-Williams and Chezy-Manning head loss formulas and has units of millifeet (mm) for the Darcy-Weisbach formula. Choice of head loss formula is supplied in the [OPTIONS] section.
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

## Network Map/Tags

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

