---
title:  "EPANET: Measurement Units"
sequence: 004
---

## Measurement Units

The toolkit can use data expressed in either US Customary of SI Metric units.

<p class="w3-light-grey w3-round-large">
在EPANET中，提供了两组计量单位：US Customary units 和 SI Metric units
</p>

---

**A project's unit system depends on the unit system used for its choice of flow units.**

<p class="w3-light-grey w3-round-large">
根据选择的flow units，来决定使用哪一组计量单位：US Customary units 和 SI Metric units
</p>

---

Flow units in **liters** or **cubic meters** implies that **SI metric units** are used for
all other quantities in addition to flow.
Otherwise US Customary units are employed.

<p class="w3-light-grey w3-round-large">
在flow units中，选择了带有liter或cubic meter的单位，就表示选择了SI metric units。
</p>

---

If the `EN_open` function is used to supply data to a project from an Input File
then its **flow units** are set in the `[OPTIONS]` section of the file.
If the `EN_init` function is used to initialize a project
then the choice of flow units is the fourth argument to the function.

如何选择flow units呢？有两个方法与flow units相关。

- 第一个是`EN_open`方法，它会读取INP文件中的`[OPTIONS]`部分；
- 第二个是`EN_init`方法，当使用`EN_SAVE_AND_INIT`参数（第4个值），会重新初始化flow units。

### Hydraulics

<table>
    <thead>
    <tr>
        <th class="w3-center">Parameter</th>
        <th class="w3-center">US Customary</th>
        <th class="w3-center">SI Metric</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td class="w3-center">Demand</td>
        <td class="w3-center">(see Flow units)</td>
        <td class="w3-center">(see Flow units)</td>
    </tr>
    <tr>
        <td class="w3-center">Diameter (Pipes)</td>
        <td class="w3-center">inches</td>
        <td class="w3-center">millimeters</td>
    </tr>
    <tr>
        <td class="w3-center">Diameter (Tanks)</td>
        <td class="w3-center">feet</td>
        <td class="w3-center">meters</td>
    </tr>
    <tr>
        <td class="w3-center">Efficiency</td>
        <td class="w3-center">percent</td>
        <td class="w3-center">percent</td>
    </tr>
    <tr>
        <td class="w3-center">Elevation</td>
        <td class="w3-center">feet</td>
        <td class="w3-center">meters</td>
    </tr>
    <tr>
        <td class="w3-center">Emitter Coefficient</td>
        <td class="w3-center">flow unit/ (psi)<sup>1/2</sup></td>
        <td class="w3-center">flow unit/ (meter)<sup>1/2</sup></td>
    </tr>
    <tr>
        <td class="w3-center">Energy</td>
        <td class="w3-center">kwatt - hours</td>
        <td class="w3-center">kwatt - hours</td>
    </tr>
    <tr>
        <td class="w3-center" rowspan="5">Flow</td>
        <td class="w3-center">CFS (cubic feet / sec)</td>
        <td class="w3-center">LPS (liters / sec)</td>
    </tr>
    <tr>
        <td class="w3-center">GPM (gallons / min)</td>
        <td class="w3-center">LPM (liters / min)</td>
    </tr>
    <tr>
        <td class="w3-center">MGD (million gal / day)</td>
        <td class="w3-center">MLD (megaliters / day) </td>
    </tr>
    <tr>
        <td class="w3-center">IMGD (Imperial MGD)</td>
        <td class="w3-center"><b>CMH (cubic meters / hr)</b></td>
    </tr>
    <tr>
        <td class="w3-center">AFD (acre-feet / day)</td>
        <td class="w3-center">CMD (cubic meters / day)</td>
    </tr>
    <tr>
        <td class="w3-center">Friction Factor</td>
        <td class="w3-center">unitless</td>
        <td class="w3-center">unitless</td>
    </tr>
    <tr>
        <td class="w3-center">Head</td>
        <td class="w3-center">feet</td>
        <td class="w3-center">meters</td>
    </tr>
    <tr>
        <td class="w3-center">Length</td>
        <td class="w3-center">feet</td>
        <td class="w3-center">meters</td>
    </tr>
    <tr>
        <td class="w3-center">Minor Loss Coefficient</td>
        <td class="w3-center">unitless</td>
        <td class="w3-center">unitless</td>
    </tr>
    <tr>
        <td class="w3-center">Power</td>
        <td class="w3-center">horsepower</td>
        <td class="w3-center">kwatts</td>
    </tr>
    <tr>
        <td class="w3-center">Pressure</td>
        <td class="w3-center">psi</td>
        <td class="w3-center">meters</td>
    </tr>
    <tr>
        <td class="w3-center">Roughness Coefficient</td>
        <td class="w3-center">millifeet (Darcy-Weisbach) unitless otherwise</td>
        <td class="w3-center">mm (Darcy-Weisbach) unitless otherwise</td>
    </tr>
    <tr>
        <td class="w3-center">Velocity</td>
        <td class="w3-center">ft/sec</td>
        <td class="w3-center">meters/sec</td>
    </tr>
    <tr>
        <td class="w3-center">Volume</td>
        <td class="w3-center">cubic feet</td>
        <td class="w3-center">cubic meters</td>
    </tr>
    </tbody>
</table>

- psi: pounds per square inch

### Water Quality

<table>
    <thead>
    <tr>
        <th class="w3-center">Parameter</th>
        <th class="w3-center">US Customary</th>
        <th class="w3-center">SI Metric</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td class="w3-center">Concentration</td>
        <td class="w3-center">mg/L or ug/L</td>
        <td class="w3-center">mg/L or ug/L</td>
    </tr>
    <tr>
        <td class="w3-center">Reaction Coefficient (Bulk)</td>
        <td class="w3-center">1/day (1st-order)</td>
        <td class="w3-center">1/day (1st-order)</td>
    </tr>
    <tr>
        <td class="w3-center" rowspan="2">Reaction Coefficient (Wall)</td>
        <td class="w3-center">mass/sq-ft/day (0-order)</td>
        <td class="w3-center">mass/sq-m/day (0-order)</td>
    </tr>
    <tr>
        <td class="w3-center">ft/day (1st-order)</td>
        <td class="w3-center">meters/day (1st-order)</td>
    </tr>
    <tr>
        <td class="w3-center">Source Mass Injection</td>
        <td class="w3-center">mass/minute</td>
        <td class="w3-center">mass/minute</td>
    </tr>
    <tr>
        <td class="w3-center">Water Age</td>
        <td class="w3-center">hours</td>
        <td class="w3-center">hours</td>
    </tr>
    </tbody>
</table>


