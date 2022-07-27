---
title:  "EPANET: Warning And Error Codes"
sequence: 006
---

需要注意`224`错误：No tanks or reservoirs in network。

## Warning Codes

<table>
    <thead>
    <tr>
        <th class="w3-center">Code</th>
        <th class="w3-center">Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td class="w3-center">1</td>
        <td>
            System hydraulically unbalanced - convergence to a hydraulic solution
            was not achieved in the allowed number of trials 
        </td>
    </tr>
    <tr>
        <td class="w3-center">2</td>
        <td>System may be hydraulically unstable - hydraulic convergence was only achieved after the status of all links was held fixed</td>
    </tr>
    <tr>
        <td class="w3-center">3</td>
        <td>System disconnected - one or more nodes with positive demands were disconnected from all supply sources</td>
    </tr>
    <tr>
        <td class="w3-center">4</td>
        <td>Pumps cannot deliver enough flow or head - one or more pumps were forced to either shut down (due to insufficient head) or operate beyond the maximum rated flow </td>
    </tr>
    <tr>
        <td class="w3-center">5</td>
        <td>Valves cannot deliver enough flow - one or more flow control valves could not deliver the required flow even when fully open </td>
    </tr>
    <tr>
        <td class="w3-center">6</td>
        <td>System has negative pressures - negative pressures occurred at one or more junctions with positive demand</td>
    </tr>
    </tbody>
</table>

## Error Codes

<table>
    <thead>
    <tr>
        <th class="w3-center">Code</th>
        <th class="w3-center">Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td class="w3-center">0</td>
        <td>No error </td>
    </tr>
    <tr>
        <td class="w3-center">101</td>
        <td>Insufficient memory available </td>
    </tr>
    <tr>
        <td class="w3-center">102</td>
        <td>No network data available </td>
    </tr>
    <tr>
        <td class="w3-center">103</td>
        <td>Hydraulic solver not opened </td>
    </tr>
    <tr>
        <td class="w3-center">104</td>
        <td>No hydraulics for water quality analysis </td>
    </tr>
    <tr>
        <td class="w3-center">105</td>
        <td>Water quality solver not opened</td>
    </tr>
    <tr>
        <td class="w3-center">106</td>
        <td>No results saved to report on</td>
    </tr>
    <tr>
        <td class="w3-center">107</td>
        <td>Hydraulics supplied from external file </td>
    </tr>
    <tr>
        <td class="w3-center">108</td>
        <td>Cannot use external file while hydraulics solver is open </td>
    </tr>
    <tr>
        <td class="w3-center">110</td>
        <td>Cannot solve network hydraulic equations </td>
    </tr>
    <tr>
        <td class="w3-center">120</td>
        <td>Cannot solve water quality transport equations </td>
    </tr>
    </tbody>
</table>

<table>
    <thead>
    <tr>
        <th class="w3-center">Code</th>
        <th class="w3-center">Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td class="w3-center">200</td>
        <td>One or more errors in an input file</td>
    </tr>
    <tr>
        <td class="w3-center">201</td>
        <td>Syntax error</td>
    </tr>
    <tr>
        <td class="w3-center">202</td>
        <td>Function call contains an illegal numeric value</td>
    </tr>
    <tr>
        <td class="w3-center">203</td>
        <td>Function call refers to an undefined node</td>
    </tr>
    <tr>
        <td class="w3-center">204</td>
        <td>Function call refers to an undefined link </td>
    </tr>
    <tr>
        <td class="w3-center">205</td>
        <td>Function call refers to an undefined time pattern </td>
    </tr>
    <tr>
        <td class="w3-center">206</td>
        <td>Function call refers to an undefined curve </td>
    </tr>
    <tr>
        <td class="w3-center">207</td>
        <td>Function call attempts to control a check valve pipe or a GPV valve </td>
    </tr>
    <tr>
        <td class="w3-center">208</td>
        <td>Function call contains illegal PDA pressure limits</td>
    </tr>
    <tr>
        <td class="w3-center">209</td>
        <td>Function call contains an illegal node property value </td>
    </tr>
    <tr>
        <td class="w3-center">211</td>
        <td>Function call contains an illegal link property value </td>
    </tr>
    <tr>
        <td class="w3-center">212</td>
        <td>Function call refers to an undefined Trace Node </td>
    </tr>
    <tr>
        <td class="w3-center">213</td>
        <td>Function call contains an invalid option value </td>
    </tr>
    <tr>
        <td class="w3-center">214</td>
        <td>Too many characters in a line of an input file </td>
    </tr>
    <tr>
        <td class="w3-center">215</td>
        <td>Function call contains a duplicate ID label </td>
    </tr>
    <tr>
        <td class="w3-center">216</td>
        <td>Function call refers to an undefined pump </td>
    </tr>
    <tr>
        <td class="w3-center">217</td>
        <td>Invalid pump energy data </td>
    </tr>
    <tr>
        <td class="w3-center">219</td>
        <td>Illegal valve connection to tank node </td>
    </tr>
    <tr>
        <td class="w3-center">220</td>
        <td>Illegal valve connection to another valve </td>
    </tr>
    <tr>
        <td class="w3-center">221</td>
        <td>Mis-placed clause in rule-based control </td>
    </tr>
    <tr>
        <td class="w3-center">222</td>
        <td>Link assigned same start and end nodes </td>
    </tr>
    <tr>
        <td class="w3-center">223</td>
        <td>Not enough nodes in network </td>
    </tr>
    <tr>
        <td class="w3-center">224</td>
        <td>No tanks or reservoirs in network </td>
    </tr>
    <tr>
        <td class="w3-center">225</td>
        <td>Invalid lower/upper levels for tank </td>
    </tr>
    <tr>
        <td class="w3-center">226</td>
        <td>No head curve or power rating for pump</td>
    </tr>
    <tr>
        <td class="w3-center">227</td>
        <td>Invalid head curve for pump </td>
    </tr>
    <tr>
        <td class="w3-center">230</td>
        <td>Nonincreasing x-values for curve </td>
    </tr>
    <tr>
        <td class="w3-center">240</td>
        <td>Function call refers to nonexistent water quality source </td>
    </tr>
    <tr>
        <td class="w3-center">241</td>
        <td>Function call refers to nonexistent control </td>
    </tr>
    <tr>
        <td class="w3-center">250</td>
        <td>Function call contains invalid format (e.g. too long an ID name) </td>
    </tr>
    <tr>
        <td class="w3-center">251</td>
        <td>Function call contains invalid parameter code </td>
    </tr>
    <tr>
        <td class="w3-center">253</td>
        <td>Function call refers to nonexistent demand category </td>
    </tr>
    <tr>
        <td class="w3-center">254</td>
        <td>Function call refers to node with no coordinates </td>
    </tr>
    <tr>
        <td class="w3-center">257</td>
        <td>Function call refers to nonexistent rule </td>
    </tr>
    <tr>
        <td class="w3-center">258</td>
        <td>Function call refers to nonexistent rule clause </td>
    </tr>
    <tr>
        <td class="w3-center">259</td>
        <td>Function call attempts to delete a node that still has links connected to it </td>
    </tr>
    <tr>
        <td class="w3-center">260</td>
        <td>Function call attempts to delete node assigned as a Trace Node </td>
    </tr>
    <tr>
        <td class="w3-center">261</td>
        <td>Function call attempts to delete a node or link contained in a control </td>
    </tr>
    <tr>
        <td class="w3-center">262</td>
        <td>Function call attempts to modify network structure while a solver is open </td>
    </tr>
    </tbody>
</table>

<table>
    <thead>
    <tr>
        <th class="w3-center">Code</th>
        <th class="w3-center">Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td class="w3-center">301</td>
        <td>Identical file names used for different types of files </td>
    </tr>
    <tr>
        <td class="w3-center">302</td>
        <td>Cannot open input file </td>
    </tr>
    <tr>
        <td class="w3-center">303</td>
        <td>Cannot open report file </td>
    </tr>
    <tr>
        <td class="w3-center">304</td>
        <td>Cannot open output file </td>
    </tr>
    <tr>
        <td class="w3-center">305</td>
        <td>Cannot open hydraulics file </td>
    </tr>
    <tr>
        <td class="w3-center">306</td>
        <td>Hydraulics file does not match network data </td>
    </tr>
    <tr>
        <td class="w3-center">307</td>
        <td>Cannot read hydraulics file </td>
    </tr>
    <tr>
        <td class="w3-center">308</td>
        <td>Cannot save results to binary file </td>
    </tr>
    <tr>
        <td class="w3-center">309</td>
        <td>Cannot save results to report file </td>
    </tr>
    </tbody>
</table>

