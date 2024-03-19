## 概述

[ScriptDaemon](/API/ScriptDaemon/README.md)
是后台运行的服务,例如 [HttpServer](/API/Network/HttpServer/HttpServer/README.md)
, [FloatyWindow](/API/Floaty/FloatyWindow/README.md)
就属于 [ScriptDaemon](/API/ScriptDaemon/README.md)
,只有脚本线程上启动的所有 [HttpServer](/API/Network/HttpServer/HttpServer/README.md) 停止运行获取
[FloatyWindow](/API/Floaty/FloatyWindow/README.md) 关闭脚本线程才有可能停止。