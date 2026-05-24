### 系统架构图

```mermaid
graph TD
    subgraph AWS Cloud
        subgraph EC2_A [EC2 实例 A]
            Java_API[Java 进程: 订单 API]
        end
        subgraph EC2_B [EC2 实例 B]
            Worker[Payment Worker]
        end
    end
    Worker -->|HTTP REST API| Java_API
