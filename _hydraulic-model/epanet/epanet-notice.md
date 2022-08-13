---
title:  "EPANET：注意事项"
sequence: 9
---

## Distance

An import point to remember when calculating distances is that
Epanet will not take into account the altitude of junctions
but treats it as a **flat surface**.

In the image below, Epanet would calculate the length of the pipes A, B and C as 500m,
although more pipe would be needed to reach the point 100m higher than the horizontal.
The overall pipe requirement will not change dramatically but remember to order an additional 10%.

{:refdef: style="text-align: center;"}
![](/assets/image/hydraulic-model/epanet/epanet-flat-surface.png)
{: refdef}





