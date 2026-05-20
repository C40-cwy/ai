# 微博舆情信息爬取与多维度分析系统 v1.0

一个基于 Python 的微博数据爬取与分析系统，支持热搜榜单爬取、关键词搜索、评论采集、用户画像分析等功能。

## 🌟 功能特性

### 核心功能
- **微博热搜爬取**：自动获取微博全站热搜榜单
- **关键词搜索**：支持自定义关键词搜索微博内容
- **评论采集**：深度采集博文评论数据
- **用户画像**：获取博主和评论者的详细用户信息
- **数据存储**：将采集数据保存到 Excel 文件
- **多维度分析**：情感分析、文本分析、时间分析、用户分析
- **可视化图表**：自动生成数据可视化报告

### 技术优势
- **智能Cookie管理**：首次登录后自动保存并复用Cookies
- **浏览器自动化**：使用 Selenium 模拟浏览器操作
- **数据去重**：自动检测重复数据，避免重复存储
- **异常处理**：完善的错误处理和日志记录
- **性能优化**：支持缓存机制，提高爬取效率

## 📁 项目结构

```
practice06/
├── main.py                    # 命令行入口
├── main_gui.py                # GUI界面入口
├── config.py                  # 配置文件
├── spider/                    # 爬虫模块
│   ├── weibo_spider.py        # 微博爬虫核心
│   ├── comment_spider.py      # 评论爬虫
│   ├── cookie_manager.py      # Cookie管理
│   └── browser_user_fetcher.py # 浏览器用户信息获取
├── store/                     # 数据存储模块
│   └── excel_writer.py        # Excel文件写入
├── analysis/                  # 数据分析模块
│   ├── sentiment_analysis.py  # 情感分析
│   ├── text_analysis.py       # 文本分析
│   ├── time_analysis.py       # 时间分析
│   └── user_analysis.py       # 用户分析
├── visual/                    # 可视化模块
│   └── chart_generator.py     # 图表生成
├── utils/                     # 工具模块
│   ├── logger.py              # 日志管理
│   └── crawl_utils.py         # 爬取工具
├── data/                      # 数据文件目录
├── cookies/                   # Cookies存储目录
├── logs/                      # 日志文件目录
└── output_html/               # 可视化输出目录
```

## 🛠️ 安装环境

### 依赖安装

```bash
pip install -r requirements.txt
```

### 依赖列表
- `selenium` - 浏览器自动化
- `pandas` - 数据处理
- `openpyxl` - Excel文件操作
- `requests` - HTTP请求
- `beautifulsoup4` - HTML解析
- `matplotlib` - 数据可视化
- `snownlp` - 中文情感分析
- `wordcloud` - 词云生成

### 浏览器驱动

本项目使用 Microsoft Edge 浏览器，请确保已安装 Edge 浏览器，并下载对应版本的 [EdgeDriver](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)。

## 🚀 使用方法

### 方法一：命令行模式

```bash
python main.py
```

运行后按照提示操作：
1. 选择爬取模式（热搜榜单/关键词搜索）
2. 输入爬取页数（关键词搜索模式）
3. 选择是否采集评论数据
4. 选择是否采集用户信息

### 方法二：图形界面模式

```bash
python main_gui.py
```

打开 GUI 界面后：
1. 输入搜索关键词
2. 设置爬取页数
3. 点击「开始爬取」按钮
4. 实时查看爬取进度

## 📊 数据结构

### 博文数据 (posts)

| 字段 | 类型 | 说明 |
|------|------|------|
| id | string | 博文ID |
| content | string | 博文内容 |
| publish_time | string | 发布时间 |
| source | string | 来源 |
| topics | string | 话题标签 |
| like_count | int | 点赞数 |
| comment_count | int | 评论数 |
| repost_count | int | 转发数 |
| user_id | string | 博主ID |
| user_name | string | 博主昵称 |
| user_followers | int | 博主粉丝数 |
| user_verified | bool | 博主认证状态 |
| user_verified_type | string | 博主认证类型 |
| region | string | 博主地区 |
| url | string | 博文链接 |

### 评论数据 (comments)

| 字段 | 类型 | 说明 |
|------|------|------|
| id | string | 评论ID |
| post_id | string | 所属博文ID |
| content | string | 评论内容 |
| comment_time | string | 评论时间 |
| like_count | int | 评论点赞数 |
| user_id | string | 评论者ID |
| user_name | string | 评论者昵称 |
| reply_to | string | 回复目标 |

### 用户数据 (users)

| 字段 | 类型 | 说明 |
|------|------|------|
| user_id | string | 用户ID |
| user_name | string | 用户昵称 |
| gender | string | 性别 |
| region | string | 地区 |
| followers_count | int | 粉丝数 |
| following_count | int | 关注数 |
| weibo_count | int | 微博数 |
| verified | bool | 认证状态 |
| verified_type | string | 认证类型 |
| description | string | 个人简介 |

## 📈 分析功能

### 情感分析
- 对博文和评论进行情感倾向判断（正面/负面/中性）
- 统计情感分布情况

### 文本分析
- 关键词提取
- 词云生成
- 文本相似度分析

### 时间分析
- 发布时间分布
- 活跃度趋势分析

### 用户分析
- 用户画像分析
- 粉丝分布统计
- 认证用户比例

## 🔧 配置说明

### config.py 主要配置

```python
# 浏览器配置
BROWSER_TYPE = 'Edge'
DRIVER_PATH = './msedgedriver.exe'

# 爬取配置
MAX_PAGES = 10
MAX_COMMENTS = 500
HUMAN_DELAY = (0.5, 1.5)

# 输出配置
OUTPUT_DIR = './data'
LOG_DIR = './logs'
```

## 📝 日志说明

系统会自动记录运行日志到 `logs/` 目录：
- `weibo_spider.log` - 爬虫日志
- `weibo_crawler.log` - 爬取日志
- `error.log` - 错误日志

## ⚠️ 注意事项

1. **登录要求**：首次运行需要登录微博账号，后续会自动复用Cookies
2. **频率限制**：请合理控制爬取频率，避免触发微博反爬机制
3. **数据安全**：Cookies文件包含登录信息，请妥善保管
4. **网络环境**：建议在稳定的网络环境下运行
5. **浏览器版本**：请保持浏览器和驱动版本一致




---

