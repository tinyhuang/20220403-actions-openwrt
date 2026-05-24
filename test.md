graph TD
    %% 这是一段开发者注释：本图用于说明订单模块与支付模块的内部调用链路
    %% 下方定义外层基础设施结构
    subgraph AWS Cloud
        subgraph EC2_A [EC2 实例 A: 核心服务]
            Java_API[Java 进程: 订单 API<br/>监听端口: 8080]
        end
        
        subgraph EC2_B [EC2 实例 B: 异步任务]
            Worker[Payment Worker<br/>监听端口: 9090]
        end
    end

    %% 下方定义数据请求链路（带步骤、方法、路径和说明）
    Worker -- "1. POST /api/orders<br/>(发起订单结算请求)" --> Java_API
    
    %% 使用虚线 (-.->) 表示响应返回
    Java_API -.->|"2. HTTP 200 OK<br/>(返回包含 OrderID 的 JSON 结果)"| Worker
