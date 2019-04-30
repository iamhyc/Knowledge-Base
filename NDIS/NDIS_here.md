1. Verifier Tool

   ```
   type `vefifier` in the command line, and verify the driver file in the opend window.
   ```

2. 中间驱动同时具有miniport和protocol的特点

3. 每个网络组件必须有信息(INF)文件，网络类安装器可以用来安装组件。网络INF文件基于通用的INF文件格式

4. Reliable kernel driver

   * validate operations and handlers
   * handle the I/O stack properly

5. **Miniport Drivers**

   A miniport driver manages miniport adapters and provides an interface to the adapters for higher-level drivers.

   **Protocol Drivers**

   A protocol driver provides high-level services in a driver stack.

   A protocol driver binds to underlying miniport adapters.

   A *upper-level* protocol driver implements an interface.

   **Filter Drivers**

   A filter driver filters information on the interface between protocol drivers and miniport drivers.

   Filter drivers can implement modifying or monitoring filters.

   **Intermediate Drivers**

   An intermediate driver interfaces between upper-level protocol drivers and miniport drivers.

6. The NDIS direct OID request interface is mandatory for NDIS 6.20

7. Code

   ```c
   #pragma NDIS_INIT_FUNCTION(DriverEntry)
   mem_ops: NdisZeroMemory, NdisMoveMemory
   lock_ops: FILTER_ACQUIRE_LOCK, FILTER_RELEASE_LOCK

   ```

   DriverEntry (->FnHookRegist) --> FilterAttach (TrackReceives, TrackSneds) -->

8. Status

   FilterInitialized, FilterPausing, FilterPaused, FilterRunning, FilterRestrating, FilterDetaching

9. OID Object

   *Object Identifier* is used to perform the following tasks:

   * Set or retrieve a CAPICOM name and display name for the OID
   * Set of retrieve the dotted number for the OID
   * `FriendlyName`, `Name`, `Value`

10. NBL, aka, Net Buffer Lists

11. NDIS总是按照过滤驱动调用NdisFSendNetBufferLists提交的顺序传递给下层驱动,但是回返FilterSendNetBufferListsComplete 的顺序则是任意的。

    Filter Driver可以请求一个回环发送请求,只要把NdisFSendNetBufferLists的SendFlags设置成NDIS_SEND_FLAGS_CHECK_FOR_LOOPBACK就行了。

    NDIS会引发一个包含发送数据的接收包指示。

12. NDIS Filter Send NBL Hook

    FilterSendNetBufferLists函数: 

    * Filter Driver不能改变其它驱动传来的NET_BUFFER_LIST结构中的SourceHandle成员的值
    * Filter可以在发送前修改缓冲区的内容, 可以像处理自己引发的发送请求的缓冲区一样处理这个缓冲区
    * 调用 NdisFSendNetBufferListsComplete 拒绝传递这个包 
    * 拷贝缓冲区并引发一个发送请求, 类似自己引发一个发送请求,但必须先调用`NdisFSendNetBufferComplete`返回上层驱动的缓冲区

13. ​

    ​







