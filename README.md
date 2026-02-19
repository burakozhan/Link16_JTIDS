# Link16 Communication System

## Project Overview

The Link16 communication system is a complete tactical datalink communication system implementation, including message processing, encoding and encryption, physical layer processing, and simulation capabilities. This system supports the Link16 standard message format and provides a complete implementation from the application layer to the physical layer. The system uses the cross-platform CMake build system and can run on various operating systems such as Windows, Linux, and macOS.

## Features

- **Message processing**: Supports the J-series message format of the Link16 standard, including header words, start words, extension words, and continuation words.
- **Encoding and Encryption**: Implements Reed-Solomon encoding, AES encryption, parity checking, and interleaving functions.
- **Physical layer processing**: Supports USRP hardware interface, multiple modulation methods (BPSK, QPSK), frequency hopping, and synchronization.
- **Simulation Functionality**: Provides end-to-end wireless link simulation, including AWGN and Rayleigh fading channel models, as well as bit error rate and throughput calculations.


## Project Structure

```
link16/                                # 项目根目录
├── src/                               # 源代码目录
│   ├── api/                           # API实现
│   │   ├── Link16.cpp                 # 主API实现
│   │   ├── MessageAPI.cpp             # 消息API实现
│   │   ├── CodingAPI.cpp              # 编码API实现
│   │   ├── PhysicalAPI.cpp            # 物理层API实现
│   │   └── SimulationAPI.cpp          # 仿真API实现
│   │
│   ├── application/                   # 应用层
│   │   ├── main.cpp                   # 主程序入口
│   │   ├── Link16System.h             # 系统集成类
│   │   ├── Link16System.cpp           # 系统集成类实现
│   │   ├── real/                      # 实际通信模式
│   │   │   ├── Link16App.h            # 实际通信应用类
│   │   │   └── Link16App.cpp          # 实际通信应用实现
│   │   └── simulation/                # 仿真模式
│   │       ├── SimulationApp.h        # 仿真应用类
│   │       └── SimulationApp.cpp      # 仿真应用实现
│   │
│   ├── core/                          # 核心功能
│   │   ├── types/                     # 基本数据类型
│   │   │   ├── dataType.h             # 数据类型定义
│   │   │   └── Link16Types.h          # Link16特定类型定义
│   │   │
│   │   ├── config/                    # 配置相关
│   │   │   ├── global.h               # 全局变量和常量
│   │   │   ├── global.cpp             # 全局变量实现
│   │   │   ├── SystemConfig.h         # 系统配置
│   │   │   └── SystemConfig.cpp       # 系统配置实现
│   │   │
│   │   └── utils/                     # 通用工具
│   │       ├── tools.h                # 通用工具函数
│   │       ├── tools.cpp              # 通用工具实现
│   │       ├── fileUtils.h            # 文件操作工具
│   │       ├── fileUtils.cpp          # 文件操作实现
│   │       ├── logger.h               # 日志工具
│   │       ├── logger.cpp             # 日志实现
│   │       └── platform.h             # 平台相关工具
│   │
│   ├── protocol/                      # 协议层
│   │   ├── message/                   # 消息处理
│   │   │   ├── word/                  # 字处理
│   │   │   │   ├── Word.hpp           # 基类
│   │   │   │   ├── Word.cpp           # 基类实现
│   │   │   │   ├── HeaderWord.h       # 报头字
│   │   │   │   ├── HeaderWord.cpp     # 报头字实现
│   │   │   │   ├── InitialWord.h      # 初始字
│   │   │   │   ├── InitialWord.cpp    # 初始字实现
│   │   │   │   ├── ExtendWord.h       # 扩展字
│   │   │   │   ├── ExtendWord.cpp     # 扩展字实现
│   │   │   │   ├── ContinueWord.h     # 继续字
│   │   │   │   └── ContinueWord.cpp   # 继续字实现
│   │   │   │
│   │   │   ├── STDPMsg.h              # STDP消息类
│   │   │   └── STDPMsg.cpp            # STDP消息实现
│   │   │
│   │   ├── interface/                 # 协议接口
│   │   │   ├── interface.h            # 消息层接口
│   │   │   └── interface.cpp          # 消息层接口实现
│   │   │
│   │   └── formats/                   # 消息格式定义
│   │       ├── J_Series.h             # J系列消息格式
│   │       └── J_Series.cpp           # J系列消息实现
│   │
│   ├── coding/                        # 编码层
│   │   ├── error_correction/          # 纠错编码
│   │   │   ├── reed_solomon/          # RS编码
│   │   │   │   ├── RSCoder.h          # RS编码器接口
│   │   │   │   └── RSCoder.cpp        # RS编码器实现
│   │   │   │
│   │   │   ├── convolutional/         # 卷积码(预留)
│   │   │   │   ├── ConvolutionalCoder.h
│   │   │   │   └── ConvolutionalCoder.cpp
│   │   │   │
│   │   │   ├── ldpc/                  # LDPC码(预留)
│   │   │   │   ├── LDPCCoder.h
│   │   │   │   └── LDPCCoder.cpp
│   │   │   │
│   │   │   └── turbo/                 # Turbo码(预留)
│   │   │       ├── TurboCoder.h
│   │   │       └── TurboCoder.cpp
│   │   │
│   │   ├── error_detection/           # 错误检测
│   │   │   ├── crc/                   # CRC校验
│   │   │   │   ├── CRCCoder.h         # CRC校验接口
│   │   │   │   └── CRCCoder.cpp       # CRC校验实现
│   │   │   │
│   │   │   └── parity/                # 奇偶校验
│   │   │       ├── BIPCoder.h         # 奇偶校验接口
│   │   │       └── BIPCoder.cpp       # 奇偶校验实现
│   │   │
│   │   ├── crypto/                    # 加密
│   │   │   ├── symmetric/             # 对称加密
│   │   │   │   ├── aes/               # AES加密
│   │   │   │   │   ├── AES.h          # AES加密接口
│   │   │   │   │   └── AES.cpp        # AES加密实现
│   │   │   │   │
│   │   │   │   └── des/               # DES加密(预留)
│   │   │   │       ├── DES.h
│   │   │   │       └── DES.cpp
│   │   │   │
│   │   │   └── hash/                  # 哈希函数
│   │   │       ├── md5/               # MD5哈希
│   │   │       │   ├── md5.h          # MD5哈希接口
│   │   │       │   └── md5.cpp        # MD5哈希实现
│   │   │       │
│   │   │       └── sha/               # SHA哈希(预留)
│   │   │           ├── SHA.h
│   │   │           └── SHA.cpp
│   │   │
│   │   └── interleaving/              # 交织
│   │       ├── matrix/                # 矩阵交织
│   │       │   ├── MatrixInterleaver.h
│   │       │   └── MatrixInterleaver.cpp
│   │       │
│   │       └── block/                 # 块交织(预留)
│   │           ├── BlockInterleaver.h
│   │           └── BlockInterleaver.cpp
│   │
│   ├── physical/                      # Physical layer
│   │   ├── hardware/                  # Hardware interface
│   │   │   ├── usrp/                  # USRP hardware
│   │   │   │   ├── USRPInterface.h    # USRP Core Interface
│   │   │   │   ├── USRPInterface.cpp
│   │   │   │   ├── USRPTransmitter.h  # USRP Transmitter
│   │   │   │   ├── USRPTransmitter.cpp
│   │   │   │   ├── USRPReceiver.h     # USRP Receiver
│   │   │   │   └── USRPReceiver.cpp
│   │   │   │
│   │   │   └── sdr/                   # Other SDR hardware (reserved)
│   │   │       ├── SDRInterface.h
│   │   │       └── SDRInterface.cpp
│   │   │
│   │   ├── modulation/                # modulation and demodulation
│   │   │   ├── digital/               # 数字调制
│   │   │   │   ├── PSK/               # 相移键控
│   │   │   │   │   ├── BPSKModulator.h
│   │   │   │   │   ├── BPSKModulator.cpp
│   │   │   │   │   ├── QPSKModulator.h
│   │   │   │   │   └── QPSKModulator.cpp
│   │   │   │   │
│   │   │   │   ├── FSK/               # 频移键控
│   │   │   │   │   ├── FSKModulator.h
│   │   │   │   │   └── FSKModulator.cpp
│   │   │   │   │
│   │   │   │   └── QAM/               # 正交幅度调制
│   │   │   │       ├── QAMModulator.h
│   │   │   │       └── QAMModulator.cpp
│   │   │   │
│   │   │   └── analog/                # 模拟调制(预留)
│   │   │       ├── AMModulator.h
│   │   │       └── AMModulator.cpp
│   │   │
│   │   ├── frequency/                 # 频率管理
│   │   │   ├── hopping/               # 跳频
│   │   │   │   ├── FrequencyHopping.h
│   │   │   │   └── FrequencyHopping.cpp
│   │   │   │
│   │   │   └── management/            # 频率管理
│   │   │       ├── FrequencyManager.h
│   │   │       └── FrequencyManager.cpp
│   │   │
│   │   └── synchronization/           # 同步
│   │       ├── time/                  # 时间同步
│   │       │   ├── TimeSynchronizer.h
│   │       │   └── TimeSynchronizer.cpp
│   │       │
│   │       └── frame/                 # 帧同步
│   │           ├── FrameSynchronizer.h
│   │           └── FrameSynchronizer.cpp
│   │
│   └── simulation/                    # 仿真模块
│       ├── EndToEndSimulation.h       # 端到端仿真接口
│       ├── EndToEndSimulation.cpp     # 端到端仿真实现
│       │
│       ├── channel/                   # 信道模型
│       │   ├── base/                  # 基础信道模型
│       │   │   ├── ChannelModel.h     # 信道模型基类
│       │   │   └── ChannelModel.cpp
│       │   │
│       │   ├── awgn/                  # 加性高斯白噪声信道
│       │   │   ├── AWGNChannel.h
│       │   │   └── AWGNChannel.cpp
│       │   │
│       │   └── fading/                # 衰落信道
│       │       ├── RayleighChannel.h  # 瑞利衰落
│       │       └── RayleighChannel.cpp
│       │
│       ├── metrics/                   # 性能指标
│       │   ├── BER.h                  # 误码率
│       │   ├── BER.cpp
│       │   ├── Throughput.h           # 吞吐量
│       │   └── Throughput.cpp
│       │
│       └── engine/                    # 仿真引擎
│           ├── SimulationEngine.h     # 仿真引擎核心
│           ├── SimulationEngine.cpp
│           ├── SimulationConfig.h     # 仿真配置
│           └── SimulationConfig.cpp
│
├── include/                           # 公共头文件
│   └── link16/                        # 对外接口
│       ├── Link16.h                   # 主要API
│       ├── api/                       # API子模块
│       │   ├── MessageAPI.h           # 消息API
│       │   ├── CodingAPI.h            # 编码API
│       │   ├── PhysicalAPI.h          # 物理层API
│       │   └── SimulationAPI.h        # 仿真API
│       │
│       └── simulation/                # 仿真接口
│           ├── ChannelSimulation.h    # 信道仿真接口
│           └── EndToEndSimulation.h   # 端到端仿真接口
│
├── lib/                               # 第三方库
│   ├── schifra/                       # Schifra库
│   │   ├── schifra_crc.hpp
│   │   ├── schifra_ecc_traits.hpp
│   │   ├── schifra_error_processes.hpp
│   │   ├── schifra_fileio.hpp
│   │   ├── schifra_galois_field.hpp
│   │   ├── schifra_galois_field_element.hpp
│   │   ├── schifra_galois_field_polynomial.hpp
│   │   ├── schifra_reed_solomon_bitio.hpp
│   │   ├── schifra_reed_solomon_block.hpp
│   │   ├── schifra_reed_solomon_decoder.hpp
│   │   ├── schifra_reed_solomon_encoder.hpp
│   │   └── schifra_sequential_root_generator_polynomial_creator.hpp
│   │
│   ├── uhd/                           # UHD库(USRP硬件驱动)
│   │   └── README.md                  # UHD库说明
│   │
│   └── boost/                         # Boost库(可能用于仿真)
│       └── README.md                  # Boost库说明
│
├── tests/                             # 测试目录
│   ├── unit/                          # 单元测试
│   │   ├── core_tests/                # 核心功能测试
│   │   ├── protocol_tests/            # 协议层测试
│   │   ├── coding_tests/              # 编码层测试
│   │   ├── physical_tests/            # 物理层测试
│   │   └── simulation_tests/          # 仿真模块测试
│   │
│   ├── integration/                   # 集成测试
│   │   ├── end_to_end_tests/          # 端到端测试
│   │   └── performance_tests/         # 性能测试
│   │
│   └── simulation/                    # 仿真测试
│       ├── channel_tests/             # 信道模型测试
│       └── end_to_end_tests/          # 端到端仿真测试
│
├── docs/                              # 文档
│   ├── api/                           # API文档
│   ├── design/                        # 设计文档
│   │   ├── protocol/                  # 协议设计
│   │   ├── coding/                    # 编码设计
│   │   └── physical/                  # 物理层设计
│   │
│   └── examples/                      # 示例
│       ├── basic/                     # 基础示例
│       └── advanced/                  # 高级示例
│
├── scripts/                           # 脚本
│   ├── build/                         # 构建脚本
│   │   ├── build.bat                  # Windows构建脚本
│   │   └── build.sh                   # Linux构建脚本
│   │
│   └── tools/                         # 工具脚本
│       ├── code_format.bat            # 代码格式化脚本
│       └── generate_docs.bat          # 文档生成脚本
│
├── build/                             # 构建输出目录(git忽略)
│   ├── debug/                         # 调试版本
│   └── release/                       # 发布版本
│
├── CMakeLists.txt                     # 主CMake构建文件
├── README.md                          # 项目说明
└── LICENSE                            # 许可证
```

## How to use

### Compilation of Project

#### Windows

```batch
# Use the provided build script
build.bat

# Or build manually
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
cmake --build . --config Release
```

#### Linux/macOS

```bash
# Use the provided build script
./build.sh

# Or build manually
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
cmake --build .
```

### Run the application

```bash
# Windows
build\bin\Release\link16_app.exe

# Linux/macOS
build/bin/link16_app
```

### Generate documentation

```bash
# In the build directory
cmake --build . --target docs
```

### Run tests

```bash
# In the build directory
ctest -C Release
```

## Development Guide

### Project Architecture

This project adopts a layered architecture, from top to bottom as follows:

- **Application layer**: User interface and application logic
- **API Layer**: Provides public APIs, connecting users and internal implementations.
- **Protocol layer**: Handles Link16 message format and protocol
- **Encoding layer**: Implements various encoding, encryption, and interleaving algorithms.
- **Physical layer**: handles modulation, frequency hopping, synchronization, and hardware interfaces.
- **Simulation layer**: Provides end-to-end wireless link simulation

### Add new encoding methods

1. src/coding/error_correction/Create new subdirectories under the current directory .
2. Implement the corresponding encoder interface
3. src/api/CodingAPI.cppAdd support for the new encoder.
4. Update public API interfaceinclude/link16/api/CodingAPI.h

### Add new modulation methods

1. `src/physical/modulation/` Create new subdirectories under the current directory.
2. Implement the corresponding modulator interface
3. Add `src/api/PhysicalAPI.cpp support for new modulators
4. Update public API interface `include/link16/api/PhysicalAPI.h`

### Add a new channel model

1. `src/simulation/channel/` Create new subdirectories under the current directory.
2. Implement the corresponding channel model interface.
3. `src/simulation/engine/SimulationEngine.cpp` Add support for the new channel model.
4. `src/api/SimulationAPI.cpp` Add support for the new channel model.
5. Update public API interface `include/link16/api/SimulationAPI.h`

### Cross-platform development considerations

1. `src/core/utils/platform.h` Platform detection macros and utility functions in use
2. Avoid using platform-specific APIs and path separators.
3. Use standard C++17 features and avoid using compiler-specific extensions.
4. Handling platform differences using CMake's conditional compilation features

## License

[License Information]

(The original project does not have any licence information attached.)
