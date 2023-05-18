---
title: "水力模型：翟老师版本"
sequence: "011"
---

## 源码

- 水力模型前端代码 [fe-anqing](http://36.138.170.6:8929/gis/aq/aq_latest/fe-anqing)
- 水力模型后端代码 [be-anqing](http://36.138.170.6:8929/gis/aq/aq_latest/be-anqing)

其中，`fe` 表示 Front End（前端），`be` 表示 Back End（后端）。

## 前端代码

切换到 `dev` 分支，水力模型的相关文件路径：

```text
src/page/model
```

## 后端代码

切换到 `dev` 分支。

Java 后台定时运行上边表里数据生成 `.inp` 文件，通过调用 `SimulateAutoServiceImpl` 类实现，
并调用 Python 水力模型服务的 `/file` 接口上传 `.inp` 文件，然后继续调用 `/epanet/simulate` 接口运行模型，
返回结果保存到 `water_node_result` 和 `water_link_result`，其中，

- `water_node_result` 重点关注 `pressure`（压力计算值）、`real_value`（压力实测时）和 `real_time` 预测时间；
- `water_link_result` 重点关注 `flow`（流量计算值）、 `real_value`（流量实测时）和 `real_time`（预测时间）。

### SimulateAutoServiceImpl

```java
@Configuration
public class SimulateAutoServiceImpl implements SimulateAutoService {
    @Override
    @Scheduled(cron = "0 0 0 * * ?")
    public void epanetAutoSimulate() {
        waterResultService.epanetAutoSimulate( tempWaterLayerManager,waterPointManager, waterServerManager,
                junctionInfoManager, reservoirManager, tankManager, pumpManager,
                valveManager, pointManager, curveManager, curveLineManager, waterTimeManager,
                dictManager, waterPatternManager, waterPatternDetailManager, waterEnergyManager,
                waterReactionsManager, resultManager, restTemplateService,
                waterHydraulicManager, waterQualityManager, redisTemplate, waterLinkManager);
    }
}
```

### WaterResultServiceImpl

```java
@Service
public class WaterResultServiceImpl implements WaterResultService {
     @Override
    public void epanetAutoSimulate(TempWaterLayerManager tempWaterLayerManager,
                                   WaterPointManager waterPointManager,
                                   SetWaterServerManager waterServerManager,
                                   WaterJunctionInfoManager junctionInfoManager,
                                   WaterReservoirManager reservoirManager,
                                   WaterTankManager tankManager,
                                   WaterPumpManager pumpManager,
                                   WaterValveManager valveManager,
                                   WaterPointManager pointManager,
                                   WaterCurveManager curveManager,
                                   WaterCurveLineManager curveLineManager,
                                   WaterTimeManager waterTimeManager,
                                   WaterDictManager dictManager,
                                   WaterPatternManager waterPatternManager,
                                   WaterPatternDetailManager waterPatternDetailManager,
                                   WaterEnergyManager waterEnergyManager,
                                   WaterReactionsManager waterReactionsManager,
                                   WaterResultManager resultManager,
                                   RestTemplateService restTemplateService,
                                   WaterHydraulicManager waterHydraulicManager,
                                   WaterQualityManager waterQualityManager,
                                   RedisTemplate<String, Object> redisTemplate,
                                   WaterLinkManager waterLinkManager) {
         // ...

         // 生成 INP 文件
         String fileName = inpFileService.inpFileWrite(junctionList,rservoirList,tankList,
                 linkList,pumpList,valveList,curves,waterTimeVO,publicWaterPattern,patterns,
                 waterOptionsVO,waterEnergyVO,waterReactions);
         
         // 上传 INP 文件到 Python 实现的水力模型
         File inpFile = new File(fileName);
         System.out.println("fileName:"+fileName);
         InpFileUpdateDTO updateDTO = restTemplateService.upload(simulatePath+"/file",inpFile);

         // 从水力模型中获取计算结果
         Map<String,Object> paramMap=new HashMap<>();
         paramMap.put("path",updateDTO.getResult());
         EpanetResultResponseDTO resultData = restTemplateService.post(simulatePath+"/epanet/simulate",paramMap);

         // ...
     }
}
```

### InpFileServiceImpl

`com.gyhl.basic.waterModule.service.impl.InpFileServiceImpl` 类中的 `fileContetStr` 方法是用来生成 `.inp` 文件内容：

```java
@Service
public class InpFileServiceImpl implements InpFileService {
    @Override
    public String inpFileWrite(List<WaterJunctionInfoDTO> junctions, List<WaterReservoirDTO> reservoirs,
                               List<WaterTankDTO> tanks, List<WaterLinkDTO> links, List<WaterPumpDTO> pumps,
                               List<WaterValveDTO> valves, List<WaterCurveDTO> curves,
                               WaterTimeVO waterTime,WaterPatternDTO publicWaterPattern,
                               List<WaterPatternDTO> waterPatterns, WaterOptionsVO waterOptionsVO,
                               WaterEnergyVO waterEnergyVO, WaterReactionsVO waterReactionsVO) {
        // ...

        String str = this.fileContetStr(junctions,reservoirs,tanks,links,pumps,valves,curves,waterTime,
                publicWaterPattern,waterPatterns,waterOptionsVO,waterEnergyVO,waterReactionsVO);
        
        // ...
    }
    
   private String fileContetStr(List<WaterJunctionInfoDTO> junctions, List<WaterReservoirDTO> reservoirs,
                                List<WaterTankDTO> tanks, List<WaterLinkDTO> links,
                                List<WaterPumpDTO> pumps, List<WaterValveDTO> valves, List<WaterCurveDTO> curves,
                                WaterTimeVO waterTime, WaterPatternDTO publicWaterPattern,
                                List<WaterPatternDTO> waterPatterns, WaterOptionsVO waterOptionsVO,
                                WaterEnergyVO waterEnergyVO, WaterReactionsVO waterReactionsVO){
        StringBuffer sb = new StringBuffer();
        sb.append("[TITLE]\n\n\n");
        //节点
        //节点坐标
        StringBuffer coordinatesb = new StringBuffer();
        coordinatesb.append("\n\n[COORDINATES]\n");
        coordinatesb.append(";Node            \tX-Coord         \tY-Coord");
        //节点
        sb.append("[JUNCTIONS]\n;ID              \tElev        \tDemand      \tPattern         ");
        if(junctions!=null){
            for(WaterJunctionInfoDTO junction:junctions){
                sb.append("\n");
                sb.append(" "+getFormatStr(junction.getJunctionId()+"",16));
                sb.append(getFormatStr(junction.getElevation()+"",12));
                sb.append(getFormatStr(junction.getDemand()+"",12));
                if(junction.getPatternId()!=null){
                    sb.append(getFormatStr(junction.getPatternId()+"",16));
                }else if(publicWaterPattern!=null){
//                    sb.append(getFormatStr(publicWaterPattern.getId()+"",16));
                    sb.append(getFormatStr("",16));
                }
                sb.append(";");
                coordinatesb.append("\n");
                coordinatesb.append(" "+getFormatStr(junction.getJunctionId()+"",16));
                coordinatesb.append(getFormatStr(junction.getX()+"",16));
                coordinatesb.append(getFormatStr(junction.getY()+"",16));
            }
        }
        //水库
        sb.append("\n\n[RESERVOIRS]\n");
        sb.append(";ID              \tHead        \tPattern         ");
        if(reservoirs!=null){
            for(WaterReservoirDTO reservoir:reservoirs){
                sb.append("\n");
                sb.append(" "+getFormatStr(reservoir.getReservoirId()+"",16));
                sb.append(getFormatStr(reservoir.getTotalHead()+"",12));
                if(reservoir.getHeadPattern()!=null){
                    sb.append(getFormatStr(reservoir.getHeadPattern()+"",16));
                }else if(publicWaterPattern!=null){
//                    sb.append(getFormatStr(publicWaterPattern.getId()+"",16));
                    sb.append(getFormatStr("",16));
                }
                sb.append(";");
                coordinatesb.append("\n");
                coordinatesb.append(" "+getFormatStr(reservoir.getReservoirId()+"",16));
                coordinatesb.append(getFormatStr(reservoir.getX()+"",16));
                coordinatesb.append(getFormatStr(reservoir.getY()+"",16));
            }
        }
        //水池
        sb.append("\n\n[TANKS]\n");
        sb.append(";ID              \tElevation   \tInitLevel   \tMinLevel    \tMaxLevel    \tDiameter    \tMinVol      \tVolCurve");
        if(tanks!=null){
            for(WaterTankDTO tank:tanks){
                sb.append("\n");
                sb.append(" "+getFormatStr(tank.getTankId()+"",16));
                sb.append(getFormatStr(tank.getElevation()+"",12));
                sb.append(getFormatStr(tank.getInitialLevel()+"",12));
                sb.append(getFormatStr(tank.getMinLevel()+"",12));
                sb.append(getFormatStr(tank.getMaxLevel()+"",12));
                sb.append(getFormatStr(tank.getMaxLevel()+"",12));
                sb.append(getFormatStr("",12));
                sb.append(getFormatStr("",8));
                sb.append(";");
                coordinatesb.append("\n");
                coordinatesb.append(" "+getFormatStr(tank.getTankId()+"",16));
                coordinatesb.append(getFormatStr(tank.getX()+"",16));
                coordinatesb.append(getFormatStr(tank.getY()+"",16));
            }
        }
        //管线
        sb.append("\n\n[PIPES]\n");
        sb.append(";ID              \tNode1           \tNode2           \tLength      \tDiameter    \tRoughness   \tMinorLoss   \tStatus");
        if(links!=null){
            for(WaterLinkDTO link:links){
                sb.append("\n");
                sb.append(" "+getFormatStr(link.getPipeId()+"",16));
                sb.append(getFormatStr(link.getStartId()+"",16));
                sb.append(getFormatStr(link.getEndId()+"",16));
                sb.append(getFormatStr(link.getLength()+"",12));
                sb.append(getFormatStr(link.getPipeDiameter()+"",12));
                sb.append(getFormatStr(link.getRoughness()+"",12));
                if(!StringUtil.isNullOrEmpty(link.getMinorLoss().trim())){
                    sb.append(getFormatStr(link.getMinorLoss()+"",12));
                }else{
                    sb.append(getFormatStr("0.0",12));
                }

                String statusName = link.getStatusName();
                if("在用".equals(statusName)){
                    sb.append(getFormatStr("OPEN",6));
                }else {
                    sb.append(getFormatStr("OPEN",6));
                }
                sb.append(";");
            }
        }
        //水泵
        sb.append("\n\n[PUMPS]\n");
        sb.append(";ID              \tNode1           \tNode2           \tParameters");
        if(pumps!=null){
            for(WaterPumpDTO pump:pumps){
                sb.append("\n");
                sb.append(" "+getFormatStr(pump.getPumpId()+"",16));
                sb.append(getFormatStr(pump.getStartId()+"",16));
                sb.append(getFormatStr(pump.getEndId()+"",16));
                sb.append(getFormatStr("HEAD "+pump.getCurveId(),0));
                sb.append(";");
            }
        }
        //阀门
        sb.append("\n\n[VALVES]\n");
        sb.append(";ID              \tNode1           \tNode2           \tDiameter    \tType\tSetting     \tMinorLoss");
        if(valves!=null){
            for(WaterValveDTO valve:valves){
                sb.append("\n");
                sb.append(" "+getFormatStr(valve.getValveId()+"",16));
                sb.append(getFormatStr(valve.getStartId()+"",16));
                sb.append(getFormatStr(valve.getEndId()+"",16));
                sb.append(getFormatStr(valve.getDiameter()+"",12));
                sb.append(getFormatStr(valve.getType()+"",4));
                sb.append(getFormatStr(valve.getSetting()+"",12));
                sb.append(getFormatStr(valve.getMinorLoss()+"",9));
                sb.append(";");
            }
        }
        //标签
        sb.append("\n\n[TAGS]\n");
        //
        sb.append("\n\n[DEMANDS]\n");
        sb.append(";Junction        \tDemand      \tPattern         \tCategory");
        //
        sb.append("\n\n[STATUS]\n");
        sb.append(";ID              \tStatus/Setting");
        //模式
        sb.append("\n\n[PATTERNS]\n");
        sb.append(";ID              \tMultipliers");
        sb.append("\n;");
        if(waterPatterns!= null){
            for(WaterPatternDTO pattern:waterPatterns){
                List<WaterPatternDetailDTO> patternDetailList = pattern.getDetailList();
                if(patternDetailList!=null&&patternDetailList.size()>0){
                    for(int i=0;i<patternDetailList.size();i++){
                        WaterPatternDetailDTO patternDetail = patternDetailList.get(i);
                        if(i%4==0){
                            sb.append("\n ");
                            sb.append(pattern.getId());
                            sb.append("               \t");
                        }
                        sb.append(patternDetail.getValue());
                        sb.append("         \t");
                    }
                }
            }
        }
//        sb.append(" 1               \t0.5         \t1.3         \t1.0         \t1.2 ");
        //曲线
        sb.append("\n\n[CURVES]\n");
        sb.append(";ID              \tX-Value     \tY-Value");
        if(curves!=null){
            for(WaterCurveDTO curve:curves){
                sb.append("\n");
                sb.append(";");
                sb.append(curve.getTypeValue());
                sb.append("\n");
                sb.append(" "+getFormatStr(curve.getId()+"",16));
                List<WaterCurveLineDTO> curveLines = curve.getCurveLines();
                if(curveLines!=null){
                    for(WaterCurveLineDTO curveLine:curveLines){
                        sb.append(getFormatStr(curveLine.getX()+"",12));
                        sb.append(getFormatStr(curveLine.getY()+"",12));
                        sb.append("\n");
                    }
                }
            }
        }
        //
        sb.append("\n\n[CONTROLS]\n");
        //
        sb.append("\n\n[RULES]\n");
        //能量
        sb.append("\n\n[ENERGY]\n");
        if(waterEnergyVO!=null){
            sb.append("\n Global Efficiency  \t");
            sb.append(waterEnergyVO.getGlobalEfficiency());
            sb.append("\n Global Price       \t");
            sb.append(waterEnergyVO.getGlobalPrice());
            sb.append("\n Demand Charge      \t");
            sb.append(waterEnergyVO.getDemandCharge());
        }
        //
        sb.append("\n\n[EMITTERS]\n");
        sb.append(";Junction        \tCoefficient");
        //
        sb.append("\n\n[QUALITY]\n");
        sb.append(";Node            \tInitQual");
        //
        sb.append("\n\n[SOURCES]\n");
        sb.append(";Node            \tType        \tQuality     \tPattern");
        //反应
        sb.append("\n\n[REACTIONS]\n");
        sb.append(";Type     \tPipe/Tank       \tCoefficient");
        //反应
        sb.append("\n\n[REACTIONS]\n");
        if(waterReactionsVO!=null){
            sb.append(" Order Bulk            \t");
            sb.append(waterReactionsVO.getOrderBulk());
            sb.append("\n");
            sb.append(" Order Tank            \t");
            sb.append(waterReactionsVO.getOrderTank());
            sb.append("\n");
            sb.append(" Order Wall            \t");
            sb.append(waterReactionsVO.getOrderWallValue());
            sb.append("\n");
            sb.append(" Global Bulk            \t");
            sb.append(waterReactionsVO.getGlobalBulk());
            sb.append("\n");
            sb.append(" Global Wall            \t");
            sb.append(waterReactionsVO.getGlobalWall());
            sb.append("\n");
            sb.append(" Limiting Potential            \t");
            sb.append(waterReactionsVO.getLimitingPotential());
            sb.append("\n");
            sb.append(" Roughness Correlation            \t");
            sb.append(waterReactionsVO.getRoughnessCorrelation());
        }
        //
        sb.append("\n\n[MIXING]\n");
        sb.append(";Tank            \tModel");
        //时间
        sb.append("\n\n[TIMES]\n");
        if(waterTime!=null){
            sb.append(" Duration           \t");
            sb.append(waterTime.getDuration());
            sb.append("\n");
            sb.append(" Hydraulic Timestep \t");
            sb.append(TimeUtil.millisecond2Hour(waterTime.getHydraulicTimestep()));
            sb.append("\n");
            sb.append(" Quality Timestep   \t");
            sb.append(TimeUtil.millisecond2Hour(waterTime.getQualityTimestep()));
            sb.append("\n");
            sb.append(" Pattern Timestep   \t");
            sb.append(TimeUtil.millisecond2Hour(waterTime.getPatternTimestep()));
            sb.append("\n");
            sb.append(" Pattern Start      \t");
            sb.append(TimeUtil.millisecond2Hour(waterTime.getPaternStart()));
            sb.append("\n");
            sb.append(" Report Timestep    \t");
            sb.append(TimeUtil.millisecond2Hour(waterTime.getReportTimestep()));
            sb.append("\n");
            sb.append(" Report Start       \t");
            sb.append(TimeUtil.millisecond2Hour(waterTime.getReportStart()));
            sb.append("\n");
//            sb.append(" Start ClockTime    \t");
//            sb.append(waterTime.getStartClockTime());
//            sb.append(" am\n");
            sb.append(" Statistic          \t");
            sb.append(waterTime.getStatisticValue());
        }else {
            sb.append(" Duration           \t0\n");
            sb.append(" Hydraulic Timestep \t1:00\n");
            sb.append(" Quality Timestep   \t0:05\n");
            sb.append(" Pattern Timestep   \t6:00\n");
            sb.append(" Pattern Start      \t0:00\n");
            sb.append(" Report Timestep    \t1:00\n");
            sb.append(" Report Start       \t0:00\n");
            sb.append(" Start ClockTime    \t12 am\n");
            sb.append(" Statistic          \tNone");
        }
        //
        sb.append("\n\n[REPORT]\n");
        sb.append(" Status             \tNo\n");
        sb.append(" Summary            \tNo\n");
        sb.append(" Page               \t0\n");
        //水力设置
        sb.append("\n\n[OPTIONS]\n");
        sb.append(" Units              \t");
        sb.append(waterOptionsVO.getUnitsValue());
        sb.append("\n");
        sb.append(" Headloss           \t");
        sb.append(waterOptionsVO.getHeadlossValue());
        sb.append("\n");
        sb.append(" Specific Gravity   \t");
        sb.append(waterOptionsVO.getSpecificGravity());
        sb.append("\n");
        sb.append(" Viscosity          \t");
        sb.append(waterOptionsVO.getViscosity());
        sb.append("\n");
        sb.append(" Trials             \t");
        sb.append(waterOptionsVO.getTrials());
        sb.append("\n");
        sb.append(" Accuracy           \t");
        sb.append(waterOptionsVO.getAccuracy());
        sb.append("\n");
        sb.append(" CHECKFREQ          \t");
        sb.append(waterOptionsVO.getCheckfreq());
        sb.append("\n");
        sb.append(" MAXCHECK           \t");
        sb.append(waterOptionsVO.getMaxcheck());
        sb.append("\n");
        sb.append(" DAMPLIMIT          \t");
        sb.append(waterOptionsVO.getDamplimit());
        sb.append("\n");
        sb.append(" Unbalanced         \t");
        sb.append(waterOptionsVO.getUnbalancedValue());
        sb.append("\n");
        sb.append(" Pattern            \t");
        sb.append(waterOptionsVO.getPattern());
        sb.append("\n");
        sb.append(" Demand Multiplier  \t");
        sb.append(waterOptionsVO.getDemandMultiplier());
        sb.append("\n");
        sb.append(" Emitter Exponent   \t");
        sb.append(waterOptionsVO.getEmitterExponent());
        sb.append("\n");
        sb.append(" Quality            \t");
        if(waterOptionsVO.getQuality()!=null&&!waterOptionsVO.getQuality().equals("无")){
            sb.append("lv"+waterOptionsVO.getQualityUnitsValue());
        }else {
            sb.append("none");
        }
        sb.append("\n");
        sb.append(" Diffusivity        \t");
        sb.append(waterOptionsVO.getDiffusivity());
        sb.append("\n");
        sb.append(" Tolerance          \t");
        sb.append(waterOptionsVO.getTolerance());
        //
        sb.append(coordinatesb.toString());

        /**
        //
        sb.append("\n\n[VERTICES]\n");
        sb.append(";Link            \tX-Coord         \tY-Coord");
        //
        sb.append("\n\n[LABELS]\n");
        sb.append(";X-Coord           Y-Coord          Label & Anchor Node");
        //
        sb.append("\n\n[BACKDROP]\n");
        sb.append(" DIMENSIONS     \t0.00            \t0.00            \t10000.00        \t10000.00        \n");
        sb.append(" UNITS          \tNone\n");
        sb.append(" FILE           \t\n");
        sb.append(" OFFSET         \t0.00            \t0.00            ");
         **/
        //
        sb.append("\n\n[END]");
        return  sb.toString();
    }
}
```

