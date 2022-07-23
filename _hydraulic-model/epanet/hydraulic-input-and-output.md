---
title:  "EPANET: Hydraulic 输入和输出"
sequence: 003
---

## Node

### Junction

The basic input data required for junctions are:

- Elevation above some reference (usually mean sea level)
- Water demand (rate of withdrawal from the network)
- Initial water quality

The output results computed for junctions at all time periods of a simulation are:

- Hydraulic head (internal energy per unit weight of fluid)
- Pressure
- Water quality

## Link

### pipe

The principal hydraulic input parameters for pipes are:

- Start and end nodes
- Diameter
- Length
- Roughness coefficient (for determining headloss)
- Status (open, closed, or contains a check valve)

Computed outputs for pipes include:

- Flow rate
- Velocity
- Headloss
- Darcy-Weisbach friction factor

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>输出数据</p>
    <p>
        注意：flow rate表示流量（单位：\(m^{3}/s\)），velocity表示流速（单位：\(m/s\)）。
    </p>
</div>

