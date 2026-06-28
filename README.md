<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=30&duration=3000&pause=1000&color=F57C00&center=true&vCenter=true&width=500&lines=%F0%9F%91%8B+Hi%2C+I'm+Keisumhuis;%E4%B8%80%E5%90%8D+C%2B%2B+%E5%90%8E%E7%AB%AF%E5%BC%80%E5%8F%91%E5%B7%A5%E7%A8%8B%E5%B8%88;Keep+Coding%2C+Stay+Crazy+%F0%9F%94%A5" alt="Typing SVG" />
</p>

<p align="center">
  <a href="https://github.com/Keisumhuis/crazy">
    <img src="https://img.shields.io/badge/%F0%9F%9A%80_crazy-v1.0.2-FF6F00?style=flat-square" />
  </a>
  <a href="https://github.com/Keisumhuis/crazy/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-brightgreen?style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/C%2B%2B-17-00599C?style=flat-square&logo=cplusplus" />
  <img src="https://img.shields.io/badge/CMake-3.15%2B-064F8C?style=flat-square&logo=cmake" />
  <img src="https://img.shields.io/badge/Platform-Win_%7C_Linux-808080?style=flat-square" />
</p>

---

### 🧠 关于我

一名 C++ 后端开发工程师，专注于高性能服务端框架、网络编程和并发模型。热爱底层技术，追求代码的简洁与高效。

- 🔭 正在维护 [**crazy**](https://github.com/Keisumhuis/crazy) — 一个轻量级 C++17 基础框架库
- 🌱 持续学习：分布式系统、Linux 内核、性能优化
- 💬 欢迎交流：C++ 后台开发、网络编程、系统设计
- 📫 联系我：keisumhuis@qq.com

---

### 🚀 核心项目：crazy

> 轻量级 C++ 基础框架库，提供 Actor 模型、网络通信、日志、配置、加密、MySQL 等常用功能模块。

| 模块 | 说明 |
| :--- | :--- |
| 🎭 Actor 模型 | 消息驱动的并发模型，独立线程 + 消息队列，支持命令行向指定 Actor 发消息 |
| 🌐 网络通信 | TCP 服务端/客户端、Socket 封装、Selector 多路复用（wepoll）、本地 Socket |
| 📝 日志系统 | 多级别日志（trace ~ fatal），支持自定义格式器和输出目标 |
| ⚙️ 配置管理 | INI 格式配置文件解析，支持 int/string/boolean 多类型读取 |
| 🔐 加密模块 | Base64 编解码、MD5 哈希 |
| 🗄️ MySQL | 连接池、预处理语句、完善的异常体系 |
| 🗺️ 内存映射 | 跨平台 mmap 文件映射与 mmap_vector 容器 |
| 📦 JSON | 序列化/反序列化，支持 STL 容器和自定义类型 |
| 🧵 线程工具 | 线程池、原子锁、条件互斥锁、文件锁、MVCC 锁 |
| 🪞 反射 | `REFLECTION(...)` 宏一行搞定序列化，自动生成二进制协议和 JSON 序列化代码 |
| 🔧 基础工具 | DateTime、UUID、URI、Buffer、Singleton、KeyValuePair、命令行解析 |

#### ✨ 亮点特性：反射宏

```cpp
#include "crazy.h"

struct UserInfo {
    std::string name;
    int32_t age;
    double score;
    std::vector<std::string> tags;
    REFLECTION(name, age, score, tags);  // 一行搞定序列化，最多支持 60 个字段
};

UserInfo user{"kesium", 25, 99.5, {"c++", "gamedev"}};

// 序列化到二进制协议
std::string bin = crazy::protocol::Converter::Serializable(user);

// 反序列化
UserInfo user2 = crazy::protocol::Converter::Deserializable<UserInfo>(bin);

// 序列化到 JSON
crazy::json::Serialise jsonSer;
user.to_json(jsonSer);
// → {"name":"kesium","age":25,"score":99.5,"tags":["c++","gamedev"]}
```

#### ✨ Actor 模型 + 命令行交互

```cpp
class MyActor : public crazy::ActorInterface {
    using crazy::ActorInterface::ActorInterface;
    std::map<std::string, std::string> helps() override {
        return {{"query", "查询数据"}, {"clear", "清除缓存"}};
    }
    void handleCommandLineMessgaBase(
        crazy::MessageBase::ptr req, crazy::MessageBase::ptr rsp) override {
        auto cmds = crazy::StringUtil::Split(req->getData());
        if ("query" == cmds[0]) rsp->setData("result: ok");
        else if ("clear" == cmds[0]) rsp->setData("cleared");
    }
};

int main(int argc, char** argv) {
    crazy::Application app(argc, argv);
    app.registerActor<MyActor>("my_actor");
    app.exec();
}
```

```bash
# 终端 A：启动服务
$ ./exe

# 终端 B：向指定 Actor 发送命令
$ ./exe -s my_actor@query
# → result: ok

$ ./exe -s my_actor@clear
# → cleared
```

---

### 🛠️ 技术栈

<p align="center">
  <img src="https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" />
  <img src="https://img.shields.io/badge/CMake-064F8C?style=for-the-badge&logo=cmake&logoColor=white" />
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" />
  <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" />
  <img src="https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white" />
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white" />
  <img src="https://img.shields.io/badge/VS_Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white" />
</p>

<p align="center">
  <img src="https://quotes-github-readme.vercel.app/api?type=horizontal&theme=gruvbox" />
</p>