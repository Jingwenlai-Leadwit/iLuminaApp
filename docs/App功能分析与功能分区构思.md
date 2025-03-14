# App功能分析与功能分区构思

这是一个集成了眼部健康检测和门店管理功能的Android平板应用，主要面向两类用户：
1. **美容顾问**：主要使用眼部检测相关功能，为顾客提供眼部健康检测服务
2. **店长**：除了可以使用眼部检测功能外，还能使用门店管理功能

## 核心功能模块

### 1. 用户角色与权限管理
- **登录系统**：支持不同角色（店长、美容顾问）登录
- **权限控制**：根据角色显示不同功能模块
- **账号管理**：个人信息维护和账号切换

### 2. 眼部健康检测（所有角色可用）
- **客户选择/创建**：通过电话号码快速查找或创建客户
- **问卷调查**：9题OSDI干眼问卷填写
- **图像采集**：引导用户完成眼周图像拍摄
- **AI分析**：分析眼周图像，生成评估结果
- **五维度评分**：疲劳度、浑浊度、脆弱度、松弛度、老化度
- **结果展示**：多维度展示检测结果，支持点击查看详情
- **方案推荐**：基于检测结果推荐产品和护理方案

### 3. 客户管理（所有角色可用，但在不同位置访问）
- **客户档案**：管理客户基本信息
- **检测历史**：查看客户历次检测记录
- **购买记录**：记录客户产品购买情况
- **客户标签**：为客户添加分类标签
- **客户跟进**：记录客户沟通和服务情况

### 4. 服务管理（所有角色可用）
- **服务展示**：展示所有服务项目和套餐
- **服务详情**：查看服务流程、适用人群和价格
- **服务案例**：展示服务前后对比效果
- **服务推荐**：向客户推荐适合的服务

### 5. 门店管理（仅店长可用）
- **数据看板**：展示门店核心业务指标
- **员工管理**：管理门店员工账号和权限
- **业绩统计**：查看门店销售和检测数据
- **库存管理**：管理产品库存情况
- **活动管理**：设置和管理门店营销活动

## 功能整合与分区构思

根据最新的界面布局，美睛美科App的功能分区如下：

```
美睛美科App 业务功能区布局构思
├── 公共区域
│   └── 底部导航栏（首页/服务/检测/报告/我的）
├── 首页
│   ├── 门店活动轮播
│   ├── 热门服务展示
│   └── 服务案例展示
├── 服务
│   ├── 服务分类（眼部护理/眼部检测/套餐推荐）
│   ├── 服务详情
│   └── 服务案例
├── 检测
│   ├── 客户选择/创建
│   ├── 问卷调查（9题评估）
│   ├── 图像采集
│   ├── 结果展示（五维度雷达图）
│   │   ├── 维度详情（点击各维度查看）
│   │   ├── 检测详情（AI分析结果）
│   │   └── 检测报告（综合评估）
│   └── 方案推荐
├── 报告
│   ├── 当前检测用户的完整报告详情（含问卷、AI检测对比、详情、推荐方案等）
└── 我的（根据角色显示不同内容）
    ├── 登录界面（角色选择）
    ├── 美容顾问视图
    │   ├── 个人信息
    │   ├── 业绩数据
    │   ├── 今日数据
    │   └── 功能中心（检测记录/客户管理/预约管理等）
    |   ├── 客户区域
    |   │   ├── 客户分类
    |   │   ├── 客户列表
    |   │   └── 客户详情
    |   │       ├── 基本信息
    |   │       ├── 检测记录
    |   │       └── 消费记录
    └── 店长视图
        ├── 个人信息
        ├── 门店业绩
        ├── 今日数据
        └── 功能中心（门店管理/员工管理/客户管理等）
```

## 用户角色与权限系统

### 美容顾问角色
- **可访问功能**：
  - 首页：查看门店活动、热门服务和服务案例
  - 服务：查看所有服务项目和详情
  - 检测：执行完整的眼部检测流程
  - 客户：管理自己的客户
  - 我的：查看个人业绩、今日数据和功能中心
- **权限限制**：
  - 只能查看自己的客户和业绩数据
  - 无法访问门店管理、员工管理等功能
  - 无法修改系统设置和服务内容

### 店长角色
- **可访问功能**：
  - 美容顾问的所有功能
  - 门店管理：查看门店概览、员工业绩和库存预警
  - 员工管理：管理员工账号和权限
  - 数据分析：查看详细的业绩报表和转化分析
  - 活动管理：设置和管理门店营销活动
- **额外权限**：
  - 可查看所有员工的客户和业绩数据
  - 可修改系统设置和服务内容
  - 可导出数据报表

## 眼部检测流程详解

眼部检测是系统的核心功能，完整流程如下：

1. **客户选择/创建**
   - 通过电话号码快速查找客户
   - 若为新客户，创建客户档案
   - 若为老客户，调用历史数据

2. **问卷调查**
   - 填写9题专业问卷
   - 评估眼睛异物感、不适感、电子设备使用等情况
   - 问卷结果作为AI分析的辅助数据

3. **图像采集**
   - 环境光检测，确保光线适合拍摄
   - 引导客户将眼部对准指示框
   - 拍摄清晰的眼周图像
   - 图像质量评估，确保分析准确性

4. **AI分析处理**
   - 图像预处理，提取关键特征
   - 结合问卷数据进行综合分析
   - 生成五维度评分和综合评分

5. **结果展示**
   - 显示综合评分和健康等级
   - 五维度雷达图展示（疲劳度、浑浊度、脆弱度、松弛度、老化度）
   - 支持点击各维度查看详情
   - 支持查看AI分析的图像对比和详细结果

6. **方案推荐**
   - 基于检测结果推荐个性化方案
   - 提供基础、标准、高级三个级别的方案
   - 展示预期效果和价格

## 交互设计特点

1. **多入口设计**
   - 检测功能可从多个入口进入（底部导航栏、首页热门服务、客户详情页）
   - 根据入口不同，可能跳过某些步骤（如已选择客户）

2. **深度交互**
   - 五维度雷达图支持点击交互，查看各维度详情
   - 检测结果支持多层级展示，从概览到详情
   - 图像对比功能，直观展示AI分析结果

3. **数据隐私保护**
   - 今日数据和客户信息集中在"我的"页面，减少信息泄露风险
   - 根据角色显示不同级别的数据，确保信息安全

4. **一致性体验**
   - 核心功能（如检测）对所有角色保持一致体验
   - 统一的设计语言和交互模式，降低学习成本


