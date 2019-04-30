### VLC Hrbrid Mode Uplink Problem

1. uplink with ***RF broadcast*** or ***RF Routing*** ?

2. Wi-Fi + VLC ***binding*** AP, or, ***seperated*** with extra wire communication?
   * If binding, the uplink would occupy an extran RF channel, at a very close distance, as VLC coordinator; May interference with another RF uplink

3. We know that: for LTE UE, when initialized, it requests a ***PDN-link***, and P-GW would allocate an IP adress for UE and tell UE the ***IP address over PDN-link***

   (PDN Connectivity Request --> Session Resuqet(proxy) )

   so, there is analogy that we: allocate IP from the top-level switch for VLC UE, ***at the VLC coordinator***; and tell VLC UE the ***IP address over VLC-link***;


### VLC Hybrid Mode Uplink Design

1. 如何确定Frame的长度，应为多少个slot？
2. beacon或前导码如何选择？（应参考GSM/LTE的TDMA规范）
3. 同步所需要的精准时钟，就靠FPGA了！