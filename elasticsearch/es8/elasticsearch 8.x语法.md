# elasticsearch 8.x语法

## 目录

- [1. 基本概念](#1-基本概念)
  - [1.1 索引](#11-索引)
  - [1.2 文档](#12-文档)
  - [1.3 映射](#13-映射)
- [2. 映射管理](#2-映射管理)
  - [2.1 settings管理](#21-settings管理)
  - [2.1.1 settings管理](#211-查看settings)
  - [2.1.2 settings管理](#212-修改settings)
  - [2.2 mappings管理](#22-mappings管理)
  - [2.2.1 mappings管理](#221-查看mappings)
  - [2.2.2 mappings管理](#222-修改mappings)
  - [2.2.3 mappings管理](#223-mappings参数)
  - [2.2.4 mappings管理](#224-字段数据类型)
  - [2.2.5 mappings管理](#225-metadata字段)
- [3. 索引管理](#3-索引管理)
  - [3.1 创建管理](#31-创建索引)  
  - [3.2 删除管理](#32-删除索引)
  - [3.3 查看管理](#33-查看索引)
  - [3.4 检查索引是否存在](#34-检查索引是否存在)
  - [3.5 查看所有索引](#35-查看所有索引)
- [4. 别名管理](#4-别名管理)
  - [4.1 查看别名](#41-查看别名)
  - [4.2 添加别名](#42-添加别名)
  - [4.3 删除别名](#43-删除别名)
  - [4.4 修改别名](#44-修改别名)
  - [4.5 检查别名是否存在](#45-检查别名是否存在)
- [5. 文档管理](#5-文档管理)
  - [5.1 创建文档](#51-创建文档)
  - [5.2 查看文档](#52-查看文档)
  - [5.3 更新文档](#53-更新文档)
  - [5.4 删除文档](#54-删除文档)
  - [5.5 批量操作管理](#55-批量操作管理)
    - [5.5.1 批量管理文档](#551-批量管理文档)
    - [5.5.2 带条件的批量操作管理](#552-带条件的批量操作管理)
  - [5.6 脚本管理](#56-脚本管理)
    - [5.6.1 创建脚本](#561-创建脚本)
    - [5.6.2 查看脚本](#562-查看脚本)
    - [5.6.3 删除脚本](#563-删除脚本)
  - [5.7 重新索引文档](#57-重新索引文档)
  - [5.8 检查文档是否存在](#58-检查文档是否存在)
- [6 查询](#6-查询)
  - [6.1 match all query](#61-match-all-query)
  - [6.2 term-level query](#62-term-level-query)
    - [6.2.1 ids query](#621-ids-query)
    - [6.2.2 term query](#622-term-query)
    - [6.2.3 terms query](#623-terms-query)
    - [6.2.4 terms_set query](#624-terms_set-query)
    - [6.2.5 range query](#625-range-query)
    - [6.2.6 Fuzzy query](#626-fuzzy-query)
    - [6.2.7 prefix query](#627-prefix-query)
    - [6.2.8 wildcard query](#628-wildcard-query)
    - [6.2.9 regexp query](#629-regexp-query)
    - [6.2.10 Exists query](#6210-exists-query)
  - [6.3 full-text query 全文查询](#63-full-text-query-全文查询)
    - [6.3.1 Query_string query](#631-query_string-query)
    - [6.3.2 Simple_query_string query](#632-simple_query_string-query)
    - [6.3.3 Match query](#633-match-query)
    - [6.3.4 Match_phrase query](#634-match_phrase-query)
    - [6.3.5 Multi_match query](#635-multi_match-query)
    - [6.3.6 Combined_fields query 组合字段查询](#636-combined_fields-query-组合字段查询)
    - [6.3.7 intervels query 间隔查询](#637-intervels-query-间隔查询)
  - [6.4 compound query 复合查询](#64-compound-query-复合查询)
    - [6.4.1 bool query](#641-bool-query)
    - [6.4.2 boosting query](#642-boosting-query)
    - [6.4.3 constant_score query](#643-constant_score-query)
    - [6.4.4 dis_max query](#644-dis_max-query)
    - [6.4.5 function_score query](#645-function_score-query)
  - [6.5 span query 跨度查询](#65-span-query-跨度查询)
    - [6.5.1 span_term query](#651-span_term-query)
    - [6.5.2 span_field_masking query](#652-span_field_masking-query)
    - [6.5.3 span_first query](#653-span_first-query)
    - [6.5.4 span_multi query](#654-span_multi-query)
    - [6.5.5 span_near query](#655-span_near-query)
    - [6.5.6 span_not query](#656-span_not-query)
    - [6.5.7 span_or query](#657-span_or-query)
    - [6.5.8 span_containing query](#658-span_containing-query)
    - [6.5.9 span_within query](#659-span_within-query)
  - [6.6 scroll query](#66-scroll-query)
  - [6.7 joining query](#67-joining-query)
    - [6.7.1 nested query](#671-nested-query)
    - [6.7.2 has child query](#672-has-child-query)
    - [6.7.3 has parent query](#673-has-parent-query)
    - [6.7.4 parent id query](#674-parent-id-query)
  - [6.8 特殊查询](#68-特殊查询)
    - [6.8.1 script query](#681-script-query)
  - [6.9 常用查询设置](#69-常用查询设置)
    - [6.9.1 排序字段](#691-排序字段)
    - [6.9.2 查询指定字段](#692-查询指定字段)
    - [6.9.3 分页](#693-分页)
    - [6.9.4 设置查询结果总数](#694-设置查询结果总数)
    - [6.9.5 filter search result 过滤查询结果](#695-filter-search-result-过滤查询结果)
    - [6.9.6 highlighting 高亮查询](#696-highlighting-高亮查询)
    - [6.9.7 inner hits 内部命中](#697-inner-hits-内部命中)
    - [6.9.8 muti search 多索引查询](#698-muti-search-多索引查询)
    - [6.9.9 search template 查询模板](#699-search-template-查询模板)
  - [6.10 查看分词器的分词结果](#610-查看分词器的分词结果)
- [7. aggregations 聚合](#7-aggregations-聚合)
  - [7.1 Bucket aggregations 桶聚合](#71-bucket-aggregations-桶聚合)
    - [7.1.1 terms aggregation](#711-terms-aggregation)
    - [7.1.2 range aggregation](#712-range-aggregation)
    - [7.1.3 date_range aggregation](#713-date_range-aggregation)
    - [7.1.4 ip_range aggregation](#714-ip_range-aggregation)
    - [7.1.5 histogram aggregation](#715-histogram-aggregation)
    - [7.1.6 date_histogram aggregation](#716-date_histogram-aggregation)
    - [7.1.7 filter aggregation](#717-filter-aggregation)
    - [7.1.8 filters aggregation](#718-filters-aggregation)
    - [7.1.9 global aggregation](#719-global-aggregation)
    - [7.1.10 composite aggregation](#7110-composite-aggregation)
    - [7.1.11 multi terms aggregation](#7111-multi-terms-aggregation)
    - [7.1.12 missing agregation](#7112-missing-agregation)
    - [7.1.13 nested agregation](#7113-nested-agregation)
  - [7.2 Metric aggregations 指标聚合](#72-metric-aggregations-指标聚合)
    - [7.2.1 avg aggregation](#721-avg-aggregation)
    - [7.2.2 sum aggregation](#722-sum-aggregation)
    - [7.2.3 min aggregation](#723-min-aggregation)
    - [7.2.4 max aggregation](#724-max-aggregation)
    - [7.2.5 cardinality aggregation](#725-cardinality-aggregation)
    - [7.2.5 stats aggregation](#725-stats-aggregation)
    - [7.2.6 rate aggregation](#726-rate-aggregation)
    - [7.2.7 value count aggregation](#727-value-count-aggregation)
    - [7.2.8 top hits aggregation](#728-top-hits-aggregation)
    - [7.2.9 top metrics aggregation](#729-top-metrics-aggregation)
  - [7.3 Pipeline aggregations 管道聚合](#73-pipeline-aggregations-管道聚合)
    - [7.3.1 average bucket aggregation](#731-average-bucket-aggregation)
    - [7.3.2 sum bucket aggregation](#732-sum-bucket-aggregation)
    - [7.3.3 min bucket aggregation](#733-min-bucket-aggregation)
    - [7.3.4 max bucket aggregation](#734-max-bucket-aggregation)
    - [7.3.5 stats bucket aggregation](#735-stats-bucket-aggregation)
    - [7.3.6 percentiles bucket aggregation](#736-percentiles-bucket-aggregation)
    - [7.3.7 bucket script aggregation](#737-bucket-script-aggregation)
    - [7.3.8 bucket selector aggregation](#738-bucket-selector-aggregation)
    - [7.3.9 bucket sort aggregation](#739-bucket-sort-aggregation)
    - [7.3.10 cumulative cardinality aggregation](#7310-cumulative-cardinality-aggregation)
    - [7.3.11 cumulative sum aggregation](#7311-cumulative-sum-aggregation)
- [8. 数据迁移](#8-数据迁移)
  - [8.1 在线迁移](#81-在线迁移)
  - [8.2 离线迁移](#82-离线迁移)

## 1. 基本概念

### 1.1 索引

索引是文档的集合，相当于数据库中的数据库。

### 1.2 文档

文档是索引中存储的数据，相当于数据库中的表。

### 1.3 映射

映射是索引中字段的定义，相当于数据库中的表结构。

mappings 中字段的属性创建后就不能修改，只能删除索引后重新创建。

settings 创建后可以修改，但是有些settings选项修改后需要重新索引数据。

## 2. 映射管理

### 2.1 settings管理

#### 2.1.1 查看settings

```json
# 查看指定索引的settings

GET: /index_name/_settings

# 查看所有索引的settings

GET: /_settings
```

#### 2.1.2 修改settings

```json
# 解锁ES的只读模式,es空间不足解除自动写保护

PUT /_settings
{
  "index": {
    "blocks": {
      "read_only_allow_delete": "false"
    }
  }
}

# 修改指定索引的settings

PUT /index_name/_settings
{
  "index": {
    "blocks": {
      "read_only_allow_delete": "false"
    }
  }
}

# 修改集群最大分片数，默认为1000

PUT /_cluster/settings
{
  "persistent": {
    "cluster.max_shards_per_node": 2000
  }
}

# 修改指定索引的settings

PUT /index_name/_settings
{
  "index": {
    "refresh_interval": "30s"
  }
}

# 修改所有索引的settings

PUT /_settings
{
  "index": {
    "refresh_interval": "30s"
  }
}
```

### 2.2 mappings管理

#### 2.2.1 查看mappings

```json
# 查看指定索引的mappings

GET: /index_name/_mappings

# 查看所有索引的mappings

GET: /_mappings

# 查看指定索引的指定字段的mappings

GET: /index_name/_mapping/field/Id,Title,Category
```

#### 2.2.2 修改mappings

```json
# 添加字段
PUT /index_name/_mapping
{
    "properties": {
        "PunishmentAmount": {
            "type": "double"
        }
    }
}
```

### 2.2.3 mappings参数

- `dynamic`: 动态映射，默认为`true`，当索引文档时，如果遇到未定义的字段，会自动添加到映射中
  - `true`: 自动添加未定义字段
  - `false`: 不自动添加未定义字段
  - `strict`: 如果遇到未定义字段，会抛出异常
  - `runtime`: 动态映射，新的字段作为运行时字段被添加到映射中。这些字段未建立索引，会在查询时从 `_source` 中加载
- `enabled`: 是否启用索引字段，默认为`true`，如果为`false`，则该字段不会被索引。整个映射功能也可被禁用，文档将存储在 _source 字段中，可以检索该文档，但所有内容均不会被索引。
- `store`: 是否存储字段，默认为`false`，如果为`true`，则该字段会被存储，可以单独获取该字段的值。默认情况下，字段值存储在 `_source` 字段中，因此不需要显式存储字段。
- `index`: 是否索引字段，默认为`true`，如果为`false`，则该字段不会被索引。数值类型、日期类型、布尔类型、IP类型、地理点类型以及关键词类型，在未建立索引但仅启用文档值的情况下，同样可以进行查询。
- `fields`:多字段，针对不同用途，以多种方式对同一字段进行索引通常非常有用。例如，字符串字段可以映射为`text`字段用于全文搜索，也可以映射为`keyword`字段用于排序或聚合操作。
- `properties`: 类型映射、对象字段及嵌套字段均包含称为`properties`的子字段。这些属性可以是任何数据类型，包括`object`和`nested`。
- `analyzer`:用于指定在对`text`字段进行索引或搜索时所使用的文本分析工具。只有`text`类型字段支持。不能更新一个已经存在的字段的`analyzer`
- `doc_values`:是一种在文档索引时构建的列式存储方式的磁盘数据结构，一种数据访问模式。与`_source`字段存储相同的值，排序和聚合操作提高效率。除`text`和`annoteated text`外，所有字段类型都支持   `doc values`:默认为`true`，为`false`，无法进行排序和聚合操作、`script query`，可以节省磁盘存储空间。
- `format`: Elasticsearch 使用一组预配置的格式来识别并解析json中的日期字符串，转换为`UTC` 时间“自纪元以来经过的毫秒数”的长整型值。预置格式可以使用`format`参数指定。
- `term_vector`:包含了分析过程中生成的`terms`相关信息
  - `no`: 不存储任何信息
  - `yes`: 仅存储`terms`
  - `with_positions`: 存储`terms`和位置
  - `with_offsets`: 存储`terms`和字符偏移量
  - `with_positions_offsets`: 存储`terms`、位置、字符偏移量
  - `with_positions_payloads`: 存储`terms`、位置和每个术语位置相关联的用户自定义二进制数据。
  - `with_positions_offsets_payloads`: 存储`terms`、位置、字符偏移量和每个术语位置相关联的用户自定义二进制数据。

- `ignore_above`: 长度超过`ignore_above`值的字符串将不会被建立索引或存储。对于字符串数组，`ignore_above`会分别应用于每个数组元素。最大是Lucene为32766，非ascii中的UTF8字符应该除以4。
- `null_value`：空值无法进行索引或搜索。当某个字段被设置为`null`（或为空数组或包含多个`null`值的数组）时，系统会将其视为该字段没有值。`null_value`只影响数据的索引方式，不会修改`_source`文档。
- `search_analyzer`:默认情况下，查询和索引使用相同的分词器，在使用同义词查询时，可通过 `search_analyzer` 设置进行覆盖。
- `index_options`: 控制添加到倒排索引中以用于搜索和高亮显示的信息。仅`text`和`keyword`等基于词段的字段类型支持此配置。默认为`positions`。
  - `docs`: 仅索引文档ID
  - `freqs`: 索引文档ID和词频
  - `positions`: 索引文档ID、词频和词位置
  - `offsets`: 索引文档ID、词频、词位置和词偏移量
- `index_prefix`：用于索引词前缀以加快前缀搜索速度。
  - `min_chars`: 前缀的最小长度，默认为2，大于0，包含值
  - `max_chars`: 前缀的最大长度，默认为5，小于20，包含值
- `position_increment_gap`: 在对具有多个值的文本字段进行索引时，会在各值之间添加一个“虚拟”间隔，以防止大多数短语查询在这些值之间发生匹配。该间隙的大小通过`position_increment_gap`参数进行配置，默认值为 100。
- `normalizer`：`keyword`字段的`normalizer`与`analyzer`类似，但它保证了分析链产生单个词元。规范化器在索引`keyword`之前应用，以及在搜索时应用，当通过查询解析器（如`match`查询）或通过词级查询（如term查询）搜索`keyword`字段时。
- `ignore_malformed`: 默认为`false`，如果为`true`，则忽略格式错误的数字、日期或布尔值等数据类型，而不是抛出异常。使用`_ignored`字段的`exists` 或`terms`查询检查格式错误文档。
- `copy_to`：允许将多个字段的值复制到一个组字段中，该组字段随后可作为单个字段进行查询，可以提高查询效率。示例：`first_name`和 `last_name`复制到`full_name`字段。
- `coerce`:是否启用类型转换，默认为`true`。
  - `true`: 启用类型转换，`string`类型转换为`number`，`float`类型会截取为`integer`类型。
  - `false`: 禁用类型转换
- `subobjects`：是否启用子对象，默认为`true`，如果为`false`，则忽略子对象。索引指标数据时，`metrics.time.min:10`, mapping:`"metrics": {"type": "object", "subobjects": false}`，则`min`不会创建子对象，创建 `time.min` 作为`time`同级字段mapping。

### 2.2.4 字段数据类型

`常用类型`

- `boolean`: 布尔型
- `binary`: 二进制型，二进制值以 Base64 字符串形式编码，默认情况下不会被存储，也无法进行搜索。
- `text type family` 默认不支持排序、聚合、脚本。mappings启用`fielddata:true`支持，但会消耗大量内存，不建议使用。建议使用`fields mappings`设置多个字段类型。
  - `text`: 文本类型，用于全文搜索
  - `match_only_text`: 仅匹配文本类型，禁用评分功能，最适合用于对日志消息索引。只能使用默认分词器，不支持`span query`,可以使用`interval query`。
- `keywords type family`
  - `keyword`: 关键字类型，用于精确匹配
  - `constant_keyword`: 常量关键字类型，用于精确匹配
  - `wildcard`: 通配符类型，用于模糊匹配
- `numbers`
  - `long`: 64位长整数类型
  - `integer`: 32位整数类型
  - `short`: 16位短整型
  - `byte`: 8位整数，字节型
  - `double`: 双精度64位浮点型
  - `float`: 单精度32位浮点型
  - `half_float`: 半精度16位浮点型
  - `scaled_float`: 缩放浮点型，由一个 `long` 数据类型表示，并通过固定的双精度缩放因子进行缩放。
  - `unsigned_long`: 无符号64位长整数类型
- `dates`
  - `date`: 日期类型，现有的日期数据类型以毫秒为单位存储日期。
  - `date_nanos`: 日期纳秒类型，数据类型以纳秒为单位存储日期。聚类依旧使用毫秒。
- `arrays`: 数组类型，支持任何数据类型，包括嵌套数组。不需要显示`mapping`设置，但是必须是相同的数据类型。对象数组不支持检索单个对象，使用`nested`类型代替。

`object和关系类型`

- `object`: json对象类型
- `nested`: 嵌套json对象类型
- `join`: 关系类型，用于定义父子关系。唯一适用的情况是当数据包含一对多关系时，且其中一个实体的数量远多于另一个实体。
- `flattened`:扁平化类型，将整个 JSON 对象作为单一字段值。适用于对具有大量或未知数量唯一键的对象进行索引。

`结构化数据类型`

- `range`
  - `integer_range`: 整数范围类型
  - `long_range`: 整数范围类型
  - `float_range`: 浮点数范围类型
  - `double_range`: 双精度浮点数范围类型
  - `date_range`: 日期范围类型
  - `ip_range`: ip范围类型
- `ip`: ip类型，ipv4和ipv6
- `nurmur3`: 哈希类型
- `version`: 软件版本类型，支持`Semantic Versioning`

`聚合数据类型`

- `histogram`: 直方图类型，存储表示直方图的预聚合数值数据的字段
- `aggregate_metric_double`:预聚合的度量值

`文本检索类型`

- `text fields`
  - `text`: 文本类型，用于全文搜索
  - `match_only_text`: 仅匹配文本类型
- `annotated-text`: 注释文本类型
- `completion`: 自动补全类型
- `search_as_you_type`: 搜索时自动补全类型
- `token_count`: 计数类型，接收一个字符串，使用`analyzer`分析，返回`token`数量。

`文档排名类型`

- `dense_vector`: 密集向量类型
- `sparse_vector`: 稀疏向量类型
- `rank_feature`: 排名特征类型，记录一个数值特征，以提高查询时的命中率。
- `rank_features`: 排名特征类型，记录数值特征以提升查询时的命中率。

`特殊数据类型`

- `geo_point`: 地理位置点类型
- `geo_shape`: 地理位置形状类型
- `point`: 点类型
- `shape`: 形状类型
- `percolator`：渗透器字段类型可将JSON结构解析为原生查询语句并存储该查询语句，从而使`Percolate`查询能够利用该语句来匹配指定文档
- `alias`: 字段别名类型，给已存在的字段添加别名，查询、聚合和排序字段、脚本，也可用于请求 `docvalue_fields`、`stored_fields`、建议结果及高亮显示内容。字段功能的`field capabilities`。字段类型不能是`object`或者另一个别名字段，不支持能过字段别名索引数据，查询不支持`terms`、`geo_shape`、`more_like_this`。
- `completion`：类型补全类型，使用补全建议功能时使用。

### 2.2.5 metadata字段

`Identity metadata fields`

- `_index`: 索引名称
- `_id`: 文档id，最大长度限制为512字节

`Document source metadata fields`

- `_source`: 文档源数据，禁用`_source`可以节省存储空间，不能按条件更新文档、重新索引数据、实时高亮功能，不推荐，使用 `{"mappings": {"_source": {"enabled": false}}`禁用
  - `synthetic source`：合成源，有数据字段类型限制，还会修改获取的源数据结构。使用`{"mappings": {"_source": {"mode": "synthetic"}}}` 可以启用合成源
- `_size`: 文档大小

`Doc count metadata fields`

- `_doc_count`: 聚合结果每个bucket的文档数量

`indexing metadata fields`

- `_field_names`: 用于对文档中所有包含非空值的字段名称进行索引。该字段被exists查询用于查找文档，这些文档要么在某个特定字段中包含非空值，要么不包含任何非空值。
- `_ignored`: 用于索引并存储文档中所有在索引过程中被忽略的字段名称。例如，当字段格式不正确且启用了`ignore_malformed`选项时，或者当关键词字段的值超过了其可选的`ignore_above`设置时，就可能出现这种情况。

`routing metadata fields`

- `_routing`: 文档的路由值，默认是文档的`_id`，定制路由时需要在先索引数据时指定`routing`值，否则无法通过`routing`值查询到数据

`other metadata fields`

- `_meta`: 文档的元数据,映射类型可以关联自定义元数据。Elasticsearch完全不使用这些功能，但可用于存储应用程序特定的元数据
- `_tier`: 文档的层级,在跨多个索引执行查询时，有时需要针对特定数据层级（`data_hot`、`data_warm`、`data_cold` 或 `data_frozen`）节点上持有的索引进行操作。`tier`字段可用于根据文档被索引到的索引的`tierPreference`设置进行匹配

## 3. 索引管理

### 3.1 创建索引

```json
 PUT /index_name
 {
    "aliases": {},
    "mappings": {
        "dynamic": "false",
        "_source": {
            "excludes": [
                "FullText"
            ]
        },
        "properties": {
            "Category": {
                "type": "keyword",
                "store": true
            },
            "FullText": {
                "type": "text",
                "term_vector": "with_positions_offsets",
                "analyzer": "standard"
            },
            "CreateTime": {
                "type": "date",
                "store": true,
                "format": "yyyy||yyyyMM||yyyy.MM||yyyy/MM||yyyy-MM||yyyyMMdd||yyyy.MM.dd||yyyy/MM/dd||yyyy-MM-dd||yyyy-MM-dd HH:mm:ss||yyyy.MM.dd HH:mm:ss||yyyy/MM/dd HH:mm:ss||yyyy-MM-dd HH:mm:ss.SSS||yyyy.MM.dd HH:mm:ss.SSS||yyyy/MM/dd HH:mm:ss.SSS"
            },            
            "Id": {
                "type": "keyword"
            },
            "SortNum": {
                "type": "integer"
            },           
            "Title": {
                "type": "text",
                "store": true,
                "term_vector": "with_positions_offsets",
                "analyzer": "standard"
            }            
        }
    },
    "settings": {
        "index": {
            "number_of_shards": "2",
            "number_of_replicas": "1"
        }
    }
}   
```

### 3.2 删除索引

```json
DELETE /index_name
```

### 3.3 查看索引

```json
GET /index_name
```

### 3.4 检查索引是否存在

```json
HEAD /index_name
```

### 3.5 查看所有索引

```json
GET /_cat/indices?v=true
```

## 4. 别名管理

### 4.1 查看别名

```json
# 查看所有别名

GET /aliases

# 查看指定索引的别名

GET /index_name/_alias

# 查看指定的别名

GET /_alias/alias_name

```

### 4.2 添加别名

```json
# 添加别名
PUT: /index_name/_alias/alias1
PUT: /index_name/_aliases/alias1
{

}

POST /_aliases
{
  "actions": [
    {
      "add": {
        "index": "test",
        "alias": "alias1",        
      }
    }
  ]
}

# 添加别名并设置过滤条件
PUT: /index_name1,index_name2/_alias/alias1
 {
    "filter": {
        "range": {
            "UpdateTime": {
                "from": "2025-01-01"
            }
        }
    }
 }

 POST: /_aliases
{
    "actions": [
        {
            "add": {
                "indices": [
                    "index_name1",
                    "index_name2"
                ],
                "aliases": [
                    "alias1",
                    "alias2"
                ],
                "filter": {
                    "range": {
                        "UpdateTime": {
                            "from": "2025-01-01"
                        }
                    }
                }
            }
        }
    ]
}


```

### 4.3 删除别名

```json
# Delete删除指定索引的指定别名

DELETE: /index_name/_alias/alias_name1

# POST删除指定索引的指定别名

POST /_aliases
{
  "actions": [
    {
      "remove": {
        "index": "index_name",
        "alias": "alias_name"
      }
    }
  ]
}

# Delete删除指定的别名

DELETE: /index_name1,index_name2/_alias/alias_name1
DELETE: /index_name1,index_name2/_aliases/alias_name1

# POST删除指定的别名

POST /_aliases
{
  "actions": [
    {
      "remove": {
        "indices": [
          "index_name1",
          "index_name2"
        ],
        "alias": "alias_name"
      }
    }
  ]
}
```

### 4.4 修改别名

```json
# POST修改别名

POST /_aliases
{
  "actions": [
    {
      "remove": {
        "index": "index_name",
        "alias": "alias_name"
      }
    },
    {
      "add": {
        "index": "index_name",
        "alias": "alias_name"
      }
    }
  ]
}

POST: /_aliases               
{
    "actions": [
        {
            "remove": {
                "aliases": [
                    "test1",
                    "test2"
                ],
                "indices": "test"
            }
        },
        {
            "add": {
                "aliases": [
                    "test1",
                    "test2"
                ],
                "indices": [
                    "test",
                    "testa"
                ],
                "filter": {
                    "range": {
                        "UpdateTime": {
                            "from": "2025-01-01"
                        }
                    }
                }
            }
        }
    ]
}
```

### 4.5 检查别名是否存在

```json
# 检查指定索引的别名是否存在

HEAD /index_name/_alias/alias_name

# 检查指定的别名是否存在

HEAD /_alias/alias_name
```

## 5. 文档管理

### 5.1 创建文档

```json
# 创建文档,如果_id存在，则报错

PUT /index_name/_create/1
{
  "Id": "1",
  "Title": "test",
  "Category": ["001"],
  "UpdateTime": "2025-01-01"
}

# 索引文档,如果_id存在，则覆盖
PUT /index_name/_doc/1
{
  "Id": "1",
  "Title": "test",
  "Category": ["001"],
  "UpdateTime": "2025-01-01"
}
```

### 5.2 查看文档

```json
# 查看指定文档

GET: /index_name/_doc/1?pretty=true

# 查看指定文档的指定字段

GET: /index_name/_doc/1?_source=Id,Title,Category

# 查看指定文档的指定字段

GET: /index_name/_source/1?_source_includes=Id,Title,Category&pretty=true
```

### 5.3 更新文档

```json
# doc更新文档部分字段

POST: /index_name/_update/1?pretty=true
 {              
    "doc": {
    "UpdateTime": "2025-11-03 15:13:01"
    }              
}

# script 更新文档部分字段

POST: /index_name/_update/1?pretty=true
{
    "script": {
    "lang": "painless",
    "source": "ctx._source.UpdateTime = params.updateTime",
    "params": {
        "updateTime": "2025-11-14 09:38:02"
    }
    },
    "scripted_upsert": true
}
```

### 5.4 删除文档

```json
DELETE /index_name/_doc/1
```

### 5.5 批量操作管理

#### 5.5.1 批量管理文档

```json
# 批量创建文档，如果_id存在，则报错

POST /index_name/_bulk
{"create":{"_id":"1"}}
{"Id":"1","Title":"test","Category":["001"],"UpdateTime":"2025-01-01"}
{"create":{"_index":"index_name","_id":"2"}}
{"Id":"2","Title":"test","Category":["001"],"UpdateTime":"2025-01-01"}

# 批量索引文档，如果_id存在，则覆盖

POST /index_name/_bulk
{"index":{"_id":"1"}}
{"Id":"1","Title":"test","Category":["001"],"UpdateTime":"2025-01-01"}
{"index":{"_id":"2"}}
{"Id":"2","Title":"test","Category":["001"],"UpdateTime":"2025-01-01"}

# 批量更新文档，如果_id存在，则更新，如果_id不存在，则创建

POST /index_name/_bulk
{"update":{"_id":"1"}}
{"doc":{"Title":"test1"}}
{"update":{"_id":"2"}}
{"doc":{"Title":"test2"}}

# 批量删除文档  

POST /index_name/_bulk
{"delete":{"_id":"1"}}
{"delete":{"_id":"2"}}

# 批量索引、更新、删除文档

POST /_bulk
{"create":{"_index":"index_name","_id":"1"}}
{"Id":"1","Title":"test","Category":["001"],"UpdateTime":"2025-01-01"}
{"index":{"_index":"index_name","_id":"2"}}
{"Id":"2","Title":"test","Category":["001"],"UpdateTime":"2025-01-01"}
{"update":{"_index":"index_name","_id":"2"}}
{"doc":{"Title":"test1"}}
{"delete":{"_index":"index_name","_id":"3"}}

```

#### 5.5.2 带条件的批量操作管理

```json
# 按条件使用script批量更新文档

POST: /index_name/_update_by_query?pretty=true
{
    "query": {
        "term": {
            "Id": {
                "value": "100"
            }
        }
    },
    "script": {
        "source": "ctx._source.UpdateTime = params.updateTime ; ctx._source.MaxTiao = ctx._source.MaxTiao + params.maxTiao;",
        "params": {
            "updateTime": "2025-11-14 14:20:24",
            "maxTiao": 5
        }
    }
}

# 按条件使用script_id批量更新文档

POST: /chl/_update_by_query?pretty=true
{
    "query": {
        "term": {
            "Id": {
                "value": "100"
            }
        }
    },
    "script": {
        "id": "scrpit_update_updatetime1",
        "params": {
            "updateTime": "2025-11-14 14:44:24"
        }
    }
}

# 按条件批量删除文档

POST: /index_name/_delete_by_query?pretty=true
{
    "query": {
        "term": {
            "Id": {
                "value": "100"
            }
        }
    }
}
```

### 5.6 脚本管理

注意：

- `ctx._source`：用于更新脚本，读写原始数据。

- `ctx.doc`：用于检索脚本，只读，不能用于更新

#### 5.6.1 创建脚本

```json
PUT /_scripts/script_name
{
  "script": {
    "lang": "painless",
    "source": "ctx._source.UpdateTime = params.updateTime"    
  }
}
```

#### 5.6.2 查看脚本

```json
GET /_scripts/script_name
```

#### 5.6.3 删除脚本

```json
DELETE /_scripts/script_name
```

### 5.7 重新索引文档

```json
POST /_reindex?pretty=true&wait_for_completion=true
{
    "conflicts": "proceed",
    "dest": {
        "index": "dest_index_name"
    },
    "script": {
        "lang": "painless",
        "source": "ctx._source.UpdateTime = params.updateTime",
        "params": {
            "updateTime": "2025.11.18 15:17:12"
        }
    },
    "source": {
        "index": "source_index_name",
        "query": {
            "term": {
                "Gid": {
                    "value": "100"
                }
            }
        },
        "_source": [
            "Id",
            "Title",
            "FullText",
            "Category",            
            "CreateTime"
        ]
    }
}
```

### 5.8 检查文档是否存在

```json
HEAD /index_name/_doc/1
```

## 6 查询

### 6.1 match all query

`match_all query`：匹配所有文档，返回所有文档。

```json
GET: /index_name/_search
{  
  "query": {
    "match_all": {}
  }
}
```

`match_none query`：不匹配任何文档，返回空结果集。

```json
GET: /index_name/_search
{  
  "query": {
    "match_none": {}
  }
}
```

### 6.2 term-level query

通过`Term-Level query`，基于结构化数据中的精确数值查找文档。结构化数据的示例包括日期范围、IP地址、价格或产品ID。

与`Full-text query`不同，`Term-Level query`不分析搜索词。相反，`Term-Level query`会与字段中存储的精确`terms`进行匹配。

#### 6.2.1 ids query

- `values` ：要搜索的文档`_id`列表

```json
GET: /index_name/_search
{  
  "query": {
    "ids": {      
      "values": ["1", "2", "3"]
    }
  }
}
```

#### 6.2.2 term query

`term query`：精确匹配，用于`keyword`类型字段

- `value` ：要搜索的值，该`term`必须与字段值完全匹配，包括空格和大小写。
- `boost` ：用于降低或提高查询相关性评分的浮点数，默认值为1.0。Boost值相对于默认值1.0进行计算。Boost值在0至1.0之间时，会降低相关性评分；当Boost值超过1.0时，则会提高相关性评分。
- `case_insensitive` [7.10.0]：是否忽略大小写，默认值为false

```json
GET: /index_name/_search
{  
  "query": {
    "term": {      
      "Category": "001"
    }
  }
}
```

**注意：** 避免在`text`类型字段中使用`term query`

默认情况下，Elasticsearch会在分析过程中修改`text`字段的值。这可能导致难以精确匹配`text`字段的值。如需检索`text`字段值，请改用`match query`。

默认的`standard analyzer`改变`text`字段的值如下

1. 删除大部分标点符号
2. 将剩余内容分割为独立词汇，称为`tokens`
3. 将`tokens`转换为小写形式

#### 6.2.3 terms query

`terms query`与`term query`相同，但支持多值检索。只要文档包含任意一个匹配`term`，即视为符合条件。如需检索包含多个匹配`term`的文档，请使用`terms_set query`。

```json
GET: /index_name/_search
{  
  "query": {
    "terms": {      
      "Category": ["001", "002"]
    }
  }
}
```

#### 6.2.4 terms_set query

`terms_set` 检索包含多个匹配`term`的文档。`terms_set` 查询可以用于精确匹配，也可以用于模糊匹配。

- `field`：要搜索的字段
- `terms`：要匹配的值列表，匹配项的最低数量要求由`minimum_should_match_field`或`minimum_should_match_script`参数定义
- `minimum_should_match_field`: 数字字段，用于存储返回文档所需的匹配项数量
- `minimum_should_match_script`: 定制脚本，包含返回文档所需的匹配项数量
- `boost`：查询的权重

```json
# terms_set查询至少匹配两种语言的文档
GET /index_name/_search
{
  "query": {
    "terms_set": {
      "programming_languages": {
        "terms": [ "c++", "java", "php" ],
        "minimum_should_match_field": "required_matches"
      }
    }
  }
}

GET: /index_name/_search
{  
  "query": {
    "terms_set": {      
      "ProgrammingLanguages": {
        "terms": ["c", "c#", "c++", "java"],
        "minimum_should_match_script": {
          "source": "Math.min(params.num_terms, doc['ProgrammingLanguages'].value.length)"
        }
      }
    }
  }
}
```

#### 6.2.5 range query

- `field` ：要搜索的字段
- `gte` ：大于或等于
- `gt` ：大于
- `lte` ：小于或等于
- `lt` ：小于
- `from`：大于或等于
- `to` ：小于或等于
- `format`: 用于转换查询中日期值的日期格式
- `relation`:用于指定范围查询与范围字段值的匹配方式。默认值为`INTERSECTS`  
  - `INTERSECTS`:字段值与查询范围有交集（最宽松，默认）
  - `CONTAINS`:字段值包含查询范围
  - `WITHIN`:字段值被包含在查询范围内
- `time_zone`:用于将查询中的日期值转换为 UTC 的协调世界时（UTC）偏移量或 IANA 时区。
  - ISO 8601 UTC 偏移量，例如 `+01：00` 或 `-08：00`
  - IANA 时区 ID，例如 `America/Los_Angeles`
- `boost` ：查询的权重,默认值为1.0

**注意**:若`format`或日期值不完整，范围查询将用`missing date components`默认值替换，缺失的年份不会被替换。

`missing date components`

```md
MONTH_OF_YEAR:    01
DAY_OF_MONTH:     01
HOUR_OF_DAY:      23
MINUTE_OF_HOUR:   59
SECOND_OF_MINUTE: 59
NANO_OF_SECOND:   999_999_999
```

```json
# 查询数字范围
GET /_search
{
  "query": {
    "range": {
      "age": {
        "gte": 10,
        "lte": 20,
        "boost": 2.0
      }
    }
  }
}

# 查询日期时间范围

GET _search
{
    "query": {
        "range" : {
            "CreateTime" : {
                "gte" : "now-1d/d",
                "lt" :  "now/d"
            }
        }
    }
}

```

`Date Math`

**时间单位**：

- `y`: 年
- `M`：月
- `W`：周
- `d`：天
- `h`：小时
- `H`: 小时
- `m`：分钟
- `s`：秒

表达式以锚定日期开头，该日期可以是当前时间，也可以是以 `||` 结尾的日期字符串。该锚定日期可选地可跟随一个或多个数学表达式：

- `now`：当前日期和时间，如`now`是`2001-02-01 12:00:00`
- `+1h`：增加1小时,如`now + 1h`是`2001-02-01 13:00:00`
- `-1d`：减去一天，如`now - 1d`是`2001-01-31 12:00:00`
- `/d`：向下取整至最近的日期，`now-1h/d`是 `2001-02-01 00:00:00`，`2001.02.01||+1M/d`是`2001-03-01 00:00:00`
- `/M`: 向上取整到最近的月，`2001.02.12||+1M/M`是`2001-04-01 00:00:00`
- `/y`: 向下取整到年初，`2001.02.12||/y`是`2001-01-01 00:00:00`

**注意：** 将 `search.allow_expensive_queries` 设置为 `false`，则不会执行对`text`或`keyword`字段的`range query`。

#### 6.2.6 Fuzzy query

`edit distance`：编辑距离，也称为 Levenshtein 距离，是指将一个字符串转换为另一个字符串所需的最少单字符编辑（插入、删除或替换）次数。

1. 改变字符
2. 删除字符
3. 插入字符
4. 相邻字符交换位置

- `field` ：要搜索的字段
- `value` ：要搜索的值
- `fuzziness`：允许的最大`edit distance`。默认值为`AUTO`，取值范围为`0-2`
- `max_expansions`：创建的最大变体数量。默认值为`50`
- `prefix_length`：前缀的长度。默认值为`0`
- `transpositions`：是否允许转置。默认值为`true`
- `rewrite`: 重写方式，默认 `constant_score_blended`。该参数仅限专家用户使用。更改此参数的值可能影响搜索性能和相关性。

**注意：**`search.allow_expensive_queries` 设置为 `false` ，则不会执行`fuzzy query`

```json
GET /_search
{
  "query": {
    "fuzzy": {
      "user.id": {
        "value": "ki",
        "fuzziness": "AUTO",  
        "max_expansions": 50, 
        "prefix_length": 0,
        "transpositions": true,
        "rewrite": "constant_score_blended"
      }
    }
  }
}
```

#### 6.2.7 prefix query

- `rewrite`: 重写方式，默认 `constant_score_blended`。该参数仅限专家用户使用。更改此参数的值可能影响搜索性能和相关性。
- `case_insensitive` [7.10.0]：是否忽略大小写，默认值为`false`

```json
GET: /index_name/_search
{  
  "query": {
    "prefix": {      
      "Title": "tes"
    }
  }
}
```

**注意：**`search.allow_expensive_queries` 设置为 `false` ，则不会执行`prefix query`

#### 6.2.8 wildcard query

通配符查询使用通配符表达式来匹配字段中的值。

- `value`: 检索值
  - 通配符 `*` 匹配零个或多个字符，
  - 问号 `?` 匹配任何单个字符。
- `wildcard`: `value`参数的别名。若同时指定`value`和`wildcard`，查询将采用请求体中的`wildcard`
- `boost`: 查询权重，默认1.0。
- `rewrite`: 重写方式，默认 `constant_score_blended`。该参数仅限专家用户使用。更改此参数的值可能影响搜索性能和相关性。
- `case_insensitive` [7.10.0]：是否忽略大小写，默认值为`false`

```json
GET: /index_name/_search
{  
  "query": {
    "wildcard": {      
      "Title": "tes*"
    }
  }
}
```

**注意**:

- 避免使用`*`或`?`作为开头模式。这可能增加匹配项所需的迭代次数并降低搜索性能
- `search.allow_expensive_queries` 设置为 `false` ，则不会执行`wildcard query`

#### 6.2.9 regexp query

正则表达式查询使用正则表达式来匹配字段中的值。

- `value`: 检索值
- `flags`: 为正则表达式启用可选运算符，默认`ALL`
- `case_insensitive` [7.10.0]：是否忽略大小写，默认值为`false`
- `max_determinized_states`: 正则表达式查询的最大确定状态数。默认值为`10000`
- `rewrite`: 重写方式，默认 `constant_score_blended`。该参数仅限专家用户使用。更改此参数的值可能影响搜索性能和相关性。

`操作符`:

- `.`: 匹配任何单个字符
- `?`：匹配零个或一个字符
- `*`：匹配零个或多个字符
- `+`：匹配一个或多个字符
- `|`：或操作，例如`a|b`匹配`a`或`b`
- `{}`: 前一个字符重复的最小次数和最大次数，例如`a{2,3}`匹配`aa`或`aaa`
- `()`: 分组，例如`(abc|def)`匹配`abc`或`def`
- `[]`：匹配字符集中任一字符，例如`[abc]`匹配`a`、`b`或`c`
- `[^]`：匹配不在字符集中的字符，例如`[^abc]`匹配除`a`、`b`和`c`之外的任何字符

**注意**:

`regexp query` 不支持行起始符`$`和行截止符`^`

```json
GET: /index_name/_search
{  
  "query": {
    "regexp": {      
      "Title": "tes.*"
    }
  }
}
```

**注意：**`search.allow_expensive_queries` 设置为 `false` ，则不会执行`regexp query`

#### 6.2.10 Exists query

文档字段的索引值可能因多种原因而不存在：

- source JSON 中的字段为 `null` 或 `[]`
- 字段在映射中设置了 `"index" : false` 和 `"doc_values" : false`
- 字段值的长度超出了映射中的`ignore_above`设置
- 字段值格式错误，且映射中定义了`ignore_malformed`

```json
GET: /index_name/_search
{  
  "query": {
    "exists": {      
      "field": "Category"
    }
  }
}
```

如果 JSON 值为`null`或`[]`，则认为字段不存在，但这些值将表示字段存在：

- 空字符串，例如 `""` 或 `"-"`
- 包含空值和其他值的数组，例如`[null,"foo"]`
- 字段映射中定义的自定义空值，如下面示例所示：

```json
# 自定义空值
PUT /index_name
{
  "mappings": {
    "properties": {
      "status_code": {
        "type":       "keyword",
        "null_value": "NULL" 
      }
    }
  }
}
```

**重点**：`null_value` 必须和field是相同的数据类型. 例如，如果字段是 `long` 类型，则不能有字符串 `null_value`。

```json
# 查询status_code字段没有索引值的文档
GET /index_name/_search
{
  "query": {
    "bool": {
      "must_not": {
        "exists": {
          "field": "status_code"
        }
      }
    }
  }
}
```

### 6.3 full-text query 全文查询

`Full-text query`支持对分析后的`text`字段（如电子邮件正文）进行检索。

`query string`将通过与字段索引时相同的分析器进行处理。

#### 6.3.1 Query_string query

一级参数

- `query`：必选，查询字符串，跨越所有非`Nested`字段检索
- `default_field`：可选，如果`query`未指定，默认使用`default_field`，默认为`_all`，支持通配符`*`。一次查询的字段乘以词项的数量有限制。该限制由 `indices.query.bool.max_clause_count` 搜索设置定义，默认值为 4096
- `default_operator`：可选，默认操作符，默认为`or`。取值范围为`or`或`and`
- `analyzer`：可选，分词器
- `boost`: 可选，查询权重，默认1.0
- `minimum_should_match`: 可选，指定必须匹配的`should`子句的最小数量。
- `fields`:可选，搜索字符串数组。支持通配符`*`
- `fuzziness`:可选，允许的最大`edit distance`。
- `fuzzy_max_expansions`:可选，创建的最大变体数量。默认值为`50`
- `fuzzy_prefix_length`:可选，前缀的长度。默认值为`0`
- `fuzzy_transpositions`:可选，是否允许转置。默认值为`true`
- `lenient`:可选，是否忽略格式错误，默认值为`false`,例如为数值字段提供文本值
- `allow_leading_wildcard`：可选，是否允许通配符`*`或`?`作为查询字符串的开头，默认为`true`
- `analyze_wildcard`：可选，查询会尝试分析查询字符串中的通配符词项。默认为`false`
- `auto_generate_synonyms_phrase_query` ：可选，是否自动生成同义词短语查询，默认为`true`
- `enable_position_increments`：可选，是否启用位置增量，默认为`true`
- `max_determinized_states`：可选，正则表达式查询的最大确定状态数。默认值为`10000`
- `quote_analyzer`:可选，用于将查询字符串中的引号文本转换为分词的 Analyzer
- `phrase_slop`:可选，短语匹配中允许的最大匹配词位置数。默认值为 0 。如果为 0 ，则要求精确短语匹配。转置词的 slop 值为 2 。
- `quote_field_suffix`:可选，查询字符串中引号文本后附加的后缀。
- `rewrite`:可选，重写方式。
- `time_zone`:可选，时区，默认为`UTC`

query_string 查询语法

```json
# 查询状态是active的文档
status:active

# title 字段包含 quick 或 brown
title:(quick OR brown)

# author 字段中包含确切短语 "john smith"
author:"John Smith"

# first name 字段中包含 Alice （注意我们需要用反斜杠转义空格）
first\ name:Alice

# book.title 、 book.content 或 book.date 字段中的任意一个包含 quick 或 brown （注意我们需要用反斜杠转义 * ）
book.\*:(quick OR brown)

# title 字段具有任何非空值
_exists_:title

# 2012 年的所有日期
date:[2012-01-01 TO 2012-12-31]

# 数字 1..5
count:[1 TO 5]

# 10 以上的数字
count:[10 TO *]

# 2012 年以前的日期
date:{* TO 2012-01-01}

# 1 到 5（不包括 5）
count:[1 TO 5}

# 年龄大于10
age:>10
age:>=10

# 年龄大于等于10小于20
age:(>=10 AND <20)

# boost 提升权重
title:(quick brown) ^2
title:quick^2 brown
title:"quick brown" ^2

# 布尔运算符，+表示必须存在，-表示必须不存在，没有符号表示可选
title: quick brown +fox -news

# 分组
(quick OR brown) AND fox

# 转义(1+1)=2
tip:\(1\+1\)\=2

# json 中转义字符，由于 \ （反斜杠）是 JSON 字符串中的特殊字符，需要转义，因此上述 query_string 中有两个反斜杠。
GET /my-index-000001/_search
{
  "query" : {
    "query_string" : {
      "query" : "kimchy\\!",
      "fields"  : ["user.id"]
    }
  }
}
```

query_string自定义查询

```json
# 查询所有字段中包含 quick 和 brown 的文档
GET: /index_name/_search
{  
  "query": {
    "query_string": {      
      "query": "quick brown",
      "fields": ["Title", "Author"]
    }
  }
}
```

#### 6.3.2 Simple_query_string query

语法比query_string查询更为严格，但simple_query_string查询不会因语法错误而返回错误。相反，它会忽略查询字符串中的任何无效部分。

一级参数

- `query`：必选，查询字符串，跨越所有非`Nested`字段检索
- `fields`：可选，搜索字符串数组。支持通配符`*`，可使用`^`提升权重。一次可以查询的字段数量有限制。这个限制由 indices.query.bool.max_clause_count 搜索设置定义，默认值为 1024
- `default_operator`：可选，默认操作符，默认为`or`。取值范围为`or`或`and`
- `analyzer`：可选，分词器
- `minimum_should_match`: 可选，指定必须匹配的`should`子句的最小数量。
- `fuzzy_max_expansions`:可选，创建的最大变体数量。默认值为`50`
- `fuzzy_prefix_length`:可选，前缀的长度。默认值为`0`
- `fuzzy_transpositions`:可选，是否允许转置。默认值为`true`
- `lenient`:可选，是否忽略格式错误，默认值为`false`,例如为数值字段提供文本值
- `analyze_wildcard`：可选，查询会尝试分析查询字符串中的通配符词项。默认为`false`
- `auto_generate_synonyms_phrase_query` ：可选，是否自动生成同义词短语查询，默认为`true`
- `quote_field_suffix`:可选，查询字符串中引号文本后附加的后缀。
- `flags`:可选，启用的操作符列表，默认`All`
  - `ALL`：表示启用所有操作符
  - `AND`：表示启用`+`AND操作符
  - `OR`：表示启用`|`OR操作符
  - `NOT`：表示启用`-`NOT操作符
  - `ESCAPE`:表示启用`\`作为转义操作符
  - `FUZZY`:在单词后启用`~N`作为模糊查询，`N`表示最大编辑距离
  - `NEAR`:启用`~N`操作符，`N`表示最大匹配词位置数，同`SLOP`
  - `NONE`:表示禁用所有操作符
  - `PREFIX`：表示启用`*`前缀操作符查询
  - `PHRASE`：表示启用`''`引号操作符用于短语查询
  - `PRECEDENCE`：表示启用`()`括号操作符，用于控制运算符优先级
  - `SLOP`：表示启用`~N`操作符，用于短语中`N`是最大匹配间隔数，同`NEAR`
  - `WHITESPACE`：表示启用空格分隔的单词查询

操作符：

- `+`:表示 `AND`
- `-`:表示 `NOT`
- `|`:表示 `OR`
- `(` 和 `)`:表示优先级
- `~`:表示模糊查询，`~N`在单词后表示模糊查询的最大编辑距离，`~N`后面的短语表示模糊查询的相似度。
- `*`:表示通配符查询，`*`在开头表示前缀查询
- `?`:表示通配符查询
- `"`:表示短语查询

```json
# 操作符示例
GET /_search
{
  "query": {
    "simple_query_string": {
      "fields": [ "content" ],
      "query": "foo bar -baz"
    }                                  
  }
}

# flags示例
GET /_search
{
  "query": {
    "simple_query_string": {
      "query": "foo | bar + baz*",
      "flags": "OR|AND|PREFIX"
    }
  }
}

# 对单个字段加权重
GET /_search
{
  "query": {
    "simple_query_string" : {
      "query" : "this is a test",
      "fields" : [ "subject^3", "message" ]
    }
  }
}
```

#### 6.3.3 Match query

`match` 查询的类型是 `boolean` 。这意味着提供的文本会被分析，分析过程会根据提供的文本构建一个布尔查询。 `operator` 参数可以设置为 `or` 或 `and` 来控制布尔子句（默认为 `or` ）。可以使用 `minimum_should_match` 参数来设置匹配所需的最少可选 `should` 子句数量。

查询参数

- `query`：必选，查询字符串
- `analyzer`：可选，分词器
- `boost`：可选，查询权重
- `minimum_should_match`: 可选，指定必须匹配的`should`子句的最小数量。
- `operator`:可选，用于解释 query 值中的文本的布尔逻辑，默认值为`OR`。取值范围为`OR`或`AND`
- `fuzziness`:可选，允许的最大`edit distance`。
- `fuzzy_max_expansions`:可选，创建的最大变体数量。默认值为`50`
- `fuzzy_transpositions`:可选，是否允许转置。默认值为`true`
- `fuzzy_rewrite`:可选，用于重写查询方法。默认值为`0`
- `lenient`:可选，是否忽略格式错误，默认值为`false`,例如为数值字段提供文本值
- `auto_generate_synonyms_phrase_query` ：可选，是否自动生成同义词短语查询，默认为`true`
- `prefix_length`：可选，指定前缀查询的前缀长度。默认值为`0`
- `zero_terms_query`:可选，指示如果 `analyzer` 移除所有标记（例如使用 stop 过滤器时），则不返回文档。
  - `none`：默认，不返回任何文档，`analyzer` 移除所有标记
  - `all`：返回所有文档,类似于`match_all`查询

```json
GET /_search
{
  "query": {
    "match": {
      "message": {
        "query": "this is a test"
      }
    }
  }
}

GET /_search
{
  "query": {
    "match": {
      "message": {
        "query": "to be or not to be",
        "operator": "and",
        "zero_terms_query": "all"
      }
    }
  }
}
```

#### 6.3.4 Match_phrase query

```json
GET /_search
{
  "query": {
    "match_phrase": {
      "message": "this is a test"
    }
  }
}

GET /_search
{
  "query": {
    "match_phrase": {
      "message": {
        "query": "this is a test",
        "analyzer": "my_analyzer"
      }
    }
  }
}
```

#### 6.3.5 Multi_match query

`Multi_match` 查询类型

- `best_fields`：根据最佳字段匹配，使用最佳字段的`_score`
- `most_fields`：根据多个字段匹配，返回多个字段匹配的`_score`结果
- `cross_fields`：将具有相同 analyzer 的字段视为一个大的字段。在任何字段中查找每个词
- `phrase`：在每个字段上使用`match_phrase`查询，并使用最佳字段的`_score`
- `phrase_prefix`：在每个字段上使用`phrase_prefix`查询，并使用最佳字段的`_score`
- `bool_prefix`：在每个字段上使用`match_bool_prefix`查询，并组合每个字段的`_score`

```json
GET /_search
{
  "query": {
    "multi_match" : {
      "query":    "this is a test", 
      "fields": [ "subject", "message" ] 
    }
  }
}

GET /_search
{
  "query": {
    "multi_match" : {
      "query" : "this is a test",
      "fields" : [ "subject^3", "message" ] 
    }
  }
}
```

```json
GET /_search
{
  "query": {
    "multi_match" : {
      "query":      "brown fox",
      "type":       "best_fields",
      "fields":     [ "subject", "message" ],
      "tie_breaker": 0.3
    }
  }
}
```

`tie_breaker`

默认情况下，每个按词项 blended 查询将使用组内任何字段返回的最佳分数。然后当跨组组合分数时，查询使用任何组中的最佳分数。 `tie_breaker` 参数可以改变这两个步骤的行为

- `0.0` ：仅使用最佳字段分数（默认），first_name:will 和 last_name:will 中取出单个最佳分数
- `1.0` : first_name:will 和 last_name:will 的分数相加
- `0.0 < n < 1.0`: 取单个最佳分数加上 `tie_breaker` 乘以其他匹配字段/组的每个分数

#### 6.3.6 Combined_fields query 组合字段查询

`combined_fields query`支持将多个`text`字段的内容视为一个组合字段进行检索。
该查询采用以术语为中心的分析方式：首先将输入字符串拆解为独立术语，随后在各字段中逐个检索这些术语。
当匹配可能跨越标题、摘要和正文等多个文本字段时，该查询方式尤为适用。

查询参数：

- `fields`:必选，字段列表。支持字段通配符模式。仅支持`text`字段，且字段必须使用相同的`analyzer`。
- `query`:必选，查询字符串。
- `operator`:可选，用于解释 query 值中的文本的布尔逻辑，默认值为`OR`。取值范围为`OR`或`AND`
- `minimum_should_match`: 可选，指定必须匹配的`should`子句的最小数量。
- `auto_generate_synonyms_phrase_query` ：可选，是否自动生成同义词短语查询，默认为`true`
- `zero_terms_query`:可选，指示如果 `analyzer` 移除所有标记（例如使用 stop 过滤器时），则不返回文档。
  - `none`：默认，不返回任何文档，`analyzer` 移除所有标记
  - `all`：返回所有文档,类似于`match_all`查询

```json
GET /_search
{
  "query": {
    "combined_fields" : {
      "query":      "database systems",
      "fields":     [ "title", "abstract", "body"],
      "operator":   "and"
    }
  }
}
```

`combined_field`和``multi_match`查询的区别

`combined_fields` 查询提供了一种跨多个 text 字段进行匹配和评分的原则性方法。为了支持这一点，它要求所有字段具有相同的搜索 `analyzer` 。
`multi_match`对单一查询同时处理关键词、数字等不同类型字段，`multi_match`查询可能更为合适。该查询支持`text`与非`text`字段，并可兼容不同`analyzer`的`text`字段。
`multi_match`的`best_fields`和`most_fields`采用以字段为中心的查询。相比之下，`combined_fields`采用以`term`为中心的模式：`operator`和`minimum_should_match`是按`term`而非字段来应用的。

### 6.3.7 intervels query 间隔查询

`intervals` 查询使用匹配规则，这些规则由一小部分定义构成。

- `field`: 搜索字段
- 一级有效规则：
  - match
  - prefix
  - wildcard
  - fuzzy
  - all_of
  - any_of

```json
# 搜索会匹配 my_text 值为 my favorite food is cold porridge 但不会匹配 when it's cold my favorite food is porridge 

POST _search
{
  "query": {
    "intervals" : {
      "my_text" : {
        "all_of" : {
          "ordered" : true,
          "intervals" : [
            {
              "match" : {
                "query" : "my favorite food",
                "max_gaps" : 0,
                "ordered" : true
              }
            },
            {
              "any_of" : {
                "intervals" : [
                  { "match" : { "query" : "hot water" } },
                  { "match" : { "query" : "cold porridge" } }
                ]
              }
            }
          ]
        }
      }
    }
  }
}
```

**`match`规则参数**

匹配分析后的文本

- `query`: 必选，查询字符串
- `max_gaps`: （可选，整数）匹配项之间的最大位置数。距离大于此值的项不匹配。默认为 -1 ，匹配没有宽度限制。为 0 ，则匹配项必须相邻出现
- `ordered`:可选，匹配的词是否按指定顺序出现。默认值为 false
- `analyzer`:可选，分词器
- `filter`: 可选，过滤器
- `use_field`: 可选，指定当前匹配项字段

**`prefix`规则参数**

该模式最多可以扩展以匹配 128 个项

- `prefix`:规则匹配以指定字符集开头的项。
- `analyzer`:可选，分词器
- `use_field`: 可选，指定当前匹配项字段

**`wildcard`规则参数**

该模式最多可以扩展以匹配 128 个项

- `wildcard`:必选，使用通配符模式匹配项。
  - `?`：匹配任何单个字符
  - `*`：匹配零个或多个字符
- `analyzer`:可选，分词器
- `use_field`: 可选，指定当前匹配项字段

**`fuzzy`规则参数**

匹配与指定词相似、在Fuzziness定义的`edit distance`距离范围内的词，该模式最多可以扩展以匹配 128 个项

- `term`:必选，要匹配的词
- `prefix_length`:可选，创建扩展时保留开头的字符数，默认0。
- `transpositions`:可选，指定`edit`是否包含相邻字符交换，默认为`false`。
- `fuzziness`:可选，字符串，指定最大`edit distance`，默认`auto`。
- `analyzer`:可选，分词器
- `use_field`: 可选，指定当前匹配项字段

**`all_of`规则参数**

返回跨越所有组合规则的匹配项

- `intervals`:必选，规则列表
- `max_gaps`: （可选，整数）匹配项之间的最大位置数。距离大于此值的项不匹配。默认为 -1 ，匹配没有宽度限制。为 0 ，则匹配项必须相邻出现
- `ordered`:可选，匹配的词是否按指定顺序出现。默认值为 false
- `filter`: 可选，过滤器

**`one_of`规则参数**

返回跨越所有组合规则的匹配项

- `intervals`:必选，规则列表
- `max_gaps`: （可选，整数）匹配项之间的最大位置数。距离大于此值的项不匹配。默认为 -1 ，匹配没有宽度限制。为 0 ，则匹配项必须相邻出现
- `ordered`:可选，匹配的词是否按指定顺序出现。默认值为 false
- `filter`: 可选，过滤器

**`filter`规则**

- `after`: 可选，用于返回符合过滤规则中某个间隔之后的间隔查询。
- `before`: 可选，用于返回符合过滤规则中某个间隔之前的间隔查询。
- `containing`: 可选，用于返回包含过滤规则中某个间隔的间隔查询。
- `contained_by`: 可选，用于返回被过滤规则中某个间隔包含的间隔查询。
- `not_containing`: 可选，用于返回不包含过滤规则中某个间隔的间隔查询。
- `not_contained_by`: 可选，用于返回不被过滤规则中某个间隔包含的间隔查询。
- `overlapping`: 可选，用于返回与过滤规则中某个间隔重叠的间隔查询。
- `not_overlapping`: 可选，用于返回与过滤规则中某个间隔不重叠的间隔查询。
- `script`: 可选，用于返回匹配文档的脚本。必须返回布尔值， `true` 或 `false` 。

```json
POST _search
{
  "query": {
    "intervals" : {
      "my_text" : {
        "match" : {
          "query" : "hot porridge",
          "max_gaps" : 10,
          "filter" : {
            "not_containing" : {
              "match" : {
                "query" : "salty"
              }
            }
          }
        }
      }
    }
  }
}
```

**注意**：间隔查询始终最小化间隔，以保证间隔查询可以线性运行。

```json
# 查询 "the big bad wolf",查询不到,any_of规则中big和big bad是重叠的，只能匹配小的间隔big
POST _search
{
  "query": {
    "intervals" : {
      "my_text" : {
        "all_of" : {
          "intervals" : [
            { "match" : { "query" : "the" } },
            { "any_of" : {
                "intervals" : [
                    { "match" : { "query" : "big" } },
                    { "match" : { "query" : "big bad" } }
                ] } },
            { "match" : { "query" : "wolf" } }
          ],
          "max_gaps" : 0,
          "ordered" : true
        }
      }
    }
  }
}
# 应该明确在上一层查询
POST _search
{
  "query": {
    "intervals" : {
      "my_text" : {
        "any_of" : {
          "intervals" : [
            { "match" : {
                "query" : "the big bad wolf",
                "ordered" : true,
                "max_gaps" : 0 } },
            { "match" : {
                "query" : "the big wolf",
                "ordered" : true,
                "max_gaps" : 0 } }
           ]
        }
      }
    }
  }
}
```

### 6.4 compound query 复合查询

#### 6.4.1 bool query

默认查询用于组合多个叶查询子句或复合查询子句，包括`must`、`should`、`must_not`、`filter`子句。`must`和`should`子句的评分结果会进行合并计算——匹配子句数量越多，评分越高；而`must_not`及`filter`子句则在过滤上下文中执行。

`msut`: 必须匹配的子句，匹配的文档评分越高。
`should`: 应该匹配的子句，匹配的文档评分越高。
`must_not`: 必须不匹配的子句，匹配的文档评分返回为0。
`filter`:`filter`子句对查询结果评分没有影响，评分结果返回为0，仅用于过滤结果。
`minimum_should_match`: 指定`should`子句的最小匹配数量，如果`bool`查询至少有一个`should`子句，没有`must`和`filter`子句，默认为1，否则为默认值为0

```json
POST _search
{
  "query": {
    "bool" : {
      "must" : {
        "term" : { "username" : "张三" }
      },
      "filter": {
        "term" : { "tags" : "小学生" }
      },
      "must_not" : {
        "range" : {
          "age" : { "gte" : 18, "lte" : 5 }
        }
      },
      "should" : [
        { "term" : { "class" : "三年级" } },
        { "term" : { "class" : "一年级" } }
      ],
      "minimum_should_match" : 1,
      "boost" : 1.0
    }
  }
}

GET _search
{
  "query": {
    "bool": {
      "filter": {
        "term": {
          "status": "active"
        }
      }
    }
  }
}
```

`named query`

每个查询在其顶层定义中接受一个`_name`。您可通过命名查询功能，追踪哪些查询与返回的文档相匹配。若使用命名查询，响应结果将包含每个匹配结果的`matched_queries`属性。

`_name`在单个请求中被视为唯一，否则会报错

```json
GET /_search
{
  "query": {
    "bool": {
      "should": [
        {
          "term": {
            "Category": {
              "value": "001",
              "_name": "cateogry"
            }
          }
        },
        {
          "term": {
            "EffectivenessDic": {
              "value": "XA01",
              "_name": "effective"
            }
          }
        }
      ],
      "filter": {
        "match": {
          "Title": {
            "query": "fang",
            "_name": "test"
          }
        }
      }
    }
  }
}

response 

{
  "took": 9,
  "timed_out": false,
  "_shards": {
    "total": 6,
    "successful": 6,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 7,
      "relation": "eq"
    },
    "max_score": 8.043718,
    "hits": [
      {
        "_index": "chl",
        "_id": "204",
        "_score": 8.043718,
        "_source": {
          "Gid": "204",
          "Title": "fang test create 索引单条数据_204",          
          "EffectivenessDic": [
            "XA01",
            "XA0105"
          ],
          "Category": [
            "001",
            "00106"
          ],        
          "FullText": "fang test create 索引单条数据_204"
        },
        "matched_queries": [
          "effective",
          "test",
          "cateogry"
        ]
      }
      ...
    ]
  }
}

```

#### 6.4.2 boosting query

`boosting query`用于`positive`提升或`nagative`降低查询子句的得分。

- `positive`：必选，用于提升查询子句的得分。
- `negative`：必选，用于降低查询子句的得分。
  - 1.获取查询子句的相关性得分
  - 2.将得分乘以`negative_boost`
- `negative_boost`：可选，用于降低查询子句的得分。默认为1.0，值为0 ~ 1。

```json

GET /_search
{
  "query": {
    "boosting": {
      "positive": {
        "term": {
          "title": "苹果"
        }
      },
      "negative": {
        "term": {
          "description": "酸 甜 水果"
        }
      },
      "negative_boost": 0.5
    }
  }
}
```

#### 6.4.3 constant_score query

一种封装其他查询的查询语句，但会在过滤器上下文中执行该查询。所有匹配文件均被赋予相同的恒定_score评分。

- `filter`: 必选，过滤器上下文中的查询子句。
- `boost`: 可选，匹配文档的评分。默认为1.0。

```json
GET /_search
{
  "query": {
    "constant_score": {
      "filter": {
        "term": { "username": "fang" }
      },
      "boost": 1.2
    }
  }
}
```

#### 6.4.4 dis_max query

该查询可接受多个查询条件，并返回与任一查询子句匹配的文档。与`bool`查询结合所有匹配查询的得分不同，`dis_max`查询仅采用单个最佳匹配查询子句的得分。

- `queries`: 必选，查询子句列表。
- `tie_breaker`: 可选，用于计算得分。默认为0。

通过tie_breaker参数值，可对多字段均含相同`term`的文档赋予更高相关性评分，而仅在最佳字段中出现该`term`的文档则评分较低。需注意，此机制与多字段中存在两个不同`term`的情况存在区分。

```json
GET /_search
{
  "query": {
    "dis_max": {
      "queries": [
        { "term": { "title": "Quick pets" } },
        { "term": { "body": "Quick pets" } }
      ],
      "tie_breaker": 0.7
    }
  }
}
```

若某份文档符合多项`clause`，则`dis_max`查询将按以下方式计算该文档的相关性得分：

1.取匹配子句中得分最高的相关性评分。
2.将其他匹配`clause`的得分乘以`tie_breaker`值。
3.将最高分值加至乘积分数中。
若`tie_breaker`值大于0.0，则所有匹配`clause`均计入，但得分最高的`clause`权重最高。

#### 6.4.5 function_score query

使用函数修改主查询返回的分数，当评分函数计算成本较高且仅需对经过筛选的文档集进行评分时，该方法具有实用价值。

- `functions`: 必选，函数列表。支持多个匹配项
- `function_score`: 函数评分类型
  - `script_score`: 可选，脚本评分函数。
  - `weight`: 可选，函数的权重。默认为1.0。
  - `random_score`: 可选，随机评分函数。
  - `field_value_factor`: 可选，字段值因子函数。
  - `linear`: 可选，线性函数。
  - `exp`: 可选，指数函数。
- `weight`: 可选，函数的权重。默认为1.0。
- `score_mode`:
  - `multiply`: 将函数得分与查询得分相乘。
  - `sum`:  将函数得分与查询得分相加。
  - `avg`:   各单项评分将通过加权平均法进行合并。例如，若两个函数返回的分数分别为1和2，且其相应权重分别为3和4，则其分数将按(1*3+2*4)/(3+4)的方式进行组合计算，而非(1*3+2*4)/2
  - `first`: 仅使用第一个函数得分。
  - `max`:   使用最高函数得分。
  - `min`:   使用最低函数得分。
- `boost_mode`:
  - `multiply`: 将函数得分与查询得分相乘。默认值。
  - `replace`:  仅使用函数得分。
  - `sum`:   将函数得分与查询得分相加。
  - `avg`:   各单项评分将通过加权平均法进行合并。
  - `max`:   取函数得分与查询得分的最高分。
  - `min`:   取函数得分与查询得分的最低分。
- `max_boost`:参数将新评分限制在不超过特定阈值范围内
- `min_score`:最小评分阈值，默认情况下，修改评分不会改变匹配的文档。为排除不符合特定评分阈值的文件

```json
GET /_search
{
  "query": {
    "function_score": {
      "query": { "match_all": {} },
      "boost": "5",
      "random_score": {}, 
      "boost_mode": "multiply"
    }
  }
}

GET /_search
{
  "query": {
    "function_score": {
      "query": { "match_all": {} },
      "boost": "5", 
      "functions": [
        {
          "filter": { "match": { "test": "bar" } },
          "random_score": {}, 
          "weight": 23
        },
        {
          "filter": { "match": { "test": "cat" } },
          "weight": 42
        }
      ],
      "max_boost": 42,
      "score_mode": "max",
      "boost_mode": "multiply",
      "min_score": 42
    }
  }
}
```

### 6.5 span query 跨度查询

跨度查询是一种低级位置查询，可为指定术语的顺序与邻近性提供专家级控制。这些工具通常用于对法律文件或专利实施高度特定的查询操作。
跨度查询不能与非跨度查询混合使用（`span_multi`查询除外）

### 6.5.1 span_term query

该`term`等同于查询项，但用于其他跨度查询场景。

```json
GET /_search
{
  "query": {
    "span_term" : { "user.id" : { "term" : "kimchy", "boost" : 2.0 } }
  }
}
```

### 6.5.2 span_field_masking query

支持跨不同字段进行`span-near`或`span-or`等查询操作。

```json
查找包含短语 "quick brown" 和词 "fox" 的文档，"fox"可以是词根的多种形式。
这两个短语之间的最大距离为 5 个词。
"quick brown" 和 "fox" 的出现顺序不重要。

GET /_search
{
  "query": {
    "span_near": {
      "clauses": [
        {
          "span_term": {
            "text": "quick brown"
          }
        },
        {
          "span_field_masking": {
            "query": {
              "span_term": {
                "text.stems": "fox"
              }
            },
            "field": "text"
          }
        }
      ],
      "slop": 5,
      "in_order": false
    }
  }
}

```

### 6.5.3 span_first query

接受另一种跨度查询，其匹配项必须出现在字段的前N个位置内。

- `end`:指定匹配项必须出现在字段的前N个位置内。默认为1。

```json
查找包含 user.id 字段值为 "kimchy" 的文档，且该字段值必须出现在前3个位置内
GET /_search
{
  "query": {
    "span_first": {
      "match": {
        "span_term": { "user.id": "kimchy" }
      },
      "end": 3
    }
  }
}
```

### 6.5.4 span_multi query

用于包裹`term`、`range`、`prefix`、`wildcard`、`regexp`或`fuzzy`查询

查询匹配的词条数量超过了布尔查询的限制（默认为 4096），`span_multi` 查询将触发过多子句失败

```json
GET /_search
{
  "query": {
    "span_multi": {
      "match": {
        "prefix": { "user.id": { "value": "ki", "boost": 1.08 } }
      }
    }
  }
}
```

### 6.5.5 span_near query

支持多跨度查询，其匹配项必须彼此处于指定距离范围内，并可保持相同顺序。

- `clauses`: 必选，跨度查询列表。支持多个匹配项
- `slop`: 可选，匹配项之间的最大距离。默认为0
- `in_order`: 可选，匹配项是否必须按顺序出现。默认为true

```json
GET /_search
{
  "query": {
    "span_near": {
      "clauses": [
        { "span_term": { "field": "value1" } },
        { "span_term": { "field": "value2" } },
        { "span_term": { "field": "value3" } }
      ],
      "slop": 12,
      "in_order": false
    }
  }
}
```

### 6.5.6 span_not query

接受两种跨度查询，匹配include的SpanQuery, 且不能重叠匹配exclude的SpanQuery

- `include`: 必选，包含跨度查询。
- `exclude`: 必选，排除跨度查询。
- `pre`:在包含跨度之前设置的标记数量不能与排除跨度重叠。默认值为 0。
- `post`:在包含跨度之后设置的标记数量不能与排除跨度重叠。默认值为 0。
- `dist`:在包含跨度范围内设置的标记数量不能与排除跨度重叠。默认值为 0。

`召回逻辑如下:`

`召回候选集`
使用include的SpanQuery召回全部命中文档作为候选集.

`过滤阶段1`
使用`exclude`的`SpanQuery`对候选集中的文档做过滤, 若候选文档没有命中`exclude`的`SpanQuery`, 则直接作为命中文档返回. 若候选文档命中了`exclude`的`SpanQuery`, 则进入下一个过滤阶段.

`过滤阶段2`
对于同时命中了include和exclude的文档, 需要检测include和exclude的命中position是否有重合.  如include命中位置为[0,5], exclude命中位置为[7,8] 则没有重合. include命中位置为[0,5], exclude命中位置为[4,8], 则有重合.对于include和exclude命中位置有重合的文档, 过滤掉.

```json
查找包含 field1 字段值为 "hoya" 的文档,但是排除同时包含短语 "la" 和 "hoya"（且 "la" 在 "hoya" 之前）的文档。
GET /_search
{
  "query": {
    "span_not": {
      "include": {
        "span_term": { "field1": "hoya" }
      },
      "exclude": {
        "span_near": {
          "clauses": [
            { "span_term": { "field1": "la" } },
            { "span_term": { "field1": "hoya" } }
          ],
          "slop": 0,
          "in_order": true
        }
      }
    }
  }
}
```

### 6.5.7 span_or query

匹配其跨度子句的并集

```json
GET /_search
{
  "query": {
    "span_or" : {
      "clauses" : [
        { "span_term" : { "field" : "value1" } },
        { "span_term" : { "field" : "value2" } },
        { "span_term" : { "field" : "value3" } }
      ]
    }
  }
}
```

### 6.5.8 span_containing query

接受一系列跨度查询，但仅返回同时满足第二个跨度查询条件的跨度

用于查找一个短语（小短语）是否完全包含在另一个短语（大短语）中，位置可以没有顺序

召回逻辑
召回候选集
通过little和big取交集作为候选集.

过滤阶段
对于阶段1的召回结果, 需要little匹配的position范围在big的匹配范围之内.

对于下面的例子, 即要求通过big匹配了"bar"和"baz"的同时, little的"foo"必须出现在"bar"和"baz"的中间.

```json
查找包含 "foo" 的文档，同时这些文档还必须包含 "bar" 和 "baz"，并且这两个词之间的距离不超过 5 个词，且 "bar" 必须在 "baz" 之前

GET /_search
{
  "query": {
    "span_containing": {
      "little": {
        "span_term": { "field1": "foo" }
      },
      "big": {
        "span_near": {
          "clauses": [
            { "span_term": { "field1": "bar" } },
            { "span_term": { "field1": "baz" } }
          ],
          "slop": 5,
          "in_order": true
        }
      }
    }
  }
}

```

### 6.5.9 span_within query

若单个跨度查询的结果所涵盖的范围与其他多个跨度查询返回的范围重叠，则该结果将被返回。

`SpanWithInQuery`单独使用的时候召回逻辑与`SpanContainingQuery`完全一致，并且`SpanWithInQuery`的顺序必须保持一致。 只是匹配位置不同, `SpanContainingQuery`匹配位置用的`big`的, `SpanWithinQuery`匹配位置用的`little`的

`召回逻辑`

`召回候选集`
通过little和big取交集作为候选集.

`过滤阶段`
对于阶段1的召回结果, 需要little匹配的position范围在big的匹配范围之内.

对于下面的例子, 即要求通过big匹配了"a"和"c"的同时, little的"b"必须出现在"a"和"c"的中间.

```json
GET /_search
{
  "query": {
    "span_within": {
      "little": {
        "span_term": { "field1": "b" }
      },
      "big": {
        "span_near": {
          "clauses": [
            { "span_term": { "field1": "a" } },
            { "span_term": { "field1": "c" } }
          ],
          "slop": 5,
          "in_order": true
        }
      }
    }
  }
}
```

### 6.6 scroll query

- `size`:参数用于配置每次结果批次返回的最大命中数
- `scroll`:参数用于配置滚动上下文保持打开的时间。例如，`scroll=1m`表示滚动上下文将保持打开状态1分钟。只需足够处理上一批结果的时间。
- `scroll_id`:在请求间可能发生变化，应使用最近接收到的`scroll_id`

**重要**:不再推荐使用滚动API进行深度分页。若需在分页超过10,000条结果时保持索引状态，请使用带有时间点（PIT）的search_after参数

```json
# 获取初始scroll_id
POST: /_search?scroll=2m&pretty=true
{
    "query": {
        "term": {
            "Category": {
                "value": "015"
            }
        }
    },
    "size": 10,
    "track_total_hits": true
}

# 使用返回的scroll_id获取下一批数据
POST: /_search/scroll?pretty=true
{
    "scroll": "2m",
    "scroll_id": "scroll_id_value"
}
```

***注意**：为防止因打开过多scroll而引发的问题，用户不得打开超过一定限制的scroll。默认情况下，打开的scroll的最大数量为500。此限制可通过 `search.max_open_scroll_context` 集群设置进行更新。

```json
# 查看开启的检索上下文数量
GET /_nodes/stats/indices/search

#查看 search.max_open_scroll_context
GET /_cluster/settings?include_defaults=true

在结果中搜索max_open_scroll_context
```

当滚动超时时间超过设定值时，搜索上下文将自动清除。保持滚动条开启会消耗资源，因此应通过clear-scroll API在停止使用滚动时立即清除滚动条。

```json
# 清除scroll_id
DELETE: /_search/scroll?pretty=true
{
    "scroll_id": [
      "scroll_id_value"
    ]
}

# 清除所有scroll_id
DELETE /_search/scroll/_all
```

### 6.7 joining query

- `Nested query`:嵌套查询
- `Has Child query`:子文档查询
- `Has Parent query`:父文档查询
- `Parent Id query`:父文档ID查询

将`search.allow_expensive_queries`设置为`false`，则不会执行连接查询。

#### 6.7.1 nested query

`nested`类型字段用于对对象数组进行索引，其中每个对象都可以作为独立文档进行查询
嵌套查询会像对单独文档进行索引那样对嵌套字段对象进行搜索。如果某个对象与搜索条件匹配，那么嵌套查询就会返回其根级父文档。

- `path`: 嵌套字段名称
- `query`: 查询条件，如果某个对象符合搜索条件，嵌套查询将返回其根级父文档。
- `score_mode`: 分数模式，`avg`、`sum`、`max`、`min`、`none`，默认`avg`
- `ignore_unmapped`: 是否忽略未映射的嵌套字段，并不返回任何文档而直接返回错误信息。默认`false`

`注意：`如果在嵌套查询中运行`script query`，那么您只能访问嵌套文档中的文档值，而无法访问父文档或根文档中的值。

```json
1.索引设置
PUT /my-index-000001
{
  "mappings": {
    "properties": {
      "obj1": {
        "type": "nested"
      }
    }
  }
}

2.查询
GET /my-index-000001/_search
{
  "query": {
    "nested": {
      "path": "obj1",
      "query": {
        "bool": {
          "must": [
            { "match": { "obj1.name": "blue" } },
            { "range": { "obj1.count": { "gt": 5 } } }
          ]
        }
      },
      "score_mode": "avg"
    }
  }
}
```

`multi level nested query`

```json
1.设置索引mapping

PUT /employees
{
  "mappings": {
    "properties": {
      "employee": {
        "type": "nested",
        "properties": {
          "name": {
            "type": "text"
          },
          "mobile": {
            "type": "nested",
            "properties": {
              "make": {
                "type": "text"
              },
              "model": {
                "type": "text"
              }
            }
          }
        }
      }
    }
  }
}

GET /employees/_search
{
  "query": {
    "nested": {
      "path": "employee",
      "query": {
        "nested": {
          "path": "employee.mobile",
          "query": {
            "bool": {
              "must": [
                { "match": { "employee.mobile.make": "apple" } },
                { "match": { "employee.mobile.model": "iPhone 18" } }
              ]
            }
          }
        }
      }
    }
  }
}
```

`注意：`如果一个`nested query`与文档中的一个或多个嵌套对象相匹配，那么它就会将该文档视为一个匹配结果返回。即便文档中的其他嵌套对象与查询不匹配，这种情况依然适用。在使用包含内部`must_not`子句的嵌套查询时，请务必牢记这一点。

#### 6.7.2 has child query

在单个索引内的文档之间可以存在关联字段关系。`has child`查询返回其子文档与指定查询匹配的父文档

因为执行了连接操作，所以`has_child`查询的效率比其他查询要低。随着指向唯一父文档的匹配子文档数量的增加，其性能会下降。在搜索中，每次使用`has_child`查询都会显著增加查询时间。

- `type`: 连接类型，例如`child`
- `query`: 查询条件，匹配子文档
- `max_children`: 对于返回的父文档而言，允许匹配的子文档的最大数量。
- `min_children`: 对于返回的父文档而言，必须满足的子文档最小匹配数量要求。
- `score_mode`: 分数模式，`avg`、`sum`、`max`、`min`、`none`，默认`avg`
- `ignore_unmapped`: 是否忽略未映射的嵌套字段，并不返回任何文档而直接返回错误信息。默认`false`

```json
1.索引设置mapping
PUT /my-index-000001
{
  "mappings": {
    "properties": {
      "my-join-field": {
        "type": "join",
        "relations": {
          "parent": "child"
        }
      }
    }
  }
}

2.child query
GET /_search
{
  "query": {
    "has_child": {
      "type": "child",
      "query": {
        "match_all": {}
      },
      "max_children": 10,
      "min_children": 2,
      "score_mode": "min"
    }
  }
}
```

`sorting`

`has_child`查询的结果进行排序不能使用标准的`sort`选项，可以使用`function_score query`，并使用`_score`排序

```json
GET /_search
{
  "query": {
    "has_child": {
      "type": "child",
      "query": {
        "function_score": {
          "script_score": {
            "script": "_score * doc['click_count'].value"
          }
        }
      },
      "score_mode": "max"
    }
  }
}
```

#### 6.7.3 has parent query

在单个索引内的文档之间可以存在关联字段关系。`has parent`查询则返回其父文档与指定查询匹配的子文档。

因为执行了连接操作，所以`has_parent`查询的效率比其他查询要低。随着指向唯一父文档的匹配子文档数量的增加，其性能会下降。在搜索中，每次使用`has_parent`查询都会显著增加查询时间。

- `parent_type`: 连接类型，例如`parent`
- `query`: 查询条件，匹配子文档
- `score_mode`: 分数模式，`avg`、`sum`、`max`、`min`、`none`，默认`avg`
- `ignore_unmapped`: 是否忽略未映射的嵌套字段，并不返回任何文档而直接返回错误信息。默认`false`

```json
1.索引设置mapping
PUT /my-index-000001
{
  "mappings": {
    "properties": {
      "my-join-field": {
        "type": "join",
        "relations": {
          "parent": "child"
        }
      },
      "tag": {
        "type": "keyword"
      }
    }
  }
}

2.parent query
GET /my-index-000001/_search
{
  "query": {
    "has_parent": {
      "parent_type": "parent",
      "query": {
        "term": {
          "tag": {
            "value": "Elasticsearch"
          }
        }
      }
    }
  }
}
```

`sorting`

`has_parent`查询的结果进行排序不能使用标准的`sort`选项，可以使用`function_score query`，并使用`_score`排序

```json
GET /_search
{
  "query": {
    "has_parent": {
      "parent_type": "parent",
      "score": true,
      "query": {
        "function_score": {
          "script_score": {
            "script": "_score * doc['view_count'].value"
          }
        }
      }
    }
  }
}
```

#### 6.7.4 parent id query

索引设置

`parent id`查询索引`mapping`字段必须包含`"type": "join"`，并且`"relations"`字段必须包含父文档和子文档的关联关系。

- `type`: 用于`join`字段所映射的子关系的名称
- `id`: 父文档的`id`
- `ignore_unmapped`: 是否忽略未映射的嵌套字段，并不返回任何文档而直接返回错误信息。默认`false`

```json
1.索引设置mapping
PUT /my-index-000001
{
  "mappings": {
    "properties": {
      "my-join-field": {
        "type": "join",
        "relations": {
          "my-parent": "my-child"
        }
      }
    }
  }
}

2. 索引数据
PUT /my-index-000001/_doc/1?refresh
{
  "text": "This is a parent document.",
  "my-join-field": "my-parent"
}

PUT /my-index-000001/_doc/2?routing=1&refresh
{
  "text": "This is a child document.",
  "my-join-field": {
    "name": "my-child",
    "parent": "1"
  }
}

3. parent id query
GET /my-index-000001/_search
{
  "query": {
      "parent_id": {
          "type": "my-child",
          "id": "1"
      }
  }
}
```

### 6.8 特殊查询

#### 6.8.1 script query

`script query`允许使用脚本计算相关性得分。

- `script`: 脚本，例如`doc['Category'].size() > 0 && doc['Category'].value == params.category`
- `lang`: 脚本语言，默认`painless`
- `params`: 脚本参数，例如`{ "category": '001' }`

```json
GET /_search
{
  "query": {
    "script": {
      "script": {
        "source": "doc['Category'].size() > 0 && doc['Category'].value == params.category",
        "params": {
          "factor": "001"
        }
      }
    }
  }
}
```

### 6.9 常用查询设置

#### 6.9.1 排序字段

特殊字段名称

- `_score`：按分数排序
- `_doc`：按索引顺序排序，`_doc`字段作为最高效的排序方式，在滚动查询时尤为实用。

使用`format`参数可为`date`和`date_nanos`字段的排序值指定日期格式。

`order` 参数：

- `asc`：升序
- `desc`：降序

```json
GET /index_name/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "Category": {
        "order": "desc"
      }
    }
  ]
}

# 按日期format排序

GET /index_name/_search
{
  "sort" : [
    { "CreateDate" : {"format": "strict_date_optional_time_nanos"}}
  ],
  "query" : {
    "match_all" : {}
  }
}
```

`mode`

Elasticsearch支持按数组或多值字段进行排序。`mode`选项用于指定文档所属数组的排序值。

升序排序的默认排序方式为最小值`min`——选取最低数值。

降序排序的默认排序方式为最大值`max`——选取最高数值。

`mode`参数：

- `min`：最小值
- `max`：最大值
- `sum`：总和，只适用于数字数组字段
- `avg`：平均值，只适用于数字数组字段
- `median`：中位数，只适用于数字数组字段

```json
GET /index_name/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "Category": {
        "order": "desc",
        "mode": "min"
      }
    }
  ]
}
```

`numeric_type`

对于数值字段，还可通过numeric_type选项实现类型转换。

该选项支持["double"、"long"、"date"、"date_nanos"]等类型，特别适用于需要跨多个数据流或索引进行搜索的场景，当排序字段映射方式不同时，该选项能有效提升搜索效率。

**注意**:为避免数值溢出，日期转换为`date_nanos`时，1970年之前和2262年之后的日期无法进行转换，因为纳秒以long类型表示。

```json
# numeric_type 对long字段进行转换排序
POST /index_long,index_double/_search
{
   "sort" : [
      {
        "field" : {
            "numeric_type" : "double"
        }
      }
   ]
}

# numeric_type对日期字段进行转换排序
POST /index_date,index_long/_search
{
   "sort" : [
      {
        "field" : {
            "numeric_type" : "date_nanos"
        }
      }
   ]
}
```

Elasticsearch还支持对嵌套对象内的字段进行排序。

- path: 要排序的嵌套对象。实际排序字段必须是该嵌套对象内的直接字段。当按嵌套字段排序时，此字段为必填项
- filter: 用于匹配嵌套路径中的内部对象，以便其字段值在排序时被纳入考量。常见做法是在嵌套过滤器或查询中重复使用该`query`/`filter`。默认情况下未激活任何过滤器。
- max_children: 选择排序值时，每个根文档可考虑的最大子项数量。默认为无限。
- nested: 与顶层嵌套相同，但适用于当前嵌套对象内的另一嵌套路径。

```json
POST /_search
{
   "query" : {
      "term" : { "product" : "chocolate" }
   },
   "sort" : [
       {
          "offer.price" : {
             "mode" :  "avg",
             "order" : "asc",
             "nested": {
                "path": "offer",
                "filter": {
                   "term" : { "offer.color" : "blue" }
                }
             }
          }
       }
    ]
}
```

`missing`

用于指定缺失排序字段的文档应如何处理

- `_last`：将缺失字段值的文档排在最后，默认值
- `_first`：将缺失字段值的文档排在最前

```json

GET /index_name/_search
{
  "sort" : [
    { "price" : {"missing" : "_last"} }
  ],
  "query" : {
    "term" : { "product" : "chocolate" }
  }
}

```

`script sort`

```json
GET /_search
{
  "query": {
    "term": { "user": "kimchy" }
  },
  "sort": {
    "_script": {
      "type": "number",
      "script": {
        "lang": "painless",
        "source": "doc['field_name'].value * params.factor",
        "params": {
          "factor": 1.1
        }
      },
      "order": "asc"
    }
  }
}
```

#### 6.9.2 查询指定字段

- `fields`：指定返回字段，推荐采用`fields`选项，因其能同时调取文档数据和索引映射
- `_source`：指定返回字段，默认返回所有字段

##### 6.9.2.1 fields

`fields` 优势：

- 以标准化方式返回映射类型匹配的字段
- 支持多字段及字段别名
- 格式化日期与空间数据类型
- 检索运行时字段值
- 返回脚本在索引时间点计算的字段
- 通过查找运行时字段从相关索引中返回字段
- 其他映射选项同样适用，包括`ignore_above`、`ignore_malformed`和`null_value`

```json
GET /index_name/_search
{
  "query": {
    "match_all": {}
  },
  "fields": [
    "Category",
    "CreateDate",
    "http.response.*",
    {
      "field": "UpdateTime",
      "format": "epoch_millis" 
    }
  ],
  "_source": false
}

响应结果：
{
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
      {        
        "fields" : {
          "Category":["001"],
          "CreateDate":["2025-01-02 00:00:00"],
          "UpdateTime" : [
            "4098435132000"
          ],
          "http.response.bytes": [
            1070000
          ],
          "http.response.status_code": [
            200
          ]
        }
      }
    ]
  }
}

```

**注意**:
默认情况下，当请求`fields`选项使用通配符模式（如*）时，系统不会返回文档元数据字段（如`_id`或`_index`）。但若通过字段名明确请求，则可获取`_id`、`_routing`、`_ignored`、`_index`和版本号等元数据字段。

`fields response`

`fields`响应始终会返回每个字段的值数组，即使`_source`中仅包含单个值。这是因为Elasticsearch没有专门的数组类型，且`fields`可包含多个值。`fields`参数也无法保证数组值按特定顺序返回。

`Nested fields response`

`nested`字段的响应机制与普通对象字段略有不同。普通对象字段中的叶级值会以扁平列表形式返回，而`nested`字段中的值则会进行分组处理，以保持原始嵌套数组中各对象的独立性。对于嵌套字段数组中的每个条目，其值同样会以扁平列表形式返回——除非父级嵌套对象内部存在其他嵌套字段，此时需要对更深层的嵌套字段重复上述处理流程。

```json
# 索引数据
PUT my-index-000001/_doc/1?refresh=true
{  
  "user" : [
    {
      "first" : "John",
      "last" :  "Smith"
    },
    {
      "first" : "Alice",
      "last" :  "White"
    }
  ]
}

# nested fields查询
POST my-index-000001/_search
{
  "fields": ["*"],
  "_source": false
}

# 响应结果
{  
  "hits": {
    "total": {
      "value": 1,
      "relation": "eq"
    },
    "max_score": 1.0,
    "hits": [{      
      "fields": {        
        "user": [{
            "first": ["John"],
            "last": ["Smith"]
          },
          {
            "first": ["Alice"],
            "last": ["White"]
          }
        ]
      }
    }]
  }
}

```

`unmapped fields`

默认情况下，`fields`参数仅返回已映射字段的值。但Elasticsearch支持将未映射字段存储在source字段中，例如将`dynamic`字段映射设为`false`，或使用`enabled:false`的对象字段。这些选项会禁用对象内容的解析和索引功能。

```json
# Disable all mappings
PUT my-index
{
  "mappings": {
    "enabled": false 
  }
}

# include_unmapped设置为true，可返回未映射字段的值
POST my-index/_search
{
  "fields": [    
    {
      "field": "session_data.object.*",
      "include_unmapped" : true 
    }
  ],
  "_source": false
}

# 响应结果
{  
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
      {
        "fields" : {
          "session_data.object.some_field": [
            "some_value"
          ]
        }
      }
    ]
  }
}

```

`ignored field values`

响应中的`fields`部分仅返回索引时有效的值。若搜索请求要求从字段中获取某些因格式错误或过大而被忽略的值，则这些值将单独返回至`ignored_field_values`字段值部分。

```json
# 设置ignore_above为2，忽略长度超过2的字符串
PUT my-index
{
  "mappings": {
    "properties": {
      "my-small" : { "type" : "keyword", "ignore_above": 2 }      
    }
  }
}

# 索引数据
PUT my-index/_doc/1?refresh=true
{
  "my-small": ["ok", "bad"]  
}

# 使用fileds参数查询
POST my-index/_search
{
  "fields": ["my-*"],
  "_source": false
}

# 响应结果
{
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "hits" : [
      {
        "_ignored" : [ "my-small"],
        "fields" : {          
          "my-small": ["ok"]
        },
        "ignored_field_values" : {
          "my-small": ["bad"]
        }
      }
    ]
  }
}
```

##### 6.9.2.2 _source

请求体中设置 `_source:false`时，返回结果中不包含 `_source` 字段。

```json
GET /index_name/_search
{
  "_source": false,
  "query": {
    "match_all": {}
  }
}
```

```json
# 指定字段名返回字段
GET /index_name/_search
{
  "_source": ["field1", "field2"],
  "query": {
    "match_all": {}
  }
}

# 使用通配符过滤返回字段
GET /index_name/_search
{
  "_source": ["*Date" ,"*Time"],
  "query": {
    "match_all": {}
  }
}
```

`includes`和`excludes`

```json
# includes和excludes参数可分别指定返回字段和排除字段
GET /index_name/_search
{
  "_source": {
    "includes": ["field1", "field2"],
    "excludes": ["field3"]
  },
  "query": {
    "match_all": {}
  }
}
```

##### 6.9.2.3 其它 `fields`

使用`fields`选项通常是更优选择，除非确实需要强制加载`stored`字段或`docvalue_fields`

`docvalue_fields`

doc values以磁盘存储的列式结构形式保存与`_source`字段相同的值，该结构经过优化，可高效支持排序和聚合操作。由于各字段独立存储，Elasticsearch仅读取请求字段的值，从而避免加载整个`_source`文档。

默认情况下，系统会为支持的字段存储doc values。但`text`字段或`text_annotated`字段不支持文档值。

```json
GET my-index/_search
{
  "query": {
    "match_all": { }
  },
  "docvalue_fields": [
    "user.id",
    "http.response.*", 
    {
      "field": "date",
      "format": "epoch_millis" 
    }
  ]
}
```

**注意**:无法通过`docvalue_fields`参数获取嵌套对象的doc values。若指定嵌套对象，系统将返回空数组[]。要访问嵌套字段，请使用`inner_hits`参数的`docvalue_fields`属性。

`stored_fields`

通过使用`store`映射选项来存储单个字段的值,可使用`stored_fields`参数将这些存储值包含在搜索响应中

`stored_fields` 默认关闭该功能通常不推荐。建议改用`source filter`功能，以选择原始源文档中需要返回的子集

- 从文档本身获取的`store`字段值始终以数组形式返回。而像路由（_routing）这样的元数据字段则不会以数组形式返回
- 仅能通过`stored_fields`选项返回叶子字段。若指定对象字段，系统将忽略该字段。
- 单独使用`stored_fields`无法加载嵌套对象中的字段，若字段路径包含嵌套对象，则该存储字段将不返回数据。要访问嵌套字段，必须在`inner_hits`块中使用`stored_fields`。

```json
GET my-index/_search
{
  "stored_fields": [
    "user.id",
    "user.name",
    "user.email"
  ],
  "query": {
    "match_all": { }
  }
}

# 禁用stored_fields 查询
GET /my-index/_search
{
  "stored_fields": "_none_",
  "query": {
    "match_all": { }
  }
}

```

`script_fields`

`script_fields`可作用于未存储的字段（如下文中的价格字段），并允许返回自定义值（即脚本的计算结果）。

```json
GET /_search
{
  "query": {
    "match_all": {}
  },
  "script_fields": {
    "test1": {
      "script": {
        "lang": "painless",
        "source": "doc['price'].value * 2"
      }
    },
    "test2": {
      "script": {
        "lang": "painless",
        "source": "doc['price'].value * params.factor",
        "params": {
          "factor": 2.0
        }
      }
    }
  }
}

# 使用 _source字段
GET /_search
{
  "query": {
    "match_all": {}
  },
  "script_fields": {
    "test1": {
      "script": "params['_source']['message']"
    }
  }
}
```

**注意**:

理解 `doc["my_field"].value` 和 `params["source"]["my_field"]` 之间的区别很重要。使用 doc 关键字，会导致该字段的 terms被加载到内存（缓存），这将加快执行速度，但会增加内存消耗。此外，`doc[...]` 标记仅允许简单的值字段（无法从中返回 json 对象），并且仅适用于未分析或基于单个term的字段。然而，如果可能的话，使用 `doc` 仍然是访问文档值的推荐方式，因为每次使用 `_source` 时都必须加载和解析。使用 `_source` 非常慢。

#### 6.9.3 分页

请勿使用`from`和`size`参数进行深度分页或一次性请求过多结果。

默认情况下，您无法使用`from`和`size`参数来翻阅超过10,000条结果。此限制是 `index.max_result_window` 索引设置中设置的安全措施。如果您需要翻阅超过10,000条结果，请使用`search_after`参数。

- `from`：指定起始位置，默认为0
- `size`：指定返回结果数量，默认为10

```json
GET /index_name/_search
{
  "query": {
    "match_all": {}
  },
  "from": 0,
  "size": 10
}
```

**注意**:Elasticsearch采用Lucene的内部文档ID作为排序分隔符。这些内部文档ID在相同数据的不同副本中可能完全不同。当页面搜索命中时，有时会发现具有相同排序值的文档排序不一致。

`search_after`

使用search_after参数，根据前一页的排序值集合检索下一页结果。

```json
# 使用search_after功能需多次提交相同查询和排序参数的请求。

# 1.初始请求，按日期和tie_breaker_id两个字段对结果排序
GET index_name/_search
{
    "query": {
        "match_all": {}
    },
    "sort": [
        {"date": "asc"},
        {"tie_breaker_id": "asc"}     //已启用doc_values的_id字段副本
    ]
}

响应结果：
{  
  "hits" : {    
    "hits" : [
      ...
      {
        "_index" : "twitter",
        "_id" : "654322",
        "_score" : null,
        "_source" : ...,
        "sort" : [
          1463538855,
          "654322"
        ]
      },
      {
        "_index" : "twitter",
        "_id" : "654323",
        "_score" : null,
        "_source" : ...,
        "sort" : [                                
          1463538857,
          "654323"
        ]
      }
    ]
  }
}

# 2.根据响应的 sort结果的值[1463538857, "654323"]， 使用search_after参数提交请求，重复请求以获取下一页结果
GET index_name/_search
{
    "query": {
        "match": {
            "title": "elasticsearch"
        }
    },
    "search_after": [1463538857, "654323"],
    "sort": [
        {"date": "asc"},
        {"tie_breaker_id": "asc"}
    ]
}
```

若两次请求之间发生刷新，可能导致结果顺序改变，造成跨页面结果不一致。为避免此问题，可创建时间点 Print in Time（PIT）以保存当前索引状态。

`PIT`

**注意**:所有`PIT`(print in time)搜索请求都会自动添加一个名为`_shard_doc`的隐式排序`tiebreaker`字段，该字段也可显式指定。若无法使用PIT，建议在排序时添加`tiebreaker`字段。该字段需为每个文档生成唯一标识。若未设置`tiebreaker`字段，分页结果可能出现遗漏或重复匹配。

```json
# 1. 创建PIT
POST /index_name/_pit?keep_alive=1m

# 2. 使用PIT进行查询
GET /index_name/_search
{
  "size": 10000,
  "query": {
    "match_all" : {}
  },
  "pit": {
    "id":  "46ToAwMDaWR5BXV1aWQyKwZub2RlXzMAAAAAAAAAACoBYwADaWR4BXV1aWQxAgZub2RlXzEAAAAAAAAAAAEBYQADaWR5BXV1aWQyKgZub2RlXzIAAAAAAAAAAAwBYgACBXV1aWQyAAAFdXVpZDEAAQltYXRjaF9hbGw_gAAAAA==", 
    "keep_alive": "1m"
  },
  "sort": [ 
    {"@timestamp": {"order": "asc", "format": "strict_date_optional_time_nanos", "numeric_type" : "date_nanos" }}
  ]
}

响应结果：
{
  "pit_id" : "46ToAwMDaWR5BXV1aWQyKwZub2RlXzMAAAAAAAAAACoBYwADaWR4BXV1aWQxAgZub2RlXzEAAAAAAAAAAAEBYQADaWR5BXV1aWQyKgZub2RlXzIAAAAAAAAAAAwBYgACBXV1aWQyAAAFdXVpZDEAAQltYXRjaF9hbGw_gAAAAA==",   
  "hits" : {   
    "hits" : [      
      {
        "_index" : "my-index-000001",
        "_id" : "FaslK3QBySSL_rrj9zM5",       
        "_source" : ...,
        "sort" : [                                
          "2021-05-20T05:30:04.832Z",
          4294967298                              
        ]
      }
    ]
  }
}

# 3. 使用 search_after 继续进行PIT查询
使用上次搜索的排序值（tiebreaker）作为search_after参数重新执行搜索。若使用PIT，请将pit.id参数设为最新PIT ID。搜索的查询和排序参数必须保持原样。若提供from参数，其值必须为0（默认值）或-1
GET /_search
{
  "size": 10000,
  "query": {
    "match_all" : {}
  },
  "pit": {
    "id":  "46ToAwMDaWR5BXV1aWQyKwZub2RlXzMAAAAAAAAAACoBYwADaWR4BXV1aWQxAgZub2RlXzEAAAAAAAAAAAEBYQADaWR5BXV1aWQyKgZub2RlXzIAAAAAAAAAAAwBYgACBXV1aWQyAAAFdXVpZDEAAQltYXRjaF9hbGw_gAAAAA==", 
    "keep_alive": "1m"
  },
  "sort": [
    {"@timestamp": {"order": "asc", "format": "strict_date_optional_time_nanos","numeric_type" : "date_nanos"}}
  ],
  "search_after": [                                
    "2021-05-20T05:30:04.832Z",
    4294967298
  ],
  "track_total_hits": false                        
}

# 4. 删除PIT
DELETE /_pit
{
    "id" : "46ToAwMDaWR5BXV1aWQyKwZub2RlXzMAAAAAAAAAACoBYwADaWR4BXV1aWQxAgZub2RlXzEAAAAAAAAAAAEBYQADaWR5BXV1aWQyKgZub2RlXzIAAAAAAAAAAAwBYgACBXV1aWQyAAAFdXVpZDEAAQltYXRjaF9hbGw_gAAAAA=="
}
```

`sliced scroll`

默认情况下，首先在分片上进行分割，然后使用_id字段在每个分片上本地进行分割。本地分割遵循公式 slice(doc) = floorMod(hashCode(doc._id), max)。

PIT query API支持更高效的分区策略，且不会出现此问题(控制并行执行的切片查询数量，以避免内存爆炸)。建议使用带有切片的PIT query而非scroll query

另一种避免高成本的方法是利用其他字段的`doc_values`进行切片处理。该字段必须满足以下属性：

- 字段为`numeric`。
- 该字段已启用`doc_values`
- 每个文档的字段的值应仅包含一个值。若文档中指定字段存在多个值，则采用第一个值。
- 每个文档的字段的值应在创建时一次性设定且永不更新。此举可确保每个切片获得确定性结果。
- 字段的基数应设置为较大值。此举可确保每个切片获得的文档数量大致相等。

```json
GET /index_name/_search?scroll=1m
{
  "slice": {
    "field": "@timestamp",
    "id": 0,
    "max": 10
  },
  "query": {
    "match_all": {}
  }
}
```

#### 6.9.4 设置查询结果总数

默认情况下，Elasticsearch会计算匹配查询的文档总数，并将其存储在`hits.total.value`中。若查询匹配的文档数量超过10,000，则`hits.total.value`将返回10,000，`hits.total.relation`将返回`gte`。

若需要获取精确的匹配文档总数，请将`track_total_hits`参数设置为`true`。

```json
GET /_search
{
  "track_total_hits": true,
  "query": {
    "match_all": {}
  }
}
```

#### 6.9.5 filter search result 过滤查询结果

##### 6.9.5.1 boolean filter

`filter` 是`bool query`中的一个子句，可以应用到`response`中的`hits`和`aggregations`。

```json
GET /_search
{
  "query": {
    "match_all": {}
  },
  "filter": {
    "term": {
      "status": "active"
    }
  }
}
```

##### 6.9.5.2 post filter

当使用`post_filter`参数过滤搜索结果时，搜索结果将在聚合计算完成后进行筛选。后置过滤器不会影响聚合结果。

`post_filter`只能应用到`response`中的`hits`

```json
# 当需要在聚合时包含所有颜色的衬衫，然后仅对搜索结果应用颜色过滤器。这正是post_filter的作用

GET /shirts/_search
{
  "query": {
    "bool": {
      "filter": {
        "term": { "brand": "gucci" } 
      }
    }
  },
  "aggs": {
    "colors": {
      "terms": { "field": "color" } 
    },
    "color_red": {
      "filter": {
        "term": { "color": "red" } 
      },
      "aggs": {
        "models": {
          "terms": { "field": "model" } 
        }
      }
    }
  },
  "post_filter": { 
    "term": { "color": "red" }
  }
}

```

##### 6.9.5.3 rescore

`rescore`

重新排序可通过仅对查询和后处理阶段返回的前100至500份文档进行重新排序（采用通常成本更高的次级算法），而非对索引中的所有文档应用成本较高的算法，从而提高精确度。

**注意**:

- 若在重评分查询中指定除`_score`降序排序外的其他显式排序方式，系统将抛出错误。
- 向用户展示分页时，切勿在逐页浏览过程中（通过传递不同值）修改`widnows_size`，否则可能导致顶部搜索结果发生变化，使用户在浏览页面时出现令人困惑的跳转现象。

`rescore_query`

`rescore_query`仅对查询和后处理阶段返回的Top-K结果执行二次查询。每个分片中待检查的文档数量可通过`window_size`参数控制，默认值为10。

默认情况下，原始查询与`rescore_query`的得分会按线性比例组合，生成每份文档的最终得分。原始查询与`rescore_query`的相对权重可通过`query_weight`和`rescore_query_weight`参数分别控制。这两个参数默认值均为1。

```json
GET /_search
{
  "query": {
    "match": {
      "message": "elasticsearch"
    }
  },
  "rescore": {
    "window_size": 50,
    "query": {
      "rescore_query": {
        "match_phrase": {
          "message": {
            "query": "Elasticsearch",
            "slop":  2
          }
        }
      },
      "query_weight": 0.7,
      "rescore_query_weight": 1.2
    }
  }
}
```

`Multiple rescores`

第一个系统获取查询结果后，第二个系统将获取其结果，依此类推。第二次重评分将“参考”第一次重评分的排序结果，因此可以在第一次重评分中设置较大的窗口范围，以便将文档纳入第二次重评分的较小窗口范围内。

```json
POST /_search
{
   "query" : {
      "match" : {
         "message" : {            
            "query" : "the quick brown"
         }
      }
   },
   "rescore" : [ {
      "window_size" : 100,
      "query" : {
         "rescore_query" : {
            "match_phrase" : {
               "message" : {
                  "query" : "the quick brown",
                  "slop" : 2
               }
            }
         },
         "query_weight" : 0.7,
         "rescore_query_weight" : 1.2
      }
   }, {
      "window_size" : 10,
      "query" : {
         "score_mode": "multiply",
         "rescore_query" : {
            "function_score" : {
               "script_score": {
                  "script": {
                    "source": "Math.log10(doc.count.value + 2)"
                  }
               }
            }
         }
      }
   } ]
}
```

#### 6.9.6 highlighting 高亮查询

Elasticsearch支持三种高亮方式：`unified`, `plain`, and `fvh` (fast vector highlighter)。您可为每个字段指定所需使用的高亮`type`。

**注意**：高亮工具在提取高亮术语时，无法准确呈现查询的布尔逻辑。因此，对于某些复杂的布尔查询（如嵌套布尔查询、使用`minimum_should_match`等），文档中可能被高亮的部分并不符合查询条件

**`unified highlighter`**

`unified`高亮器采用Lucene统一高亮器。该工具将文本拆分为句子，并运用BM25算法对每个句子进行评分，如同处理语料库中的文档。同时支持精准的短语高亮及多词（模糊、前缀、正则表达式）高亮功能。此为默认高亮器。

**`plain highlighter`**

`plain`高亮器采用标准Lucene高亮器。其试图通过理解词语重要性及短语查询中的任何词语定位标准，来体现查询匹配逻辑。

`plain`高亮器最适合用于单个字段的简单查询匹配。在多个文档中使用复杂查询对大量字段进行高亮时，建议在`postings`字段或`term_vector`字段上使用`unified`高亮器

**`fast vector highlighter`**

`fvh`高亮器采用Lucene Fast Vector Highlighter。适用于映射中`term_vector`设置为`with_positions_offsets`的字段

- 可配合边界扫描器进行定制。
- 需将`term_vector`参数设置为`with_positions_offsets`，该操作会增大索引的存储容量
- 可将多个字段的匹配项合并为一个结果。参见 `matched_fields`
- 可为不同位置的匹配项分配不同权重，例如在高亮显示提升短语匹配优先级的Boosting Query时，可将短语匹配排序置于术语匹配之上

**注意**：

`fvh highlighter`不支持跨行查询。如需跨行查询支持，请尝试其他高亮器，例如`unified highlighter`。

**`offset strategy`**

- `index_options`: 当映射中的`index_options`设置为偏移量时，`unified highlighter`会直接调用这些信息来高亮文档，无需重新分析文本。在处理大字段时尤为重要，因为它无需重新分析文本即可实现高亮。相比使用`term_vectors`，该方法还能节省更多磁盘空间。
- `term_vectors`: 在映射中通过将`term_vector`设为`with_positions_offsets`来提供词向量信息，`unified highlighter`将自动使用`term_vector`对字段进行高亮。该方法运行速度极快，尤其适用于大字段（>1MB）和前缀/通配符等多词查询场景，因其可直接调用各文档的词典。`fvh highlighter`始终采用词向量技术。
- `plain`: 当无其他替代方案时，统一模式会采用此模式。`plain highlighter`始终使用`plain highlighting`功能。

**`highlighting settings`**

高亮显示设置既可全局配置，也可在字段层级进行覆盖。

- `boundary_chars`: 包含每个边界字符的字符串。默认值为`.,!? \t\n`
- `boundary_max_scan`: 边界字符的扫描范围。默认值为20
- `boundary_scanner`: 指定边界扫描器。指定高亮片段的拆分方式：`chars`、`sentence`、`word`。仅适用于`unified highlighter`和`fvh highlighter`。`unified highlighter`默认拆分为句子，`fvh highlighter`器默认拆分为字符。
  - `chars`: 使用`boundary_chars`指定的字符作为高亮边界。`boundary_max_scan`设置控制边界字符的扫描范围。仅适用于`unified highlighter`。
  - `sentence`: 根据Java BreakIterator的判定，在下一句边界处断开高亮片段。可通过`boundary_scannerLocale`指定所用区域设置。
  - `word`: 根据Java BreakIterator的判定，在下一句边界处断开高亮片段。可通过`boundary_scannerLocale`指定所用区域设置。
- `boundary_scanner_locale`: 用于指定搜索句子和单词边界时采用的区域设置。该参数采用语言标签形式，例如`en-US`、`fr-FR`、`ja-JP`。更多详情请参阅`Locale Language Tag`文档。默认值为`Locale.ROOT`。
- `encoder`: 指定代码片段是否采用HTML编码，默认 `default`，表示无编码;`html`表示对代码片段进行转义后再添加高亮标签
- `fields`: 指定要提取高亮的字段。可使用通配符指定字段。使用通配符时，仅`text`、`match_only_text`、 `keyword`字段会被高亮显示。
- `fragmenter`: 指定高亮片段中的文本断行方式：`simple` or `span`，默认`span`。仅适用于`plain`高亮显示
  - `simple`: 将文本分割成大小相同的片段。
  - `span`: 将文本分割为等长片段，但尽量避免在高亮术语之间分割文本。查询短语时非常实用。默认设置。
- `fragment_offset`: 控制高亮起始的边距。仅在使用`fvh`高亮工具时有效。
- `fragment_size`: 高亮片段的字符长度。默认值为100
- `highlight_query`: 高亮显示与搜索查询不同的其他查询结果。此功能在使用重评分查询时尤为实用，因为默认情况下高亮显示不会考虑这些查询。
- `matched_fields`: 通过组合多个字段的匹配结果，可高亮显示单个字段。该功能特别适用于需要以不同方式解析同一字符串的多字段分析场景。所有匹配字段的`term_vector`参数必须设置为`with_positions_offsets`，但仅加载实际进行组合匹配的字段，因此只有该字段能享受`'store':true`优化效果。本功能仅适用于`fvh`高亮器。
- `no_match_size`: 若无匹配片段可高亮显示，该字段起始位置的文本返回量。默认值为0（不返回任何内容）
- `number_of_fragments`: 可返回的最大片段数量。若将片段数量设为0，则不返回任何片段，而是高亮显示并返回整个字段内容。此设置适用于需要高亮显示标题、地址等短文本但无需分段的情况。当`number_of_fragments`为0时，`fragment_size`参数将被忽略。默认值为5。
- `order`: 启用评分模式时，系统将按相关性分数对高亮片段排序。默认情况下，片段会按字段显示顺序输出。选择评分模式后，系统将优先显示最相关的片段。各高亮器采用独立算法计算相关性分数。
- `phrase_limit`: 控制文档中匹配短语的计数上限。防止`fvh`高亮器因分析过多短语而占用过多内存。仅`fvh`高亮器支持该功能。默认值为256。
- `pre_tags`: 与 `post_tags` 一起使用，以定义用于高亮文本的 HTML 标签。默认情况下，高亮文本会用 `<em>` 和 `</em>`标签进行换行。以字符串数组形式指定。
- `post_tags`: 与 `pre_tags` 一起使用，以定义用于高亮文本的 HTML 标签。
- `require_field_match`: 默认仅高亮显示包含查询匹配项的字段。将 `require_field_match` 设置为 `false` 以高亮显示所有字段。默认值为 `true`
- `max_analyzed_offset`:默认情况下，高亮请求分析的最大字符数由 `index.highlight.max_analyzed_offset` 设置中的值限制，当字符数超过此限制时，将返回错误。
- `tags_schema`:设置为使用内置标签模式。该`styled`模式定义了以下`pre_tags`，并将`post_tags`定义为 `</em>`。
- `type`: 高亮工具类型：`unified`、`plain`、`fvh`。默认值为 `unified`。

```json
{
  "highlight": {
    "fields": {
      "NamePy ": {
        "type": "fvh"
      }
    },
    "fragment_size": 100,
    "number_of_fragments": 0,    
    "pre_tags": [
      "<span class='hitClass'>"
    ],
    "post_tags": [
      "</span>"
    ],
    "require_field_match": true
  } 
}

# 指定高亮字段顺序，fields设置为数组

GET /_search
{
  "highlight": {
    "fields": [
      { "title": {} },
      { "text": {} }
    ]
  }
}
```

#### 6.9.7 inner hits 内部命中

`inner hits`：父级-子级关联与嵌套功能支持检索不同层级的匹配文档。

在`Nested`、`has_child`或`has_parent`查询及`filter`中定义`innerHits`参数，可实现内部命中功能。

选项：

- `from`:从返回的常规搜索命中结果中，每个`inner_hits`首次命中位置的偏移量。
- `size`:每次`inner_hits`返回的最大匹配结果数量。默认情况下返回前三个匹配结果。
- `sort`:根据`inner_hits`对内部命中进行排序。默认情况下，按`score`排序。
- `name`:用于响应中特定内层匹配定义的名称。当单次搜索请求中定义多个内层匹配时，该名称非常实用。默认值取决于内层匹配在哪个查询中定义。对于`has_child`查询和`filter`，此名称表示子类型；对于`hasParent`查询和`filter`，表示父类型；对于`nested`查询和`filter`，则表示嵌套路径。

```json

PUT test
{
  "mappings": {
    "properties": {
      "comments": {
        "type": "nested"
      }
    }
  }
}

PUT test/_doc/1?refresh
{
  "title": "Test title",
  "comments": [
    {
      "author": "kimchy",
      "number": 1
    },
    {
      "author": "nik9000",
      "number": 2
    }
  ]
}

POST test/_search
{
  "query": {
    "nested": {
      "path": "comments",
      "query": {
        "match": {"comments.number" : 2}
      },
      "inner_hits": {} 
    }
  }
}

# 响应结果
一个关键默认设置是：inner_hits中返回的匹配结果_source，均以嵌套元数据为基准。因此在示例中，每次嵌套匹配仅返回comments内容，而不会包含该注释所在顶级文档的完整源文件

{  
  "hits": {
    "total" : {
        "value": 1,
        "relation": "eq"
    },    
    "hits": [
      {
        "inner_hits": {
          "comments": { 
            "hits": {
              "total" : {
                  "value": 1,
                  "relation": "eq"
              },
              "max_score": 1.0,
              "hits": [
                {
                  "_index": "test",
                  "_id": "1",
                  "_nested": {
                    "field": "comments",
                    "offset": 1
                  },
                  "_score": 1.0,
                  "_source": {
                    "author": "nik9000",
                    "number": 2
                  }
                }
              ]
            }
          }
        }
      }
    ]
  }
}
```

下面的功能可用于控制`inner_hits`的返回结果：

- `Highlighting`
- `Explain`
- `Search fields`
- `Source filtering`
- `Script fields`
- `Doc value fields`
- `Include versions`
- `Include Sequence Numbers and Primary Terms`

#### 6.9.8 muti search 多索引查询

```json
# 指定多个索引名
GET /my-index1,my-index2/_search
{
  "query": {
    "match_all": {}
  }
}

# 使用通配符
GET /my-index-*/_search
{
  "query": {
    "match_all": {}
  }
}

# 查询所有索引
GET /_search
{
  "query": {
    "match_all": {}
  }
}

GET /_all/_search
{
  "query": {
    "match_all": {}
  }
}

GET /*/_search
{
  "query": {
    "match_all": {}
  }
}
```

`indices_boost`

`indices_boost`设置索引的权重，权重值越高，查询结果中该索引的文档排名越靠前。

```json
GET /_search
{
  "indices_boost": [
    { "my-index1": 1.4 },
    { "my-index2": 1.3 }
  ]
}
```

#### 6.9.9 search template 查询模板

`source`支持与`search API` 请求体相同的参数。`source`也接受 `Mustache` 变量，这来自一个开源项目 mustache.java。
通常 `Mustache` 变量会用双卷括号包住：`{{my-var}}`。当你运行模板搜索时，Elasticsearch 会用参数中的值替换这些变量。
搜索模板必须使用`'lang':'mustache'`。

##### 6.9.9.1 创建查询模板

```json
PUT _scripts/my-search-template
{
  "script": {
    "lang": "mustache",
    "source": {
      "query": {
        "match": {
          "message": "{{query_string}}"
        }
      },
      "from": "{{from}}",
      "size": "{{size}}"
    }
  }
}
```

##### 6.9.9.2 验证查询模板

```json
POST _render/template
{
  "id": "my-search-template",
  "params": {
    "query_string": "hello world",
    "from": 20,
    "size": 10
  }
}

# 内联测试查询模板
POST _render/template
{
    "source": {
      "query": {
        "match": {
          "message": "{{query_string}}"
        }
      },
      "from": "{{from}}",
      "size": "{{size}}"
    },
  "params": {
    "query_string": "hello world",
    "from": 20,
    "size": 10
  }
}
```

##### 6.9.9.3 使用查询模板

模板查询响应结果与search API相同

```json
GET my-index/_search/template
{
  "id": "my-search-template",
  "params": {
    "query_string": "hello world",
    "from": 0,
    "size": 10
  }
}
```

##### 6.9.9.4 运行多个查询模板

```json
GET my-index/_msearch/template
{ }
{ "id": "my-search-template", "params": { "query_string": "hello world", "from": 0, "size": 10 }}
{ }
{ "id": "my-other-search-template", "params": { "query_type": "match_all" }}
```

##### 6.9.9.5 获取指定的查询模板

```json
GET _scripts/my-search-template
```

##### 6.9.9.6 获取所有搜索模板及其他存储脚本

使用集群API

```json
GET _cluster/state/metadata?pretty&filter_path=metadata.stored_scripts
```

##### 6.9.9.7 删除查询模板

```json
DELETE _scripts/my-search-template
```

##### 6.9.9.8 设置默认值

给变量设置默认值

语法：`{{my-var}}{{^my-var}}default value{{/my-var}}`

```json
# from和size 设置默认值
POST _render/template
{
  "source": {
    "query": {
      "match": {
        "message": "{{query_string}}"
      }
    },
    "from": "{{from}}{{^from}}0{{/from}}",
    "size": "{{size}}{{^size}}10{{/size}}"
  },
  "params": {
    "query_string": "hello world"
  }
}
```

##### 6.9.9.9 URL编码

使用`{{#url}}`函数编码url

语法：`{{#url}}http://example.com/{{/url}}`

```json
POST _render/template
{
  "source": {
    "query": {
      "term": {
        "url.full": "{{#url}}{{host}}/{{page}}{{/url}}"
      }
    }
  },
  "params": {
    "host": "http://example.com",
    "page": "hello-world"
  }
}
```

##### 6.9.9.10 串联值

使用 `{{#join}}` 函数将数组值串接成逗号分隔字符串。

语法：`{{#join}}{{my-array}}{{/join}}`

指定分隔符语法：`{{#join delimiter='|'}}{{my-array}}{{/join delimiter='|'}}`

```json
POST _render/template
{
  "source": {
    "query": {
      "match": {
        "user.group.emails": "{{#join}}emails{{/join}}"
      }
    }
  },
  "params": {
    "emails": [ "user1@example.com", "user_one@example.com" ]
  }
}

# 模板输出结果
{
  "template_output": {
    "query": {
      "match": {
        "user.group.emails": "user1@example.com,user_one@example.com"
      }
    }
  }
}
```

指定自定义分隔符

```json
POST _render/template
{
  "source": {
    "query": {
      "range": {
        "user.effective.date": {
          "gte": "{{date.min}}",
          "lte": "{{date.max}}",
          "format": "{{#join delimiter='||'}}date.formats{{/join delimiter='||'}}"
        }
      }
    }
  },
  "params": {
    "date": {
      "min": "2098",
      "max": "06/05/2099",
      "formats": ["dd/MM/yyyy", "yyyy"]
    }
  }
}

# 模板渲染结果
{
  "template_output": {
    "query": {
      "range": {
        "user.effective.date": {
          "gte": "2098",
          "lte": "06/05/2099",
          "format": "dd/MM/yyyy||yyyy"
        }
      }
    }
  }
}
```

##### 6.9.9.11 转换json

使用 `{{#toJson}}` 函数将变量值转换为其 JSON 表示

语法：`{{#toJson}}{{my-var}}{{/toJson}}`

```json
# 转换数组
POST _render/template
{
  "source": "{ \"query\": { \"terms\": { \"tags\": {{#toJson}}tags{{/toJson}} }}}",
  "params": {
    "tags": [
      "prod",
      "es01"
    ]
  }
}

# 模板渲染结果
{
  "template_output": {
    "query": {
      "terms": {
        "tags": [
          "prod",
          "es01"
        ]
      }
    }
  }
}

# 转换对象
POST _render/template
{
  "source": "{ \"query\": {{#toJson}}my_query{{/toJson}} }",
  "params": {
    "my_query": {
      "match_all": { }
    }
  }
}

# 模板渲染结果
{
  "template_output": {
    "query": {
      "match_all": { }
    }
  }
}

# 转换对象数组
POST _render/template
{
  "source": "{ \"query\": { \"bool\": { \"must\": {{#toJson}}clauses{{/toJson}} }}}",
  "params": {
    "clauses": [
      {
        "term": {
          "user.id": "kimchy"
        }
      },
      {
        "term": {
          "url.domain": "example.com"
        }
      }
    ]
  }
}

# 模板渲染结果
{
  "template_output": {
    "query": {
      "bool": {
        "must": [
          {
            "term": {
              "user.id": "kimchy"
            }
          },
          {
            "term": {
              "url.domain": "example.com"
            }
          }
        ]
      }
    }
  }
}
```

##### 6.9.9.12 使用条件

`if` 语法：`{{#condition}}content{{/condition}}`

`if-else` 语法：`{{#condition}}if content{{/condition}} {{^condition}}else content{{/condition}}`

```json
POST _render/template
{
  "source": "{ \"query\": { \"bool\": { \"filter\": [ {{#year_scope}} { \"range\": { \"@timestamp\": { \"gte\": \"now-1y/d\", \"lt\": \"now/d\" } } }, {{/year_scope}} { \"term\": { \"user.id\": \"{{user_id}}\" }}]}}}",
  "params": {
    "year_scope": true,
    "user_id": "kimchy"
  }
}

# year_scope=true 模板渲染结果
{
  "template_output" : {
    "query" : {
      "bool" : {
        "filter" : [
          {
            "range" : {
              "@timestamp" : {
                "gte" : "now-1y/d",
                "lt" : "now/d"
              }
            }
          },
          {
            "term" : {
              "user.id" : "kimchy"
            }
          }
        ]
      }
    }
  }
}

# year_scope=false 模板渲染结果
{
  "template_output" : {
    "query" : {
      "bool" : {
        "filter" : [
          {
            "term" : {
              "user.id" : "kimchy"
            }
          }
        ]
      }
    }
  }
}
```

##### 6.9.9.13 `mustache`变量

Mustache 标签通常用双花括号括起来。Mustache 变量： `{{my-variable}}` 是一种 `Mustache` 标签。当您运行模板搜索时，Elasticsearch 会用 params 中的值替换这些变量。

```json
PUT _scripts/my-search-template
{
  "script": {
    "lang": "mustache",
    "source": {
      "query": {
        "match": {
          "message": "{{query_string}}"
        }
      },
      "from": "{{from}}",
      "size": "{{size}}"
    }
  }
}
```

##### 6.9.9.14 `section`

`section`也是一种 `Mustache` 标签。您可以在查询模板中使用 `section` ，配合嵌套或非嵌套对象。`section`以 `{{#my-section-variable}}` 开始，以 `{{/my-section-variable}}` 结束

```json
POST _render/template
{
  "source":
  """
  {
    "query": {
      "match": {
        {{#query_message}}
          {{#query_string}}
        "message": "Hello {{#first_name_section}}{{first_name}}{{/first_name_section}} {{#last_name_section}}{{last_name}}{{/last_name_section}}"
          {{/query_string}}
        {{/query_message}}
      }
    }
  }
  """,
  "params": {
    "query_message": {
       "query_string": {
         "first_name_section": {"first_name": "John"},
         "last_name_section": {"last_name": "kimchy"}
       }
    }
  }
}

# 模板渲染结果
{
  "template_output": {
    "query": {
      "match": {
        "message": "Hello John kimchy"
      }
    }
  }
}
```

`List`列表传入查询模板中

```json
PUT _scripts/my-search-template
{
  "script": {
    "lang": "mustache",
    "source": {
      "query":{
        "multi_match":{
          "query": "{{query_string}}",
          "fields": """[{{#text_fields}}{{user_name}},{{/text_fields}}]"""
        }
      }
    }
  }
}

# 使用列表
POST _render/template
{
  "id": "my-search-template",
  "params": {
    "query_string": "My string",
    "text_fields": [
      {
        "user_name": "John"
      },
      {
        "user_name": "kimchy"
      }
    ]
  }
}

# 模板渲染结果
{
  "template_output": {
    "query": {
      "multi_match": {
        "query": "My string",
        "fields": "[John,kimchy,]"
      }
    }
  }
}

注意：以上结果会有逗号遗留问题，是无效json。一个解决方法是在其中包含一个inverted section，并添加一个变量以确保它是数组中的最后一项。

```

##### 6.9.9.15 `inverted section` 倒置部分

语法：`{{^my-variable}} content {{/my-variable}}`

```json
PUT _scripts/my-search-template
{
  "script": {
    "lang": "mustache",
    "source": {
      "query":{
        "multi_match":{
          "query": "{{query_string}}",
          "fields": """[{{#text_fields}}{{user_name}}{{^last}},{{/last}}{{/text_fields}}]"""
        }
      }
    }
  }
}

# 使用inverted section
POST _render/template
{
  "id": "my-search-template",
  "params": {
    "query_string": "My string",
    "text_fields": [
      {
        "user_name": "John",
        "last": false
      },
      {
        "user_name": "kimchy",
        "last": true
      }
    ]
  }
}


# 模板渲染结果
{
  "template_output": {
    "query": {
      "multi_match": {
        "query": "My string",
        "fields": "[John,kimchy]"
      }
    }
  }
}

# 使用倒置部分,变量为false时，为空，变量为true时，Hello World
POST _render/template
{
  "source": {
    "query": {
      "match": {
        "message": "{{^name_exists}}Hello World{{/name_exists}}"
      }
    }
  },
  "params": {
     "name_exists": false
  }
}

```

##### 6.9.9.16 变量分隔符

mustache 的分隔符变更语法。

- `{{=( )=}}` 表示将模板变量的分隔符从默认的 `{{` 和 `}}` 改为 `(` 和 `)`。
- `(={{ }}=)` 表示将分隔符又改回默认的 `{{` 和 `}}`。

```json
# 将分隔符从默认的 {{ }} 改为 ( )
PUT _scripts/my-search-template
{
  "script": {
    "lang": "mustache",
    "source":
    """
    {
      "query": {
        "match": {
           {{=( )=}}
          "message": "(query_string)"
          (={{ }}=)
        }
      }
    }
    """
  }
}

# 使用变量分隔符
POST _render/template
{
  "id": "my-search-template",
  "params": {
    "query_string": "hello world"
  }
}

# 模板渲染结果
{
  "template_output": {
    "query": {
      "match": {
        "message": "hello world"
      }
    }
  }
}
```

### 6.10 查看分词器的分词结果

```json
GET /_analyze
{
  "analyzer": "ik_smart",
  "text": "中华人民共和国"
}
```

## 7. aggregations 聚合

### 7.1 Bucket aggregations 桶聚合

#### 7.1.1 terms aggregation

获取聚类时取的近似值，不是精确值

- `field` :聚类的字段，类型可以是`Keyword`, `Numeric`, `ip`, `boolean`, or `binary`。默认不能使用`text`类型字段聚类，可以使用`text`类型字段的`sub-field`代替。
- `size` :返回桶的数量，最大值是`serch.max_buckets`的值，默认10，有更多的不同`term`并且需要全部列出，请使用`composite aggregation`。
- `shard_size` :每个分片返回桶的数量，为了获得更准确的结果，`terms agg`会从每个分片中获取超过最大`size`的`terms`。它会获取`shard_size`个`terms`，该默认值为 `size * 1.5 + 10`。
- `show_term_doc_count_error`: 设置为`true`,结果返回`doc_count_error_upper_bound`，代表每个分片返回的`doc_count`误差的上限值。该值等于每个分片中未被`shard_size`所容纳的最大桶的大小之和
- `order` :排序方式，不建议设置其他参数，极其容易创建一种会导致错误结果的排序方式，一旦做了不容易察觉，切勿随意更改。尤其要避免使用`_count：asc`
  - `_count`:默认情况下，按照文档的`_count`值进行降序排列。不建议使用`_count`升序排序，会导致错误的结果。
  - `_key`: 按照`term`的值进行排列。
  - 子聚合：按照子聚合的结果进行排序。通过子聚合进行排序通常会导致不正确的排序结果，这是因为术语聚合是从分片中获取数据的这一方式所致。在以下两种情况下，子聚合排序是安全的，并且能够返回正确的结果：按照降序排列最大值，或者按照升序排列最小值。
- `min_doc_count` :最小文档数量
- `shard_min_doc_count` :用于控制一个分片对于某个词是否应真正被添加到候选列表中的确定性程度，该确定性取决于`min_doc_count`，默认值为0
- `missing` :用于定义那些未赋值的文档应如何处理。默认情况下，这些文档会被忽略，但也可以将其视为具有值进行处理。
- `include` :包含值
- `exclude` :排除值
- `aggs` :子聚合
- `collect_mode`：聚合模式，`depth_first` or `breadth_first`，默认`depth_first`。`depth_first`会优先计算子聚合，`breadth_first`会优先计算主聚合
- `execution_hint`:聚合实现模式，`global_ordinals` or `map`，默认`global_ordinals`。`global_ordinals`使用全局序号，`map`使用映射。`global_ordinals`在数据量较大时性能更好，默认情况下，只有在对脚本进行聚合操作时才会使用 `map`模式

```json
GET /_search
{
  "aggs": {
    "colors_agg": {
      "terms": {
         "field": "color",
         "show_term_doc_count_error": true
         }
    }
  }
}

响应结果：
{
  ...
  "aggregations": {
    "colors_agg": {
      "doc_count_error_upper_bound": 0,   
      "sum_other_doc_count": 0,           
      "buckets": [                        
        {
          "key": "red",
          "doc_count": 6
        },
        {
          "key": "green",
          "doc_count": 3
        },
        {
          "key": "blue",
          "doc_count": 2
        }
      ]
    }
  }
}
 
```

`doc_count_error_upper_bound`: 一个桶在一个分片中容量很大，而在其他所有分片中则略小于 `shard_size`。在这种情况下，聚合函数会返回这个桶，因为它容量很大，但会遗漏许多落在`shard_size`阈值以下的分片中的文档的数据。`doc_count_error_upper_bound` 是这些遗漏文档的最大数量。
`sum_other_doc_count`：未被返回的桶的数量，其值大于0表示有舍弃的桶或因为`size`参数限制桶的数量或者`shard_size`参数限制

只有在按照文档数量降序排列`terms`的情况下，才能通过这种方式计算出这些错误。当聚合是按照`terms`自身的值（无论是升序还是降序）进行排序时，文档数量就不会出现错误

`聚合排序`

```json
1.按照文档数量排序
GET /_search
{
  "aggs": {
    "mobile_agg": {
      "terms": {
        "field": "color",
        "order": { "_count": "desc" }
      }
    }
  }
}

2.按聚类的值排序
{
  "aggs": {
    "mobile_agg": {
      "terms": {
        "field": "color",
        "order": { "_key": "asc" }
      }
    }
  }
}

3.子聚合排序
GET /_search
{
  "aggs": {
    "mobile_agg": {
      "terms": {
        "field": "color",
        "order": { "max_model_count": "desc" }
      },
      "aggs": {
        "max_model_count": { "max": { "field": "model_count" } }
      }
    }
  }
}

pipeline aggregation管道聚合无法用于排序操作，在所有其他聚合操作完成后，管道聚合会在归约阶段进行。因此，它们不能用于排序操作。
```

`Filter Values`

使用`include`和`exclude`过滤聚类项的值

```json
1.正则表达式过滤
GET /_search
{
  "aggs": {
    "tags": {
      "terms": {
        "field": "tags",
        "include": ".*sport.*",
        "exclude": "water_.*"
      }
    }
  }
}

2.过滤确定的值
GET /_search
{
  "aggs": {
    "JapaneseCars": {
      "terms": {
        "field": "make",
        "include": [ "mazda", "honda" ]
      }
    },
    "ActiveCarManufacturers": {
      "terms": {
        "field": "make",
        "exclude": [ "rover", "jensen" ]
      }
    }
  }
}

3.通过分区过滤
分区不能与exclude参数一同使用
GET /_search
{
   "size": 0,
   "aggs": {
      "expired_sessions": {
         "terms": {
            "field": "account_id",
            "include": {
               "partition": 0,
               "num_partitions": 20
            },
            "size": 10000,
            "order": {
               "last_access": "asc"
            }
         },
         "aggs": {
            "last_access": {
               "max": {
                  "field": "access_date"
               }
            }
         }
      }
   }
}
```

`collect_mode`

广度优先和深度优先两种模式

查询电影数据库以获取最受欢迎的 10 位演员及其最常见的 5 位合作演员。这种场景适用于广度优先模式，因为我们需要先找到最受欢迎的 10 位演员，然后再找到他们的合作演员。

```json

GET /_search
{
  "aggs": {
    "actors": {
      "terms": {
        "field": "actors",
        "size": 10,
        "collect_mode": "breadth_first" 
      },
      "aggs": {
        "costars": {
          "terms": {
            "field": "actors",
            "size": 5
          }
        }
      }
    }
  }
}
```

`missing`

```json
GET /_search
{
  "aggs": {
    "tags": {
      "terms": {
        "field": "tags",
        "missing": "N/A" 
      }
    }
  }
}

如果某个索引中该字段未被映射，value_type参数能够将未映射的字段强制转换为正确的类型
GET /_search
{
  "aggs": {
    "ip_addresses": {
      "terms": {
        "field": "destination_ip",
        "missing": "0.0.0.0",
        "value_type": "ip"
      }
    }
  }
}
```

#### 7.1.2 range aggregation

一种基于多桶值源的聚合方式，使用户能够定义一组范围——每个范围都代表一个桶。聚合方式包含`from`的值但不包含`to`的值。

- `field` :用于聚合的字段
- `keyed` :是否返回键值对格式的结果，key值可以自定义指定，默认`false`
- `size` :返回的桶的数量，默认`10`
- `shard_size` :每个分片返回的桶的数量，默认`size`的值
- `min_doc_count` :每个桶的最小文档数量，默认`0`

```json
GET sales/_search
{
  "aggs": {
    "price_ranges": {
      "range": {
        "field": "price",
        "ranges": [
          { "to": 100.0 },
          { "from": 100.0, "to": 200.0 },
          { "from": 200.0 }
        ]
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "price_ranges": {
      "buckets": [
        {
          "key": "*-100.0",
          "to": 100.0,
          "doc_count": 2
        },
        {
          "key": "100.0-200.0",
          "from": 100.0,
          "to": 200.0,
          "doc_count": 2
        },
        {
          "key": "200.0-*",
          "from": 200.0,
          "doc_count": 3
        }
      ]
    }
  }
}
```

`keyed`

```json
指定自定义key值，每个范围不是数组，是hash值形式返回
GET sales/_search
{
  "aggs": {
    "price_ranges": {
      "range": {
        "field": "price",
        "keyed": true,
        "ranges": [
          { "key": "cheap", "to": 100 },
          { "key": "average", "from": 100, "to": 200 },
          { "key": "expensive", "from": 200 }
        ]
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "price_ranges": {
      "buckets": {
        "cheap": {
          "to": 100.0,
          "doc_count": 2
        },
        "average": {
          "from": 100.0,
          "to": 200.0,
          "doc_count": 2
        },
        "expensive": {
          "from": 200.0,
          "doc_count": 3
        }
      }
    }
  }
}
```

`script`使用运行时字段

```json
计算欧元货币的价格范围
GET sales/_search
{
  "runtime_mappings": {
    "price.euros": {
      "type": "double",
      "script": {
        "source": """
          emit(doc['price'].value * params.conversion_rate)
        """,
        "params": {
          "conversion_rate": 0.835526591
        }
      }
    }
  },
  "aggs": {
    "price_ranges": {
      "range": {
        "field": "price.euros",
        "ranges": [
          { "to": 100 },
          { "from": 100, "to": 200 },
          { "from": 200 }
        ]
      }
    }
  }
}
```

`sub aggregations`

```json
GET sales/_search
{
  "aggs": {
    "price_ranges": {
      "range": {
        "field": "price",
        "ranges": [
          { "to": 100 },
          { "from": 100, "to": 200 },
          { "from": 200 }
        ]
      },
      "aggs": {
        "price_stats": {
          "stats": { "field": "price" }
        }
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "price_ranges": {
      "buckets": [
        {
          "key": "*-100.0",
          "to": 100.0,
          "doc_count": 2,
          "price_stats": {
            "count": 2,
            "min": 10.0,
            "max": 50.0,
            "avg": 30.0,
            "sum": 60.0
          }
        },
        {
          "key": "100.0-200.0",
          "from": 100.0,
          "to": 200.0,
          "doc_count": 2,
          "price_stats": {
            "count": 2,
            "min": 150.0,
            "max": 175.0,
            "avg": 162.5,
            "sum": 325.0
          }
        },
        {
          "key": "200.0-*",
          "from": 200.0,
          "doc_count": 3,
          "price_stats": {
            "count": 3,
            "min": 200.0,
            "max": 200.0,
            "avg": 200.0,
            "sum": 600.0
          }
        }
      ]
    }
  }
}
```

#### 7.1.3 date_range aggregation

一种专门用于日期值的范围聚合。这种聚合与常规范围聚合的主要区别在于，起始值和结束值可以以日期数学表达式的形式表示，并且还可以指定一种日期格式，以便返回起始和结束响应字段。这种聚合会包含起始值，但会排除结束值，针对每个范围都是如此。

- `missing`: 默认情况下，这些缺失的值将被忽略，但也可以选择将其视为具有某个值来处理。
- `keyed`：指定自定义key值，每个范围不是数组，是hash值形式返回。

```json
POST /sales/_search?size=0
{
  "aggs": {
    "range": {
      "date_range": {
        "field": "date",
        "format": "yyyy-MM",
        "ranges": [
          { "to": "now-10M/M" },  
          { "from": "now-10M/M" } 
        ]
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "range": {
      "buckets": [
        {
          "to": 1.4436576E12,
          "to_as_string": "2015-10",
          "doc_count": 7,
          "key": "*-2015-10"
        },
        {
          "from": 1.4436576E12,
          "from_as_string": "2015-10",
          "doc_count": 0,
          "key": "2015-10-*"
        }
      ]
    }
  }
}
```

`Missing`

```json
POST /sales/_search?size=0
{
   "aggs": {
       "range": {
           "date_range": {
               "field": "date",
               "missing": "1976/11/30",
               "ranges": [
                  {
                    "key": "Older",
                    "to": "2016/02/01"
                  }, 
                  {
                    "key": "Newer",
                    "from": "2016/02/01",
                    "to" : "now/d"
                  }
              ]
          }
      }
   }
}
```

`keyed response`

指定自定义key值，每个范围不是数组，是hash值形式返回

```json
POST /sales/_search?size=0
{
  "aggs": {
    "range": {
      "date_range": {
        "field": "date",
        "format": "MM-yyy",
        "ranges": [
          { "from": "01-2015", "to": "03-2015", "key": "quarter_01" },
          { "from": "03-2015", "to": "06-2015", "key": "quarter_02" }
        ],
        "keyed": true
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "range": {
      "buckets": {
        "quarter_01": {
          "from": 1.4200704E12,
          "from_as_string": "01-2015",
          "to": 1.425168E12,
          "to_as_string": "03-2015",
          "doc_count": 5
        },
        "quarter_02": {
          "from": 1.425168E12,
          "from_as_string": "03-2015",
          "to": 1.4331168E12,
          "to_as_string": "06-2015",
          "doc_count": 2
        }
      }
    }
  }
}
```

#### 7.1.4 ip_range aggregation

专门聚合`IP`类型的字段

- `keyed`：指定自定义key值，每个范围不是数组，是hash值形式返回。

```json
GET /ip_addresses/_search
{
  "size": 10,
  "aggs": {
    "ip_ranges": {
      "ip_range": {
        "field": "ip",
        "ranges": [
          { "to": "10.0.0.5" },
          { "from": "10.0.0.5" }
        ]
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "ip_ranges": {
      "buckets": [
        {
          "key": "*-10.0.0.5",
          "to": "10.0.0.5",
          "doc_count": 10
        },
        {
          "key": "10.0.0.5-*",
          "from": "10.0.0.5",
          "doc_count": 260
        }
      ]
    }
  }
}
```

`CIDR masks`：CIDR掩码

```json
GET /ip_addresses/_search
{
  "size": 0,
  "aggs": {
    "ip_ranges": {
      "ip_range": {
        "field": "ip",
        "ranges": [
          { "mask": "10.0.0.0/25" },
          { "mask": "10.0.0.127/25" }
        ]
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "ip_ranges": {
      "buckets": [
        {
          "key": "10.0.0.0/25",
          "from": "10.0.0.0",
          "to": "10.0.0.128",
          "doc_count": 128
        },
        {
          "key": "10.0.0.127/25",
          "from": "10.0.0.0",
          "to": "10.0.0.128",
          "doc_count": 128
        }
      ]
    }
  }
}
```

`keyed` 指定自定义key值，每个范围不是数组，是hash值形式返回

```json
GET /ip_addresses/_search
{
  "size": 0,
  "aggs": {
    "ip_ranges": {
      "ip_range": {
        "field": "ip",
        "ranges": [
          { "key": "infinity", "to": "10.0.0.5" },
          { "key": "and-beyond", "from": "10.0.0.5" }
        ],
        "keyed": true
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "ip_ranges": {
      "buckets": {
        "infinity": {
          "to": "10.0.0.5",
          "doc_count": 10
        },
        "and-beyond": {
          "from": "10.0.0.5",
          "doc_count": 260
        }
      }
    }
  }
}
```

#### 7.1.5 histogram aggregation

一种基于多桶值源的聚合方式，可用于处理从文档中提取的数值或数值范围值。它会动态地在这些值上构建固定大小（即区间）的桶。

- `field`：要聚合的字段。
- `interval`：每个桶的间隔大小。例如，如果字段是日期类型，则可以使用`day`、`week`、`month`、`quarter`或`year`等时间单位。
- `min_doc_count`：每个桶中至少应包含的文档数量。如果某个桶中的文档数量少于该值，则该桶将被忽略。
- `extended_bounds`：指定桶的边界范围，包括最小值和最大值。这对于处理缺失值或超出指定范围的值非常有用。
- `hard_bounds`：指定桶的硬边界，即强制将所有值限制在指定的范围内。如果某个值超出了指定的范围，则该值将被忽略。
- `order`：指定桶的排序方式。可以按文档数量（`_count`）或桶的值（`_key`）排序。默认按`_key`升序排序。
- `offset`：每个桶的偏移量。默认情况下，桶键从 0 开始，然后以固定的间隔进行连续排列。例如，如果字段是日期类型，则可以使用`1d`、`1w`、`1M`、`1q`或`1y`等时间单位。
- `keyed`：指定自定义key值，每个范围不是数组，是hash值形式返回。
- `missing`: 默认情况下，这些缺失的值将被忽略，但也可以选择将其视为具有某个值来处理。

```json
POST /sales/_search?size=0
{
  "aggs": {
    "prices": {
      "histogram": {
        "field": "price",
        "interval": 50
      }
    }
  }
}
响应结果
{
  ...
  "aggregations": {
    "prices": {
      "buckets": [
        {
          "key": 0.0,
          "doc_count": 2
        },
        {
          "key": 50.0,
          "doc_count": 3
        },
        {
          "key": 100.0,
          "doc_count": 5
        }       
      ]
    }
  }
}
```

`extended_bounds`：指定桶的边界范围，包括最小值和最大值。这对于处理缺失值或超出指定范围的值非常有用。



```json
处理min_doc_count设置为0，但是有些桶没有文档的情况，并且所有桶的文档数量都大于50，希望显示0-50范围的桶
POST /sales/_search?size=0
{
  "query": {
    "constant_score": { "filter": { "range": { "price": { "to": "500" } } } }
  },
  "aggs": {
    "prices": {
      "histogram": {
        "field": "price",
        "interval": 50,
        "extended_bounds": {
          "min": 0,
          "max": 500
        }
      }
    }
  }
}
```

`hard_bounds`: 指定桶的硬边界，即强制将所有值限制在指定的范围内。如果某个值超出了指定的范围，则该值将被忽略。在处理开放的数据范围（这可能会导致大量的桶）时，它特别有用

```json
POST /sales/_search?size=0
{
  "query": {
    "constant_score": { "filter": { "range": { "price": { "to": "500" } } } }
  },
  "aggs": {
    "prices": {
      "histogram": {
        "field": "price",
        "interval": 50,
        "hard_bounds": {
          "min": 100,
          "max": 200
        }
      }
    }
  }
}
```

`keyed`:指定自定义key值，每个范围不是数组，是hash值形式返回

```json
POST /sales/_search?size=0
{
  "aggs": {
    "prices": {
      "histogram": {
        "field": "price",
        "interval": 50,
        "keyed": true
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "prices": {
      "buckets": {
        "0.0": {
          "key": 0.0,
          "doc_count": 1
        },
        "50.0": {
          "key": 50.0,
          "doc_count": 1
        },
        "100.0": {
          "key": 100.0,
          "doc_count": 0
        }        
      }
    }
  }
}
```

`missing`: 默认情况下，这些缺失的值将被忽略，但也可以选择将其视为具有某个值来处理。

```json
POST /sales/_search?size=0
{
  "aggs": {
    "quantity": {
      "histogram": {
        "field": "quantity",
        "interval": 10,
        "missing": 0 
      }
    }
  }
}
```

#### 7.1.6 date_histogram aggregation

日期直方图聚合，只能与日期类型和日期范围一起使用，两种方式来指定间隔：基于日历的时间间隔以及固定时间间隔。

- `field`：要聚合的字段。
- `calendar_interval`：基于日历的时间间隔，例如`minute`、`hour`、`day`、`week`、`month`、`quarter`或`year`。
- `fixed_interval`：固定时间间隔，例如`1000ms`、`5s`、`3m`、`1h`、 `1d`。
- `format`: 指定`key_as_string`日期格式。默认使用字段映射中首先指定的日期格式。
- `time_zone`: 指定时区，默认使用UTC时区。Elasticsearch 将日期时间存储为协调世界时（UTC）。使用ISO 8601 UTC 偏移量（例如 `+01：00` 或 `-08：00`）或时区名称（`America/Los_Angeles`）来指定时区。
- `offset`: 指定桶的偏移量。默认情况下，桶键从 0 开始，然后以固定的间隔进行连续排列。例如，如果字段是日期类型，则可以使用`1d`、`1w`、`1M`、`1q`或`1y`等时间单位。
- `keyed`: 指定自定义key值，每个范围不是数组，是hash值形式返回。
- `order`: 指定桶的排序方式。可以按文档数量（`_count`）或桶的值（`_key`）排序。默认按`_key`升序排序。
- `missing`: 默认情况下，这些缺失的值将被忽略，但也可以选择将其视为具有某个值来处理。
- `min_doc_count`：每个桶中至少应包含的文档数量。如果某个桶中的文档数量少于该值，则该桶将被忽略。
- `extended_bounds`：指定桶的边界范围，包括最小值和最大值。这对于处理缺失值或超出指定范围的值非常有用。
- `hard_bounds`：指定桶的硬边界，即强制将所有值限制在指定的范围内。如果某个值超出了指定的范围，则该值将被忽略。
- `scripts`: 指定脚本，用于计算日期直方图聚合的值。

```json
calendar_interval
POST /sales/_search?size=0
{
  "aggs": {
    "sales_over_time": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      }
    }
  }
}

fixed_interval
POST /sales/_search?size=0
{
  "aggs": {
    "sales_over_time": {
      "date_histogram": {
        "field": "date",
        "fixed_interval": "30d"
      }
    }
  }
}

format 设置key_as_string格式，日期被表示为一个 64 位的数字，该数字表示自“纪元起”的毫秒数，未指定格式，则会使用字段映射中首先指定的日期格式
POST /sales/_search?size=0
{
  "aggs": {
    "sales_over_time": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "1M",
        "format": "yyyy-MM-dd" 
      }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "sales_over_time": {
      "buckets": [
        {
          "key_as_string": "2015-01-01",
          "key": 1420070400000,
          "doc_count": 3
        },
        {
          "key_as_string": "2015-02-01",
          "key": 1422748800000,
          "doc_count": 2
        },
        {
          "key_as_string": "2015-03-01",
          "key": 1425168000000,
          "doc_count": 2
        }
      ]
    }
  }
}
```

`time_zone`

```json
GET my-index-000001/_search?size=0
{
  "aggs": {
    "by_day": {
      "date_histogram": {
        "field":     "date",
        "calendar_interval":  "day",
        "time_zone": "+08:00"
      }
    }
  }
}

GET my-index-000001/_search?size=0
{
  "aggs": {
    "by_day": {
      "date_histogram": {
        "field":     "date",
        "calendar_interval":  "day",
        "time_zone": "America/Los_Angeles"
      }
    }
  }
}
```

`offset`：通常偏移量会小于于间隔，例如，如果间隔是1天，则偏移量可以是6小时，这样就可以在一天的开始和结束之间创建一个桶。

```json
GET my-index-000001/_search?size=0
{
  "aggs": {
    "by_day": {
      "date_histogram": {
        "field":     "date",
        "calendar_interval":  "day",
        "offset":    "+6h"
      }
    }
  }
}
```

`keyed`: 指定自定义key值，每个范围不是数组，是hash值形式返回

```json
POST /sales/_search?size=0
{
  "aggs": {
    "sales_over_time": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "1M",
        "format": "yyyy-MM-dd",
        "keyed": true
      }
    }
  }
}
```

`missing`: 默认情况下，这些缺失的值将被忽略，但也可以选择将其视为具有某个值来处理。

```json
POST /sales/_search?size=0
{
  "aggs": {
    "sale_date": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "year",
        "missing": "2000/01/01" 
      }
    }
  }
}
```

`scripts` 使用运行时字段可以在聚合查询中动态计算字段值。例如，可以使用脚本将日期字段转换为不同的时区。

```json
POST /sales/_search?size=0
{
  "runtime_mappings": {
    "date.promoted_is_tomorrow": {
      "type": "date",
      "script": """
        long date = doc['date'].value.toInstant().toEpochMilli();
        if (doc['promoted'].value) {
          date += 86400;
        }
        emit(date);
      """
    }
  },
  "aggs": {
    "sales_over_time": {
      "date_histogram": {
        "field": "date.promoted_is_tomorrow",
        "calendar_interval": "1M"
      }
    }
  }
}
```

#### 7.1.7 filter aggregation

一种单一的桶式聚合操作，它会将文档集缩小至与查询条件相匹配的那些文档。
若要限制搜索中所有聚合操作所涉及的文档范围，请使用顶级查询。这种方式比带有子聚合的单个筛选聚合要快。
若要使用多个筛选条件对文档进行分组，请使用`filters aggregation`。这种方式比使用多个`filter aggregation`操作要快。

```json
POST /sales/_search?size=0&filter_path=aggregations
{
  "aggs": {
    "avg_price": { "avg": { "field": "price" } },
    "t_shirts": {
      "filter": { "term": { "type": "t-shirt" } },
      "aggs": {
        "avg_price": { "avg": { "field": "price" } }
      }
    }
  }
}
响应结果
{
  "aggregations": {
    "avg_price": { "value": 140.71428571428572 },
    "t_shirts": {
      "doc_count": 3,
      "avg_price": { "value": 128.33333333333334 }
    }
  }
}
```

#### 7.1.8 filters aggregation

- `filters`：指定一组过滤器，每个过滤器对应一个桶。每个过滤器都是一个查询对象，用于匹配文档集。
- `other_bucket`:指定是否为不匹配任何过滤器的文档创建一个额外的桶。默认为`false`。
- `other_bucket_key`：指定为不匹配任何过滤器的文档创建一个额外的桶的名称。不指定`other_bucket_key`的值，默认为`_other_`。设置`other_bucket_key`的值，则`other_bucket`隐式设置为`true`。
- `keyed`:是否将桶以对象数组的形式返回。默认为`false`。对于匿名过滤器聚合无效。

```json
PUT /logs/_bulk?refresh
{ "index" : { "_id" : 1 } }
{ "body" : "warning: page could not be rendered" }
{ "index" : { "_id" : 2 } }
{ "body" : "authentication error" }
{ "index" : { "_id" : 3 } }
{ "body" : "warning: connection timed out" }

GET logs/_search
{
  "size": 0,
  "aggs" : {
    "message_aggs" : {
      "filters" : {
        "filters" : {
          "error_aggs" :   { "match" : { "body" : "error"   }},
          "warning_aggs" : { "match" : { "body" : "warning" }}
        }
      }
    }
  }
}
```

`anonymous filters`

```json
filters 可以使用匿名过滤器，即无需指定过滤器名称。
GET logs/_search
{
  "size": 0,
  "aggs" : {
    "message_aggs" : {
      "filters" : {
        "filters" : [
          { "match" : { "body" : "error"   }},
          { "match" : { "body" : "warning" }}
        ]
      }
    }
  }
}

响应结果
{  
  "aggregations": {
    "message_aggs": {
      "buckets": [
        {
          "doc_count": 1
        },
        {
          "doc_count": 2
        }
      ]
    }
  }
}
```

`other_bucket`

```json
other_bucket设置
GET logs/_search
{
  "size": 0,
  "aggs" : {
    "message_aggs" : {
      "filters" : {
        "other_bucket": true,
        "filters" : {
          "error_aggs" :   { "match" : { "body" : "error"   }},
          "warning_aggs" : { "match" : { "body" : "warning" }}
        }
      }
    }
  }
}

响应结果
{  
  "aggregations": {
    "message_aggs": {
      "buckets": {
        "error_aggs": {
          "doc_count": 1
        },
        "warning_aggs": {
          "doc_count": 2
        },
        "_other_": {
          "doc_count": 1
        }
      }
    }
  }
}

other_bucket_key显示设置

GET logs/_search
{
  "size": 0,
  "aggs" : {
    "message_aggs" : {
      "filters" : {
        "other_bucket_key": "other_message_aggs",
        "filters" : {
          "error_aggs" :   { "match" : { "body" : "error"   }},
          "warning_aggs" : { "match" : { "body" : "warning" }}
        }
      }
    }
  }
}

响应结果
{  
  "aggregations": {
    "message_aggs": {
      "buckets": {
        "error_aggs": {
          "doc_count": 1
        },
        "warning_aggs": {
          "doc_count": 2
        },
        "other_message_aggs": {
          "doc_count": 1
        }
      }
    }
  }
}
```

`keyed`

```json
POST /sales/_search?size=0&filter_path=aggregations
{
  "aggs": {
    "the_filter": {
      "filters": {
        "keyed": false,
        "filters": {
          "t-shirt": { "term": { "type": "t-shirt" } },
          "hat": { "term": { "type": "hat" } }
        }
      },
      "aggs": {
        "avg_price": { "avg": { "field": "price" } },
        "sort_by_avg_price": {
          "bucket_sort": { "sort": { "avg_price": "asc" } }
        }
      }
    }
  }
}

响应结果
{
  "aggregations": {
    "the_filter": {
      "buckets": [
        {
          "key": "t-shirt",
          "doc_count": 3,
          "avg_price": { "value": 128.33333333333334 }
        },
        {
          "key": "hat",
          "doc_count": 3,
          "avg_price": { "value": 150.0 }
        }
      ]
    }
  }
}
```

#### 7.1.9 global aggregation

`global aggregation`只能被置于顶级聚合器的位置

```json
POST /sales/_search?size=0
{
  "query": {
    "match": { "type": "t-shirt" }
  },
  "aggs": {
    "all_products": {
      "global": {}, 
      "aggs": {     
      "avg_price": { "avg": { "field": "price" } }
      }
    },
    "t_shirts": { "avg": { "field": "price" } }
  }
}

响应结果
平均价格是所有产品的平均价格，而不是只计算 t-shirt 的平均价格。不受查询条件的影响。
{  
  "aggregations": {
    "all_products": {
      "doc_count": 7, 
      "avg_price": {
        "value": 140.71428571428572 
      }
    },
    "t_shirts": {
      "value": 128.33333333333334 
    }
  }
}
```

#### 7.1.10 composite aggregation

一种多桶聚合操作，能够将来自不同来源的数据整合为复合桶。复合聚合高效地分页获取多层级聚合中的所有桶。能够像滚动功能对文档进行操作那样，对特定聚合的所有桶进行流式传输。

- `sources`：指定用于创建复合桶的源字段。可以使用`terms`、`histogram`、`Date Histogram`、`GeoTile gird`类型的聚合
- `size`：指定返回的桶的最大数量，默认为10

```json
sources 为 terms类型
GET /_search
{
  "size": 0,
  "aggs": {
    "my_buckets": {
      "composite": {
        "sources": [
          { "product": { "terms": { "field": "product" } } }
        ]
      }
    }
  }
}

souces 为 histogram类型
GET /_search
{
  "size": 0,
  "aggs": {
    "my_buckets": {
      "composite": {
        "sources": [
          { "histo": { "histogram": { "field": "price", "interval": 5 } } }
        ]
      }
    }
  }
}

souces 为 date_histogram类型
GET /_search
{
  "size": 0,
  "aggs": {
    "my_buckets": {
      "composite": {
        "sources": [
          { "date": { "date_histogram": { "field": "timestamp", "calendar_interval": "1d" } } }
        ]
      }
    }
  }
}

sources 为混合类型
GET /_search
{
  "size": 0,
  "aggs": {
    "my_buckets": {
      "composite": {
        "sources": [
          { "date": { "date_histogram": { "field": "timestamp", "calendar_interval": "1d" } } },
          { "product": { "terms": { "field": "product" } } }
        ]
      }
    }
  }
}
```

`order`：默认情况下，复合桶会按照其自然顺序进行排序。数值按其数值的升序排列。当需要处理多个值源时，系统将按值源顺序进行排序：首先比较复合桶中的首个值与其他复合桶的首个值，若两者相等，则采用该复合桶中的后续值进行排序。

```json
GET /_search
{
  "size": 0,
  "aggs": {
    "my_buckets": {
      "composite": {
        "sources": [
          { "date": { "date_histogram": { "field": "timestamp", "calendar_interval": "1d", "order": "desc" } } },
          { "product": { "terms": { "field": "product", "order": "asc" } } }
        ]
      }
    }
  }
}
```

`missing_bucket`：指定是否应包含缺失值的桶，默认为`false`，可选`true`
`missing_order`：指定缺失值的桶的顺序，默认为`last`，可选`first`、`last`

```json
GET /_search
{
  "size": 0,
  "aggs": {
    "my_buckets": {
      "composite": {
        "sources": [{
          "product_name": {
            "terms": {
              "field": "product",
              "missing_bucket": true,
              "missing_order": "last"
            }
          }
        }]
      }
    }
  }
}
```

`size`：指定返回的桶的最大数量，默认为10
`after`：通过`after`分页参数获取后续数据，应始终使用响应返回的`after_key`进行分页，否则会丢失数据

```json
GET /_search
{
  "size": 0,
  "aggs": {
    "my_buckets": {
      "composite": {
        "size": 2,
        "sources": [
          { "date": { "date_histogram": { "field": "timestamp", "calendar_interval": "1d" } } },
          { "product": { "terms": { "field": "product" } } }
        ]
      }
    }
  }
}

响应结果
{  
  "aggregations": {
    "my_buckets": {
      "after_key": {
        "date": 1494288000000,
        "product": "mad max"
      },
      "buckets": [
        {
          "key": {
            "date": 1494201600000,
            "product": "rocky"
          },
          "doc_count": 1
        },
        {
          "key": {
            "date": 1494288000000,
            "product": "mad max"
          },
          "doc_count": 2
        }
      ]
    }
  }
}

after 通过after_key获取下一页数据
GET /_search
{
  "size": 0,
  "aggs": {
    "my_buckets": {
      "composite": {
        "size": 2,
        "sources": [
          { "date": { "date_histogram": { "field": "timestamp", "calendar_interval": "1d", "order": "desc" } } },
          { "product": { "terms": { "field": "product", "order": "asc" } } }
        ],
        "after": { "date": 1494288000000, "product": "mad max" } 
      }
    }
  }
}
```

`sub aggregasion`

```json
GET /_search
{
  "size": 0,
  "aggs": {
    "my_buckets": {
      "composite": {
        "sources": [
          { "date": { "date_histogram": { "field": "timestamp", "calendar_interval": "1d", "order": "desc" } } },
          { "product": { "terms": { "field": "product" } } }
        ]
      },
      "aggregations": {
        "the_avg": {
          "avg": { "field": "price" }
        }
      }
    }
  }
}

响应结果
{  
  "aggregations": {
    "my_buckets": {
      "after_key": {
        "date": 1494374400000,
        "product": "mad max"
      },
      "buckets": [
        {
          "key": {
            "date": 1494460800000,
            "product": "apocalypse now"
          },
          "doc_count": 1,
          "the_avg": {
            "value": 10.0
          }
        },
        {
          "key": {
            "date": 1494374400000,
            "product": "mad max"
          },
          "doc_count": 1,
          "the_avg": {
            "value": 27.0
          }
        }        
      ]
    }
  }
}
```

#### 7.1.11 multi terms aggregation

当需要根据复合键对多个文档或指标聚合值进行排序并获取前N个结果时，多术语聚合功能最为实用。默认情况下，多术语聚合会返回按 doc_count 排序的前十个术语对应的桶。

- `size` :返回桶的数量，最大值是`serch.max_buckets`的值，默认10，有更多的不同`term`并且需要全部列出，请使用`composite aggregation`。
- `shard_size` :每个分片返回桶的数量，为了获得更准确的结果，`terms agg`会从每个分片中获取超过最大`size`的`terms`。它会获取`shard_size`个`terms`，该默认值为 `size * 1.5 + 10`。
- `show_term_doc_count_error`: 设置为`true`,结果返回`doc_count_error_upper_bound`，代表每个分片返回的`doc_count`误差的上限值。该值等于每个分片中未被`shard_size`所容纳的最大桶的大小之和
- `order` :默认设置为每个存储桶的文档数量上限。当多个数据桶的文档数量相同时，将采用桶项值作为决胜依据。  
- `min_doc_count`:每个桶的最小文档数量，默认为`1`
- `shard_min_doc_count` :每个分片中桶的最小文档数量，默认值为`min_doc_count`
- `missing` :用于定义那些未赋值的文档应如何处理。默认情况下，这些文档会被忽略，但也可以将其视为具有值进行处理。
- `collect_mode`：聚合模式，`depth_first` or `breadth_first`，默认`depth_first`。`depth_first`会优先计算子聚合，`breadth_first`会优先计算主聚合

```json
GET /products/_search
{
  "aggs": {
    "genres_and_products": {
      "multi_terms": {
        "terms": [{
          "field": "genre" 
        }, {
          "field": "product"
        }]
      }
    }
  }
}

响应结果
{
  "aggregations" : {
    "genres_and_products" : {
      "doc_count_error_upper_bound" : 0,  
      "sum_other_doc_count" : 0,          
      "buckets" : [                       
        {
          "key" : [                       
            "rock",
            "Product A"
          ],
          "key_as_string" : "rock|Product A",
          "doc_count" : 2
        },
        {
          "key" : [
            "electronic",
            "Product B"
          ],
          "key_as_string" : "electronic|Product B",
          "doc_count" : 1
        }        
      ]
    }
  }
}
```

`scripts`

```json
GET /products/_search
{
  "runtime_mappings": {
    "genre.length": {
      "type": "long",
      "script": "emit(doc['genre'].value.length())"
    }
  },
  "aggs": {
    "genres_and_products": {
      "multi_terms": {
        "terms": [
          {
            "field": "genre.length"
          },
          {
            "field": "product"
          }
        ]
      }
    }
  }
}

响应结果
{  
  "aggregations" : {
    "genres_and_products" : {
      "doc_count_error_upper_bound" : 0,
      "sum_other_doc_count" : 0,
      "buckets" : [
        {
          "key" : [
            4,
            "Product A"
          ],
          "key_as_string" : "4|Product A",
          "doc_count" : 2
        },
        {
          "key" : [
            4,
            "Product B"
          ],
          "key_as_string" : "4|Product B",
          "doc_count" : 2
        }        
      ]
    }
  }
}
```

`missing`

```json
GET /products/_search
{
  "aggs": {
    "genres_and_products": {
      "multi_terms": {
        "terms": [
          {
            "field": "genre"
          },
          {
            "field": "product",
            "missing": "Product Z"
          }
        ]
      }
    }
  }
}
```

`sub aggregation`

```json
GET /products/_search
{
  "aggs": {
    "genres_and_products": {
      "multi_terms": {
        "terms": [
          {
            "field": "genre"
          },
          {
            "field": "product"
          }
        ],
        "order": {
          "total_quantity": "desc"
        }
      },
      "aggs": {
        "total_quantity": {
          "sum": {
            "field": "quantity"
          }
        }
      }
    }
  }
}

响应结果
{  
  "aggregations" : {
    "genres_and_products" : {
      "doc_count_error_upper_bound" : 0,
      "sum_other_doc_count" : 0,
      "buckets" : [
        {
          "key" : [
            "jazz",
            "Product B"
          ],
          "key_as_string" : "jazz|Product B",
          "doc_count" : 1,
          "total_quantity" : {
            "value" : 10.0
          }
        },
        {
          "key" : [
            "rock",
            "Product A"
          ],
          "key_as_string" : "rock|Product A",
          "doc_count" : 2,
          "total_quantity" : {
            "value" : 9.0
          }
        },
        {
          "key" : [
            "electronic",
            "Product B"
          ],
          "key_as_string" : "electronic|Product B",
          "doc_count" : 1,
          "total_quantity" : {
            "value" : 3.0
          }
        }       
      ]
    }
  }
}
```

#### 7.1.12 missing agregation

基于字段数据的单桶聚合方法，可将当前文档集上下文中所有缺失字段值（即缺少字段或配置了NULL值）的文档归入同一桶中。该聚合器通常需与其他字段数据分桶聚合器（如范围聚合器）配合使用，用于返回所有因字段数据缺失而无法归入其他分桶的文档信息。

```json
POST /sales/_search?size=0
{
  "aggs": {
    "products_without_a_price": {
      "missing": { "field": "price" }
    }
  }
}
```

#### 7.1.13 nested agregation

我们有一个产品索引，每个产品都包含其经销商列表——每个经销商对该产品的定价各不相同

```json
PUT /products
{
  "mappings": {
    "properties": {
      "resellers": { 
        "type": "nested",
        "properties": {
          "reseller": {
            "type": "keyword"
          },
          "price": {
            "type": "double"
          }
        }
      }
    }
  }
}

PUT /products/_doc/0?refresh
{
  "name": "LED TV", 
  "resellers": [
    {
      "reseller": "companyA",
      "price": 350
    },
    {
      "reseller": "companyB",
      "price": 500
    }
  ]
}

获取经销商最低价格
GET /products/_search?size=0
{
  "query": {
    "match": {
      "name": "led tv"
    }
  },
  "aggs": {
    "resellers": {
      "nested": {
        "path": "resellers"
      },
      "aggs": {
        "min_price": {
          "min": {
            "field": "resellers.price"
          }
        }
      }
    }
  }
}

响应结果 
{ 
  "aggregations": {
    "resellers": {
      "doc_count": 2,
      "min_price": {
        "value": 350.0
      }
    }
  }
}
```

### 7.2 Metric aggregations 指标聚合

#### 7.2.1 avg aggregation

平均值聚类是单值指标聚类

- `missing`: 指定一个值，用于在文档中缺少该字段时使用。默认情况下，这些文档将被忽略。

```json
POST /exams/_search?size=0
{
  "aggs": {
    "avg_grade": { "avg": { "field": "grade" } }
  }
}

POST /exams/_search?size=0
{
  "aggs": {
    "grade_avg": {
      "avg": {
        "field": "grade",
        "missing": 10     
      }
    }
  }
}
```

`scripts` 使用`runtime field`修正成绩

```json
POST /exams/_search?size=0
{
  "runtime_mappings": {
    "grade.corrected": {
      "type": "double",
      "script": {
        "source": "emit(Math.min(100, doc['grade'].value * params.correction))",
        "params": {
          "correction": 1.2
        }
      }
    }
  },
  "aggs": {
    "avg_corrected_grade": {
      "avg": {
        "field": "grade.corrected"
      }
    }
  }
}
```

`histogram fields`

当在`histogram fields`上计算平均值时，聚合结果是值数组中所有元素的加权平均值，计算时会考虑计数数组中相同位置的数值数量。

```json
PUT metrics_index/_doc/1
{
  "network.name" : "net-1",
  "latency_histo" : {
      "values" : [0.1, 0.2, 0.3, 0.4, 0.5], 
      "counts" : [3, 7, 23, 12, 6] 
   }
}

PUT metrics_index/_doc/2
{
  "network.name" : "net-2",
  "latency_histo" : {
      "values" :  [0.1, 0.2, 0.3, 0.4, 0.5], 
      "counts" : [8, 17, 8, 7, 6] 
   }
}

POST /metrics_index/_search?size=0
{
  "aggs": {
    "avg_latency":
      { "avg": { "field": "latency_histo" }
    }
  }
}

响应结果
{
  "aggregations": {
    "avg_latency": {
      "value": 0.29690721649
    }
  }
}
```

#### 7.2.2 sum aggregation

求和指标聚合是单值指标聚合，用于计算字段值的总和。

- `missing`: 指定一个值，用于在文档中缺少该字段时使用。默认情况下，这些文档将被忽略。

```json
POST /sales/_search?size=0
{
  "query": {
    "constant_score": {
      "filter": {
        "match": { "type": "hat" }
      }
    }
  },
  "aggs": {
    "hat_prices": { "sum": { "field": "price" } }
  }
}

POST /sales/_search?size=0
{ 
  "aggs": {
    "all_prices": {
      "sum": {
        "field": "price",
        "missing": 100 
      }
    }
  }
}
```

`scripts`使用`runtime field`计算促销商品的价格

```json
POST /sales/_search?size=0
{
  "runtime_mappings": {
    "price.weighted": {
      "type": "double",
      "script": """
        double price = doc['price'].value;
        if (doc['promoted'].value) {
          price *= 0.8;
        }
        emit(price);
      """
    }
  },
  "query": {
    "constant_score": {
      "filter": {
        "match": { "type": "hat" }
      }
    }
  },
  "aggs": {
    "hat_prices": {
      "sum": {
        "field": "price.weighted"
      }
    }
  }
}
```

`histogram fields`:当对直方图字段进行求和运算时，聚合结果为值数组中所有元素的总和乘以计数数组中相同位置的数值。

```json
PUT metrics_index
{
  "mappings": {
    "properties": {
      "latency_histo": { "type": "histogram" }
    }
  }
}

PUT metrics_index/_doc/1?refresh
{
  "network.name" : "net-1",
  "latency_histo" : {
      "values" : [0.1, 0.2, 0.3, 0.4, 0.5],
      "counts" : [3, 7, 23, 12, 6]
   }
}

PUT metrics_index/_doc/2?refresh
{
  "network.name" : "net-2",
  "latency_histo" : {
      "values" :  [0.1, 0.2, 0.3, 0.4, 0.5],
      "counts" : [8, 17, 8, 7, 6]
   }
}

POST /metrics_index/_search?size=0&filter_path=aggregations
{
  "aggs" : {
    "total_latency" : { "sum" : { "field" : "latency_histo" } }
  }
}

响应结果
{
  "aggregations": {
    "total_latency": {
      "value": 28.8
    }
  }
}
```

#### 7.2.3 min aggregation

一种单值指标聚合，用于计算字段值的最小值。
最小值和最大值聚合运算基于数据的双精度表示进行。因此，当对绝对值大于2^53的长整型数据进行运算时，所得结果可能仅为近似值。

- `missing`: 指定一个值，用于在文档中缺少该字段时使用。默认情况下，这些文档将被忽略。

```json
POST /sales/_search?size=0
{
  "aggs": {
    "min_price": { "min": { "field": "price" } }
  }
}

POST /sales/_search
{
  "aggs": {
    "grade_min": {
      "min": {
        "field": "grade",
        "missing": 10 
      }
    }
  }
}
```

`scripts`:使用`runtime fields`计算促销商品的最低价格

```json
POST /sales/_search
{
  "size": 0,
  "runtime_mappings": {
    "price.adjusted": {
      "type": "double",
      "script": """
        double price = doc['price'].value;
        if (doc['promoted'].value) {
          price *= 0.8;
        }
        emit(price);
      """
    }
  },
  "aggs": {
    "min_price": {
      "min": { "field": "price.adjusted" }
    }
  }
}
```

`histogram fileds`：计算最小值是`values`数组中所有元素的最小值。请注意，直方图的`counts`数组会被忽略。

```json
PUT metrics_index
{
  "mappings": {
    "properties": {
      "latency_histo": { "type": "histogram" }
    }
  }
}

PUT metrics_index/_doc/1?refresh
{
  "network.name" : "net-1",
  "latency_histo" : {
      "values" : [0.1, 0.2, 0.3, 0.4, 0.5],
      "counts" : [3, 7, 23, 12, 6]
   }
}

PUT metrics_index/_doc/2?refresh
{
  "network.name" : "net-2",
  "latency_histo" : {
      "values" :  [0.1, 0.2, 0.3, 0.4, 0.5],
      "counts" : [8, 17, 8, 7, 6]
   }
}

POST /metrics_index/_search?size=0&filter_path=aggregations
{
  "aggs" : {
    "min_latency" : { "min" : { "field" : "latency_histo" } }
  }
}
```

#### 7.2.4 max aggregation

一种单值指标聚合，用于计算字段值的最小值。
最小值和最大值聚合运算基于数据的双精度表示进行。因此，当对绝对值大于2^53的长整型数据进行运算时，所得结果可能仅为近似值。

- `missing`: 指定一个值，用于在文档中缺少该字段时使用。默认情况下，这些文档将被忽略。

```json
POST /sales/_search?size=0
{
  "aggs": {
    "max_price": { "max": { "field": "price" } }
  }
}

POST /sales/_search
{
  "aggs" : {
      "grade_max" : {
          "max" : {
              "field" : "grade",
              "missing": 10       
          }
      }
  }
}
```

`script`:使用`runtime fields`计算促销商品的最高价格

```json
POST /sales/_search
{
  "size": 0,
  "runtime_mappings": {
    "price.adjusted": {
      "type": "double",
      "script": """
        double price = doc['price'].value;
        if (doc['promoted'].value) {
          price *= 0.8;
        }
        emit(price);
      """
    }
  },
  "aggs": {
    "max_price": {
      "max": { "field": "price.adjusted" }
    }
  }
}
```

`histogram fields`:计算最大值是`values`数组中所有元素的最大值。请注意，直方图的`counts`数组会被忽略。

```json
PUT metrics_index
{
  "mappings": {
    "properties": {
      "latency_histo": { "type": "histogram" }
    }
  }
}

PUT metrics_index/_doc/1?refresh
{
  "network.name" : "net-1",
  "latency_histo" : {
      "values" : [0.1, 0.2, 0.3, 0.4, 0.5],
      "counts" : [3, 7, 23, 12, 6]
   }
}

PUT metrics_index/_doc/2?refresh
{
  "network.name" : "net-2",
  "latency_histo" : {
      "values" :  [0.1, 0.2, 0.3, 0.4, 0.5],
      "counts" : [8, 17, 8, 7, 6]
   }
}

POST /metrics_index/_search?size=0&filter_path=aggregations
{
  "aggs" : {
    "max_latency" : { "max" : { "field" : "latency_histo" } }
  }
}
```

#### 7.2.5 cardinality aggregation

一种单值指标聚合方法，用于计算不同值的近似数量。基于 `HyperLogLog++` 算法，该算法通过值的哈希值进行计数
基数聚合器用于计算字段的基数（即不重复的值）。基数聚合器通常用于计算唯一值的数量，例如计算每个用户有多少个不同的订单。

- `missing`: 指定一个值，用于在文档中缺少该字段时使用。默认情况下，这些文档将被忽略。
- `precision_threshold`:指定一个阈值，低于该阈值时，计数结果预计接近准确。超过这个数值后，计数结果可能会变得有些模糊。支持的最大值为 40000，超过此数值的阈值将与 40000 的阈值产生相同效果。默认值为 3000。

```json
POST /sales/_search?size=0
{
  "aggs": {
    "type_count": {
      "cardinality": {
        "field": "type"
      }
    }
  }
}

POST /sales/_search?size=0
{
  "aggs": {
    "tag_cardinality": {
      "cardinality": {
        "field": "tag",
        "missing": "N/A" 
      }
    }
  }
}
```

`script`:使用`runtime fields`获取两个字段组合的基数

```json
POST /sales/_search?size=0
{
  "runtime_mappings": {
    "type_and_promoted": {
      "type": "keyword",
      "script": "emit(doc['type'].value + ' ' + doc['promoted'].value)"
    }
  },
  "aggs": {
    "type_promoted_count": {
      "cardinality": {
        "field": "type_and_promoted"
      }
    }
  }
}
```

#### 7.2.5 stats aggregation

统计聚合一种多值指标聚合方法，用于对从聚合文档中提取的数值进行统计计算。返回的统计信息包括：`min`, `max`, `avg`, `sum`, `count`。

- `missing`: 指定一个值，用于在文档中缺少该字段时使用。默认情况下，这些文档将被忽略。

```json
POST /exams/_search?size=0
{
  "aggs": {
    "grades_stats": { "stats": { "field": "grade" } }
  }
}

响应结果
{
  "aggregations": {
    "grades_stats": {
      "count": 2,
      "min": 50.0,
      "max": 100.0,
      "avg": 75.0,
      "sum": 150.0
    }
  }
}

POST /exams/_search?size=0
{
  "aggs": {
    "grades_stats": {
      "stats": {
        "field": "grade",
        "missing": 0      
      }
    }
  }
}
```

`script`:使用`runtime field`计算加权统计得分

```json
POST /exams/_search
{
  "size": 0,
  "runtime_mappings": {
    "grade.weighted": {
      "type": "double",
      "script": """
        emit(doc['grade'].value * doc['weight'].value)
      """
    }
  },
  "aggs": {
    "grades_stats": {
      "stats": {
        "field": "grade.weighted"
      }
    }
  }
}
```

#### 7.2.6 rate aggregation

速率指标聚合仅可在`date_histogram`或`composite`聚合内部使用。该功能会计算每个桶中文档或字段的数量。

- `mode`:指定速率聚合器应使用哪种模式来计算速率。支持的模式有：`count`（计算每个桶中文档的数量）和`sum`（计算每个桶中指定字段值的总和）。默认值为`sum`。

```json
GET sales/_search
{
  "size": 0,
  "aggs": {
    "by_date": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"  
      },
      "aggs": {
        "my_rate": {
          "rate": {
            "unit": "year"  
          }
        }
      }
    }
  }
}

响应结果，该响应返回每个区间内的年交易量。由于一年共有12个月，年费率将通过将月费率乘以12自动计算得出。
{
  "aggregations" : {
    "by_date" : {
      "buckets" : [
        {
          "key_as_string" : "2015/01/01 00:00:00",
          "key" : 1420070400000,
          "doc_count" : 3,
          "my_rate" : {
            "value" : 36.0
          }
        },
        {
          "key_as_string" : "2015/02/01 00:00:00",
          "key" : 1422748800000,
          "doc_count" : 2,
          "my_rate" : {
            "value" : 24.0
          }
        }       
      ]
    }
  }
}

GET sales/_search
{
  "size": 0,
  "aggs": {
    "by_date": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "avg_price": {
          "rate": {
            "field": "price",
            "unit": "day"
          }
        }
      }
    }
  }
}

计算每个桶中所有文档字段值的总和，或统计每个桶中的值的数量。该请求将把所有销售记录按月分组，随后计算每月总销售额，并将其转换为日均销售额。
响应结果
{
  "aggregations" : {
    "by_date" : {
      "buckets" : [
        {
          "key_as_string" : "2015/01/01 00:00:00",
          "key" : 1420070400000,
          "doc_count" : 3,
          "avg_price" : {
            "value" : 17.741935483870968
          }
        },
        {
          "key_as_string" : "2015/02/01 00:00:00",
          "key" : 1422748800000,
          "doc_count" : 2,
          "avg_price" : {
            "value" : 2.142857142857143
          }
        }       
      ]
    }
  }
}
```

```json
GET sales/_search?filter_path=aggregations&size=0
{
  "aggs": {
    "buckets": {
      "composite": { 
        "sources": [
          {
            "month": {
              "date_histogram": { 
                "field": "date",
                "calendar_interval": "month"
              }
            }
          },
          {
            "type": { 
              "terms": {
                "field": "type"
              }
            }
          }
        ]
      },
      "aggs": {
        "avg_price": {
          "rate": {
            "field": "price", 
            "unit": "day" 
          }
        }
      }
    }
  }
}

响应结果，将包含每项商品在各月份的平均每日销售价格
{
  "aggregations" : {
    "buckets" : {
      "after_key" : {
        "month" : 1425168000000,
        "type" : "t-shirt"
      },
      "buckets" : [
        {
          "key" : {
            "month" : 1420070400000,
            "type" : "bag"
          },
          "doc_count" : 1,
          "avg_price" : {
            "value" : 4.838709677419355
          }
        },        
        {
          "key" : {
            "month" : 1422748800000,
            "type" : "t-shirt"
          },
          "doc_count" : 1,
          "avg_price" : {
            "value" : 0.35714285714285715
          }
        },       
        {
          "key" : {
            "month" : 1425168000000,
            "type" : "t-shirt"
          },
          "doc_count" : 1,
          "avg_price" : {
            "value" : 5.645161290322581
          }
        }
      ]
    }
  }
}
```

`mode`:使用`value_count`参数，可以计算每个桶中文档的数量。

```json
GET sales/_search
{
  "size": 0,
  "aggs": {
    "by_date": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"  
      },
      "aggs": {
        "avg_number_of_sales_per_year": {
          "rate": {
            "field": "price", 
            "unit": "year",  
            "mode": "value_count" 
          }
        }
      }
    }
  }
}

响应结果，包含各月份的平均每日销售价格
{
  "aggregations" : {
    "by_date" : {
      "buckets" : [
        {
          "key_as_string" : "2015/01/01 00:00:00",
          "key" : 1420070400000,
          "doc_count" : 3,
          "avg_number_of_sales_per_year" : {
            "value" : 36.0
          }
        },
        {
          "key_as_string" : "2015/02/01 00:00:00",
          "key" : 1422748800000,
          "doc_count" : 2,
          "avg_number_of_sales_per_year" : {
            "value" : 24.0
          }
        }       
      ]
    }
  }
}
```

`bucket size`和`rate`的关系

`rate`聚合支持所有可用于 `date_histogram` 聚合的 `calendar_intervals` 参数中的费率。指定的速率应与日期直方图聚合间隔兼容，即应能够将桶大小转换为相应的速率。默认情况下使用 `date_histogram` 的时间间隔。

如果`date_histogram`并非`rate`的直接父级，`rate interval`与`date_histogram interval`必须属于同一组：`[second,minute,hour,day,week]`或`[month,quarter,year]`。

`script`:使用`runtime field`

```json
GET sales/_search
{
  "size": 0,
  "runtime_mappings": {
    "price.adjusted": {
      "type": "double",
      "script": {
        "source": "emit(doc['price'].value * params.adjustment)",
        "params": {
          "adjustment": 0.9
        }
      }
    }
  },
  "aggs": {
    "by_date": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "avg_price": {
          "rate": {
            "field": "price.adjusted"
          }
        }
      }
    }
  }
}

响应结果
{
  "aggregations" : {
    "by_date" : {
      "buckets" : [
        {
          "key_as_string" : "2015/01/01 00:00:00",
          "key" : 1420070400000,
          "doc_count" : 3,
          "avg_price" : {
            "value" : 495.0
          }
        },
        {
          "key_as_string" : "2015/02/01 00:00:00",
          "key" : 1422748800000,
          "doc_count" : 2,
          "avg_price" : {
            "value" : 54.0
          }
        }        
      ]
    }
  }
}
```

#### 7.2.7 value count aggregation

一种单值指标聚合方法，用于统计从聚合文档中提取出的数值数量。计数聚合器通常用于计算每个分桶中的文档数量，例如计算每个用户有多少个订单。
`value_count`功能不会对数值进行去重处理，因此即使某个字段存在重复值，每个数值仍会被单独计数。

```json
POST /sales/_search?size=0
{
  "aggs" : {
    "types_count" : { "value_count" : { "field" : "type" } }
  }
}
```

`script`使用`runtime field`

```json
POST /sales/_search
{
  "size": 0,
  "runtime_mappings": {
    "tags": {
      "type": "keyword",
      "script": """
        emit(doc['type'].value);
        if (doc['promoted'].value) {
          emit('hot');
        }
      """
    }
  },
  "aggs": {
    "tags_count": {
      "value_count": {
        "field": "tags"
      }
    }
  }
}
```

`histogram fields`:当对`histogram fields`执行 `value_count` 聚合运算时，聚合结果即为`histogram` `counts` 数组中所有数值的总和。

对于以下存储不同网络延迟指标预聚合直方图的索引

```json
PUT metrics_index/_doc/1
{
  "network.name" : "net-1",
  "latency_histo" : {
      "values" : [0.1, 0.2, 0.3, 0.4, 0.5],
      "counts" : [3, 7, 23, 12, 6] 
   }
}

PUT metrics_index/_doc/2
{
  "network.name" : "net-2",
  "latency_histo" : {
      "values" :  [0.1, 0.2, 0.3, 0.4, 0.5],
      "counts" : [8, 17, 8, 7, 6] 
   }
}

POST /metrics_index/_search?size=0
{
  "aggs": {
    "total_requests": {
      "value_count": { "field": "latency_histo" }
    }
  }
}

响应结果
{
  ...
  "aggregations": {
    "total_requests": {
      "value": 97
    }
  }
}
```

#### 7.2.8 top hits aggregation

`topHits`指标聚合器用于追踪当前正在聚合的最相关文档。该聚合器旨在作为子聚合器使用，以便能够按桶对匹配度最高的文档进行聚合。
不建议将 `topHits` 用作顶级聚合指标。请使用 `collapse` 参数对搜索结果进行分组。

- `from`:与获取的第一个结果的偏移量
- `size`:每个桶返回的最大文档数量，默认匹配度最高的前3条结果
- `sort`:指定文档排序方式，默认按查询得分降序排序

`top_hits`聚合功能返回常规搜索结果，因此能够支持每个结果包含多个功能：
`Highlighting`
`Explain`
`Named queries`
`Search fields`
`Source filtering`
`Stored fields`
`Script fields`
`Doc value fields`
`Include versions`
`Include Sequence Numbers and Primary Terms`

仅需`docvalue_fields`、`size`和`sort`字段，那么`Top Metrics`可能比`Top Hits Aggregation`更为高效。
`top_hits` 不支持 `rescore` 参数。查询重新评分仅适用于搜索结果，不适用于聚合结果。使用 `function_score` 或 `script_score` 查询更改聚合计算所使用的评分。

```json
POST /sales/_search?size=0
{
  "aggs": {
    "top_tags": {
      "terms": {
        "field": "type",
        "size": 3
      },
      "aggs": {
        "top_sales_hits": {
          "top_hits": {
            "sort": [
              {
                "date": {
                  "order": "desc"
                }
              }
            ],
            "_source": {
              "includes": [ "date", "price" ]
            },
            "size": 1
          }
        }
      }
    }
  }
}
响应结果
{
  "aggregations": {
    "top_tags": {
       "doc_count_error_upper_bound": 0,
       "sum_other_doc_count": 0,
       "buckets": [
          {
             "key": "hat",
             "doc_count": 3,
             "top_sales_hits": {
                "hits": {
                   "total" : {
                       "value": 3,
                       "relation": "eq"
                   },
                   "max_score": null,
                   "hits": [
                      {
                         "_index": "sales",
                         "_id": "AVnNBmauCQpcRyxw6ChK",
                         "_source": {
                            "date": "2015/03/01 00:00:00",
                            "price": 200
                         },
                         "sort": [
                            1425168000000
                         ],
                         "_score": null
                      }
                   ]
                }
             }
          },
          {
             "key": "t-shirt",
             "doc_count": 3,
             "top_sales_hits": {
                "hits": {
                   "total" : {
                       "value": 3,
                       "relation": "eq"
                   },
                   "max_score": null,
                   "hits": [
                      {
                         "_index": "sales",
                         "_id": "AVnNBmauCQpcRyxw6ChL",
                         "_source": {
                            "date": "2015/03/01 00:00:00",
                            "price": 175
                         },
                         "sort": [
                            1425168000000
                         ],
                         "_score": null
                      }
                   ]
                }
             }
          }          
       ]
    }
  }
}
```

#### 7.2.9 top metrics aggregation

`top_metrics`聚合功能会从文档中选取`sort`值最大或最小的指标

`metrics` 中的`sort`有限制

- 无法应用于`binary`、`flattened`、`IP`、`keyword`或`text`字段。
- 仅支持单一排序值，因此未明确规定出现平局时应以何种文档为准。

- `sort`
  - `"sort":{ "s":"desc"}`:从文档中获取评分最高的指标
  - `"sort":{ "s":"asc"}`:从文档中获取评分最低的指标
  - `"sort":{ "_geo_distance":{"location": "POINT (-78.6382 35.7796)"}}`:从地理位置最接近 35.7796，-78.6382 的文档中获取指标数据

`metrics`使用`"metrics": [{"field": "m"}, {"field": "i"}`获取多指标数据
`metrics field`类型支持`boolean`,`ip`,`keywords`,`numbers`,`runtime fields`

```json
POST /test/_bulk?refresh
{"index": {}}
{"s": 1, "m": 3.1415}
{"index": {}}
{"s": 2, "m": 1.0}
{"index": {}}
{"s": 3, "m": 2.71828}

获取文档中 s 值最大的 m 字段的值：
POST /test/_search?filter_path=aggregations
{
  "aggs": {
    "tm": {
      "top_metrics": {
        "metrics": {"field": "m"},
        "sort": {"s": "desc"}
      }
    }
  }
}
响应结果
{
  "aggregations": {
    "tm": {
      "top": [ {"sort": [3], "metrics": {"m": 2.718280076980591 } } ]
    }
  }
}
```

`多指标数据`

```json
PUT /test
{
  "mappings": {
    "properties": {
      "d": {"type": "date"}
    }
  }
}
POST /test/_bulk?refresh
{"index": {}}
{"s": 1, "m": 3.1415, "i": 1, "d": "2020-01-01T00:12:12Z", "t": "cat"}
{"index": {}}
{"s": 2, "m": 1.0, "i": 6, "d": "2020-01-02T00:12:12Z", "t": "dog"}
{"index": {}}
{"s": 3, "m": 2.71828, "i": -12, "d": "2019-12-31T00:12:12Z", "t": "chicken"}
POST /test/_search?filter_path=aggregations
{
  "aggs": {
    "tm": {
      "top_metrics": {
        "metrics": [
          {"field": "m"},
          {"field": "i"},
          {"field": "d"},
          {"field": "t.keyword"}
        ],
        "sort": {"s": "desc"}
      }
    }
  }
}

响应结果
{
  "aggregations": {
    "tm": {
      "top": [ {
        "sort": [3],
        "metrics": {
          "m": 2.718280076980591,
          "i": -12,
          "d": "2019-12-31T00:12:12.000Z",
          "t.keyword": "chicken"
        }
      } ]
    }
  }
}
```

`missing`:缺失参数用于定义对数值缺失的文档的处理方式。默认情况下，如果任何关键组件缺失，整个文档将被忽略。通过使用缺失参数，可以将缺失的组成部分视为具有数值进行处理。

```json
PUT /my-index
{
  "mappings": {
    "properties": {
      "nr":    { "type": "integer" },
      "state":  { "type": "keyword"  } 
    }
  }
}
POST /my-index/_bulk?refresh
{"index": {}}
{"nr": 1, "state": "started"}
{"index": {}}
{"nr": 3, "state": "N/A"}
{"index": {}}
{"nr": 4} 
POST /my-index/_search?filter_path=aggregations
{
  "aggs": {
    "my_top_metrics": {
      "top_metrics": {
        "metrics": {
          "field": "state",
          "missing": "N/A"}, 
        "sort": {"nr": "desc"}
      }
    }
  }
}
响应结果
{
  "aggregations": {
    "my_top_metrics": {
      "top": [
        {
          "sort": [
            4
          ],
          "metrics": {
            "state": "N/A"
          }
        }
      ]
    }
  }
}
```

`size`:默认大小为1。最大默认大小为10，因为聚合操作的工作存储采用“密集”模式，为每个桶分配存储空间。10 是一个非常保守的默认最大值，通过`top_metrics_max_size` 索引设置修改

```json
POST /test/_bulk?refresh
{"index": {}}
{"s": 1, "m": 3.1415}
{"index": {}}
{"s": 2, "m": 1.0}
{"index": {}}
{"s": 3, "m": 2.71828}
POST /test/_search?filter_path=aggregations
{
  "aggs": {
    "tm": {
      "top_metrics": {
        "metrics": {"field": "m"},
        "sort": {"s": "desc"},
        "size": 3
      }
    }
  }
}
响应结果
{
  "aggregations": {
    "tm": {
      "top": [
        {"sort": [3], "metrics": {"m": 2.718280076980591 } },
        {"sort": [2], "metrics": {"m": 1.0 } },
        {"sort": [1], "metrics": {"m": 3.1414999961853027 } }
      ]
    }
  }
}

PUT /test/_settings
{
  "top_metrics_max_size": 100
}
```

`混合类型数据排序`：浮点型字段的排序始终独立于整数型字段进行

```json
POST /test/_bulk?refresh
{"index": {"_index": "test1"}}
{"s": 1, "m": 3.1415}
{"index": {"_index": "test1"}}
{"s": 2, "m": 1}
{"index": {"_index": "test2"}}
{"s": 3.1, "m": 2.71828}
POST /test*/_search?filter_path=aggregations
{
  "aggs": {
    "tm": {
      "top_metrics": {
        "metrics": {"field": "m"},
        "sort": {"s": {"order": "asc", "numeric_type": "double"}}
      }
    }
  }
}
响应结果
{
  "aggregations": {
    "tm": {
      "top": [ {"sort": [1.0], "metrics": {"m": 3.1414999961853027 } } ]
    }
  }
}
```

### 7.3 Pipeline aggregations 管道聚合

#### 7.3.1 average bucket aggregation

一种兄弟数据管道聚合方法，用于计算兄弟聚合中指定指标的平均值。指定的度量指标必须为数值型，且兄弟聚合必须为多桶聚合。

`parameters`

- `buckets_path`:（必填，字符串）用于计算平均值的桶路径。
- `gap_policy`:（可选，字符串）指定在计算平均值时遇到空桶时的行为。默认为`skip`。
  - `insert_zeros`:遇到空桶时，将插入零值。
  - `keep_values`:遇到非空且非NA值，将保留原始值,否则跳转空桶。
  - `skip`:遇到空桶时，将跳过该桶。
- `format`:（可选，字符串）用于输出值的`DecimalFormat pattern`。如指定，格式化后的值将通过聚合结果的 `value_as_string` 属性返回。

`response body`

- `value`:（浮点数）在 buckets_path 中指定的度量指标的平均值。
- `value_as_string`:（字符串）聚合操作的格式化输出值。仅当请求中指定了`format`时，才会提供此属性。

```json
POST _search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "sales": {
          "sum": {
            "field": "price"
          }
        }
      }
    },
    "avg_monthly_sales": {  
      "avg_bucket": {
        "buckets_path": "sales_per_month>sales",
        "gap_policy": "skip",
        "format": "#,##0.00;(#,##0.00)"
      }
    }
  }
}

响应结果，avg_monthly_sales 中 sales_per_month>sales 表示 聚合计算了所有月份的销售额的平均值
{
  "aggregations": {
    "sales_per_month": {
      "buckets": [
        {
          "key_as_string": "2015/01/01 00:00:00",
          "key": 1420070400000,
          "doc_count": 3,
          "sales": {
            "value": 550.0
          }
        },
        {
          "key_as_string": "2015/02/01 00:00:00",
          "key": 1422748800000,
          "doc_count": 2,
          "sales": {
            "value": 60.0
          }
        },
        {
          "key_as_string": "2015/03/01 00:00:00",
          "key": 1425168000000,
          "doc_count": 2,
          "sales": {
            "value": 375.0
          }
        }
      ]
    },
    "avg_monthly_sales": {
      "value": 328.33333333333333,
      "value_as_string": "328.33"
    }
  }
}
```

#### 7.3.2 sum bucket aggregation

一种兄弟聚合管道聚合方法，用于计算兄弟聚合中指定指标所有分桶数据的总和。指定的度量指标必须为数值型，且兄弟聚合必须采用多桶聚合方式。

- `buckets_path`:（必填，字符串）用于计算总和的桶路径。
- `gap_policy`:（可选，字符串）指定在计算总和时遇到空桶时的行为。默认为`skip`。
  - `insert_zeros`:遇到空桶时，将插入零值。
  - `keep_values`:遇到非空且非NA值，将保留原始值,否则跳转空桶。
  - `skip`:遇到空桶时，将跳过该桶。
- `format`:（可选，字符串）输出值的`DecimalFormat pattern`。如指定，则格式化后的值将返回到聚合结果的 `value_as_string` 属性中

```json
POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "sales": {
          "sum": {
            "field": "price"
          }
        }
      }
    },
    "sum_monthly_sales": {
      "sum_bucket": {
        "buckets_path": "sales_per_month>sales" 
      }
    }
  }
}
响应结果，sum_monthly_sales 中 sales_per_month>sales 表示 聚合计算了所有月份的销售额总和
{
   "aggregations": {
      "sales_per_month": {
         "buckets": [
            {
               "key_as_string": "2015/01/01 00:00:00",
               "key": 1420070400000,
               "doc_count": 3,
               "sales": {
                  "value": 550.0
               }
            },
            {
               "key_as_string": "2015/02/01 00:00:00",
               "key": 1422748800000,
               "doc_count": 2,
               "sales": {
                  "value": 60.0
               }
            },
            {
               "key_as_string": "2015/03/01 00:00:00",
               "key": 1425168000000,
               "doc_count": 2,
               "sales": {
                  "value": 375.0
               }
            }
         ]
      },
      "sum_monthly_sales": {
          "value": 985.0
      }
   }
}
```

#### 7.3.3 min bucket aggregation

一种兄弟聚合管道聚合方法，用于识别兄弟聚合中特定指标取值最小的桶，并输出该桶的数值及其对应的键值。指定的度量指标必须为数值型，且兄弟聚合必须采用多桶聚合方式。

- `buckets_path`:（必填，字符串）用于计算最小值的桶路径。
- `gap_policy`:（可选，字符串）指定在计算总和时遇到空桶时的行为。默认为`skip`。
  - `insert_zeros`:遇到空桶时，将插入零值。
  - `keep_values`:遇到非空且非NA值，将保留原始值,否则跳转空桶。
  - `skip`:遇到空桶时，将跳过该桶。
- `format`:（可选，字符串）输出值的`DecimalFormat pattern`。如指定，则格式化后的值将返回到聚合结果的 `value_as_string` 属性中

```json
POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "sales": {
          "sum": {
            "field": "price"
          }
        }
      }
    },
    "min_monthly_sales": {
      "min_bucket": {
        "buckets_path": "sales_per_month>sales" 
      }
    }
  }
}
响应结果，min_monthly_sales 中 sales_per_month>sales 表示聚合计算了所有月份的销售额最小值

{
   "aggregations": {
      "sales_per_month": {
         "buckets": [
            {
               "key_as_string": "2015/01/01 00:00:00",
               "key": 1420070400000,
               "doc_count": 3,
               "sales": {
                  "value": 550.0
               }
            },
            {
               "key_as_string": "2015/02/01 00:00:00",
               "key": 1422748800000,
               "doc_count": 2,
               "sales": {
                  "value": 60.0
               }
            },
            {
               "key_as_string": "2015/03/01 00:00:00",
               "key": 1425168000000,
               "doc_count": 2,
               "sales": {
                  "value": 375.0
               }
            }
         ]
      },
      "min_monthly_sales": {
          "keys": ["2015/02/01 00:00:00"], 
          "value": 60.0
      }
   }
}
min_monthly_sales.keys 是一个字符串数组，因为最小值可能存在于多个桶中
```

#### 7.3.4 max bucket aggregation

一种兄弟聚合管道聚合方法，用于识别兄弟聚合中特定指标取值最大的桶，并输出该桶的数值及其对应的键值。指定的度量指标必须为数值型，且兄弟聚合必须采用多桶聚合方式。

- `buckets_path`:（必填，字符串）用于计算最大值的桶路径。
- `gap_policy`:（可选，字符串）指定在计算总和时遇到空桶时的行为。默认为`skip`。
  - `insert_zeros`:遇到空桶时，将插入零值。
  - `keep_values`:遇到非空且非NA值，将保留原始值,否则跳转空桶。
  - `skip`:遇到空桶时，将跳过该桶。
- `format`:（可选，字符串）输出值的`DecimalFormat pattern`。如指定，则格式化后的值将返回到聚合结果的 `value_as_string` 属性中

```json
POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "sales": {
          "sum": {
            "field": "price"
          }
        }
      }
    },
    "max_monthly_sales": {
      "max_bucket": {
        "buckets_path": "sales_per_month>sales" 
      }
    }
  }
}
响应结果，max_monthly_sales 中 sales_per_month>sales 表示聚合计算了所有月份的销售额最大值

{
   "aggregations": {
      "sales_per_month": {
         "buckets": [
            {
               "key_as_string": "2015/01/01 00:00:00",
               "key": 1420070400000,
               "doc_count": 3,
               "sales": {
                  "value": 550.0
               }
            },
            {
               "key_as_string": "2015/02/01 00:00:00",
               "key": 1422748800000,
               "doc_count": 2,
               "sales": {
                  "value": 60.0
               }
            },
            {
               "key_as_string": "2015/03/01 00:00:00",
               "key": 1425168000000,
               "doc_count": 2,
               "sales": {
                  "value": 375.0
               }
            }
         ]
      },
      "max_monthly_sales": {
          "keys": ["2015/01/01 00:00:00"], 
          "value": 550.0
      }
   }
}
max_monthly_sales.keys 是一个字符串数组，因为最大值可能存在于多个桶中
```

#### 7.3.5 stats bucket aggregation

一种兄弟聚合管道聚合功能，可计算指定指标在兄弟聚合中所有分桶内的各项统计指标。指定的度量指标必须为数值型，且兄弟聚合必须采用多桶聚合方式。

- `buckets_path`:（必填，字符串）用于计算统计指标的桶路径。
- `gap_policy`:（可选，字符串）指定在计算总和时遇到空桶时的行为。默认为`skip`。
  - `insert_zeros`:遇到空桶时，将插入零值。
  - `keep_values`:遇到非空且非NA值，将保留原始值,否则跳转空桶。
  - `skip`:遇到空桶时，将跳过该桶。
- `format`:（可选，字符串）输出值的`DecimalFormat pattern`。如指定，则格式化后的值将返回到聚合结果的 `value_as_string` 属性中

```json
POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "sales": {
          "sum": {
            "field": "price"
          }
        }
      }
    },
    "stats_monthly_sales": {
      "stats_bucket": {
        "buckets_path": "sales_per_month>sales" 
      }
    }
  }
}
响应结果，stats_monthly_sales 中 sales_per_month>sales 表示聚合计算了所有月份的销售额的各项统计指标
{
   "aggregations": {
      "sales_per_month": {
         "buckets": [
            {
               "key_as_string": "2015/01/01 00:00:00",
               "key": 1420070400000,
               "doc_count": 3,
               "sales": {
                  "value": 550.0
               }
            },
            {
               "key_as_string": "2015/02/01 00:00:00",
               "key": 1422748800000,
               "doc_count": 2,
               "sales": {
                  "value": 60.0
               }
            },
            {
               "key_as_string": "2015/03/01 00:00:00",
               "key": 1425168000000,
               "doc_count": 2,
               "sales": {
                  "value": 375.0
               }
            }
         ]
      },
      "stats_monthly_sales": {
         "count": 3,
         "min": 60.0,
         "max": 550.0,
         "avg": 328.3333333333333,
         "sum": 985.0
      }
   }
}
```

#### 7.3.6 percentiles bucket aggregation

一种兄弟聚合管道聚合方法，用于计算兄弟聚合中指定指标所有分桶数据的百分位数。指定的度量指标必须为数值型，且兄弟聚合必须采用多桶聚合方式。
百分位数是精确计算得出的，而非近似值

- `buckets_path`:（必填，字符串）用于计算百分数的桶路径。
- `gap_policy`:（可选，字符串）指定在计算总和时遇到空桶时的行为。默认为`skip`。
  - `insert_zeros`:遇到空桶时，将插入零值。
  - `keep_values`:遇到非空且非NA值，将保留原始值,否则跳转空桶。
  - `skip`:遇到空桶时，将跳过该桶。
- `format`:（可选，字符串）输出值的`DecimalFormat pattern`。如指定，则格式化后的值将返回到聚合结果的 `value_as_string` 属性中
- `percents`:（可选，数组）指定要计算的百分位数。默认为[1.0, 5.0, 25.0, 50.0, 75.0, 95.0, 99.0]
- `keyed`:（可选，布尔值）该标志将范围作为哈希值返回，而非键值对数组。。默认为`true`

```json
POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "sales": {
          "sum": {
            "field": "price"
          }
        }
      }
    },
    "percentiles_monthly_sales": {
      "percentiles_bucket": {
        "buckets_path": "sales_per_month>sales", 
        "percents": [ 25.0, 50.0, 75.0 ]         
      }
    }
  }
}
响应结果，percentiles_monthly_sales 中 sales_per_month>sales 计算了每月总销售额各区间对应的百分位数
{
   "aggregations": {
      "sales_per_month": {
         "buckets": [
            {
               "key_as_string": "2015/01/01 00:00:00",
               "key": 1420070400000,
               "doc_count": 3,
               "sales": {
                  "value": 550.0
               }
            },
            {
               "key_as_string": "2015/02/01 00:00:00",
               "key": 1422748800000,
               "doc_count": 2,
               "sales": {
                  "value": 60.0
               }
            },
            {
               "key_as_string": "2015/03/01 00:00:00",
               "key": 1425168000000,
               "doc_count": 2,
               "sales": {
                  "value": 375.0
               }
            }
         ]
      },
      "percentiles_monthly_sales": {
        "values" : {
            "25.0": 375.0,
            "50.0": 375.0,
            "75.0": 550.0
         }
      }
   }
}

25.0: 25%的月销售额在375.0以下。
50.0: 50%的月销售额在375.0以下（中位数）。
75.0: 75%的月销售额在550.0以下。
```

#### 7.3.7 bucket script aggregation

一种父级管道聚合机制，可执行脚本，该脚本能够在父级多桶聚合中对指定指标进行每个桶的计算。指定的度量指标必须为数值类型，且脚本必须返回数值。

`语法`

```json
{
  "bucket_script": {
    "buckets_path": {
      "my_var1": "the_sum",                     
      "my_var2": "the_value_count"
    },
    "script": "params.my_var1 / params.my_var2"
  }
}
my_var1 是该 buckets 路径在脚本中使用的变量名称，the_sum是该变量所使用的指标路径。
```

`bucket_script` Parameters

- `script`:（必填，字符串）指定要执行的脚本。脚本必须返回数值。脚本可以是内联脚本、文件脚本或索引脚本。
- `buckets_path`:（必填，对象）指定要使用的指标路径。每个路径必须指定一个唯一的变量名称，该名称将在脚本中引用。
- `gap_policy`:（可选，字符串）指定在计算总和时遇到空桶时的行为。默认为`skip`
  - `insert_zeros`:遇到空桶时，将插入零值。
  - `keep_values`:遇到非空且非NA值，将保留原始值,否则跳转空桶。
  - `skip`:遇到空桶时，将跳过该桶。
- `format`:（可选，字符串）输出值的`DecimalFormat pattern`。如指定，则格式化后的值将返回到聚合结果的 `value_as_string` 属性中

```json
计算每月T恤销售额占总销售额的百分比

POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "total_sales": {
          "sum": {
            "field": "price"
          }
        },
        "t-shirts": {
          "filter": {
            "term": {
              "type": "t-shirt"
            }
          },
          "aggs": {
            "sales": {
              "sum": {
                "field": "price"
              }
            }
          }
        },
        "t-shirt-percentage": {
          "bucket_script": {
            "buckets_path": {
              "tShirtSales": "t-shirts>sales",
              "totalSales": "total_sales"
            },
            "script": "params.tShirtSales / params.totalSales * 100"
          }
        }
      }
    }
  }
}
响应结果
{  
   "aggregations": {
      "sales_per_month": {
         "buckets": [
            {
               "key_as_string": "2015/01/01 00:00:00",
               "key": 1420070400000,
               "doc_count": 3,
               "total_sales": {
                   "value": 550.0
               },
               "t-shirts": {
                   "doc_count": 1,
                   "sales": {
                       "value": 200.0
                   }
               },
               "t-shirt-percentage": {
                   "value": 36.36363636363637
               }
            },
            {
               "key_as_string": "2015/02/01 00:00:00",
               "key": 1422748800000,
               "doc_count": 2,
               "total_sales": {
                   "value": 60.0
               },
               "t-shirts": {
                   "doc_count": 1,
                   "sales": {
                       "value": 10.0
                   }
               },
               "t-shirt-percentage": {
                   "value": 16.666666666666664
               }
            },
            {
               "key_as_string": "2015/03/01 00:00:00",
               "key": 1425168000000,
               "doc_count": 2,
               "total_sales": {
                   "value": 375.0
               },
               "t-shirts": {
                   "doc_count": 1,
                   "sales": {
                       "value": 175.0
                   }
               },
               "t-shirt-percentage": {
                   "value": 46.666666666666664
               }
            }
         ]
      }
   }
}
```

#### 7.3.8 bucket selector aggregation

一种父级管道聚合操作，会执行一个脚本来判断当前桶是否会被保留在父级多桶聚合中。指定的度量指标必须为数值类型，且脚本必须返回布尔值。如果脚本语言是表达式，则允许返回数值。在此情况下，0.0 将被判定为 `false`，而所有其他数值均将被判定为 `true`

`语法`

```json
{
  "bucket_selector": {
    "buckets_path": {
      "my_var1": "the_sum",                     
      "my_var2": "the_value_count"
    },
    "script": "params.my_var1 > params.my_var2"
  }
}
my_var1 是该 buckets 路径在脚本中使用的变量名称，the_sum是该变量所使用的指标路径。
```

`bucket_script` Parameters

- `script`:（必填，字符串）指定要执行的脚本。脚本必须返回数值。脚本可以是内联脚本、文件脚本或索引脚本。
- `buckets_path`:（必填，对象）指定要使用的指标路径。每个路径必须指定一个唯一的变量名称，该名称将在脚本中引用。
- `gap_policy`:（可选，字符串）指定在计算总和时遇到空桶时的行为。默认为`skip`
  - `insert_zeros`:遇到空桶时，将插入零值。
  - `keep_values`:遇到非空且非NA值，将保留原始值,否则跳转空桶。
  - `skip`:遇到空桶时，将跳过该桶。

```json
保留当月销售额超过200的分类桶。

POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "total_sales": {
          "sum": {
            "field": "price"
          }
        },
        "sales_bucket_filter": {
          "bucket_selector": {
            "buckets_path": {
              "totalSales": "total_sales"
            },
            "script": "params.totalSales > 200"
          }
        }
      }
    }
  }
}
响应结果
{
   "aggregations": {
      "sales_per_month": {
         "buckets": [
            {
               "key_as_string": "2015/01/01 00:00:00",
               "key": 1420070400000,
               "doc_count": 3,
               "total_sales": {
                   "value": 550.0
               }
            },
            {
               "key_as_string": "2015/03/01 00:00:00",
               "key": 1425168000000,
               "doc_count": 2,
               "total_sales": {
                   "value": 375.0
               }
            }
         ]
      }
   }
}
2015年2月1日00:00:00的销售记录已被移除，因其月销售额低于200。
```

#### 7.3.9 bucket sort aggregation

一种父级管道聚合函数，用于对其父级多桶聚合函数的桶进行排序。可指定一个或多个排序字段及其对应的排序顺序。每个桶可根据`_key`、`_count`或子聚合结果进行排序

`语法`

```json
{
  "bucket_sort": {
    "sort": [
      { "sort_field_1": { "order": "asc" } },   
      { "sort_field_2": { "order": "desc" } },
      "sort_field_3"
    ],
    "from": 1,
    "size": 3
  }
}
```

`bucket_sort Parameters`

- `sort` ：（可选）排序字段列表。每个字段可以指定一个排序顺序（`asc` 或 `desc`），也可以省略排序顺序，此时默认为 `asc`。
- `from` ：（可选）指定要返回的桶的起始位置。默认为 `0`。
- `size` ：（可选）指定要返回的桶的数量。默认使用父聚合的所有桶。
- `gap_policy`:（可选，字符串）指定在计算总和时遇到空桶时的行为。默认为`skip`
  - `insert_zeros`:遇到空桶时，将插入零值。
  - `keep_values`:遇到非空且非NA值，将保留原始值,否则跳转空桶。
  - `skip`:遇到空桶时，将跳过该桶。

```json
按降序返回月销售额最高的三个月对应的桶
POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "total_sales": {
          "sum": {
            "field": "price"
          }
        },
        "sales_bucket_sort": {
          "bucket_sort": {
            "sort": [
              { "total_sales": { "order": "desc" } } 
            ],
            "size": 3                                
          }
        }
      }
    }
  }
}
响应结果
{
   "aggregations": {
      "sales_per_month": {
         "buckets": [
            {
               "key_as_string": "2015/01/01 00:00:00",
               "key": 1420070400000,
               "doc_count": 3,
               "total_sales": {
                   "value": 550.0
               }
            },
            {
               "key_as_string": "2015/03/01 00:00:00",
               "key": 1425168000000,
               "doc_count": 2,
               "total_sales": {
                   "value": 375.0
               }
            },
            {
               "key_as_string": "2015/02/01 00:00:00",
               "key": 1422748800000,
               "doc_count": 2,
               "total_sales": {
                   "value": 60.0
               }
            }
         ]
      }
   }
}
```

```json
不排序，只返回前1个桶
POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "bucket_truncate": {
          "bucket_sort": {
            "from": 1,
            "size": 1
          }
        }
      }
    }
  }
}
```

#### 7.3.10 cumulative cardinality aggregation

一种父级管道聚合函数，用于计算父级`histogram`（或`date histogram`）聚合中的累积基数。
累积基数度聚合函数可用于统计“新增总数”，例如计算网站每日的新访客数量。常规的基数聚合功能可显示每日独立访客数量，但无法区分“新访客”与“重复访客”。累积基数聚合功能可用于统计每日独立访客中“新访客”的数量。

`语法`

```json
{
  "cumulative_cardinality": {
    "buckets_path": "my_cardinality_agg"
  }
}
```

- `buckets_path` ：（必需）指定父级基数聚合的路径。
- `format`:（可选，字符串）输出值的`DecimalFormat pattern`。如指定，则格式化后的值将返回到聚合结果的 `value_as_string` 属性中

```json
在查询中添加derivative aggregation导数聚合来实现

GET /user_hits/_search
{
  "size": 0,
  "aggs": {
    "users_per_day": {
      "date_histogram": {
        "field": "timestamp",
        "calendar_interval": "day"
      },
      "aggs": {
        "distinct_users": {
          "cardinality": {
            "field": "user_id"
          }
        },
        "total_new_users": {
          "cumulative_cardinality": {
            "buckets_path": "distinct_users"
          }
        },
        "incremental_new_users": {
          "derivative": {
            "buckets_path": "total_new_users"
          }
        }
      }
    }
  }
}
响应结果
{
   "aggregations": {
      "users_per_day": {
         "buckets": [
            {
               "key_as_string": "2019-01-01T00:00:00.000Z",
               "key": 1546300800000,
               "doc_count": 2,
               "distinct_users": {
                  "value": 2
               },
               "total_new_users": {
                  "value": 2
               }
            },
            {
               "key_as_string": "2019-01-02T00:00:00.000Z",
               "key": 1546387200000,
               "doc_count": 2,
               "distinct_users": {
                  "value": 2
               },
               "total_new_users": {
                  "value": 3
               },
               "incremental_new_users": {
                  "value": 1.0
               }
            }            
         ]
      }
   }
}
```

#### 7.3.11 cumulative sum aggregation

父级管道聚合函数，用于计算父级直方图（或日期直方图）聚合中指定指标的累积总和。

`语法`

```json
{
  "cumulative_sum": {
    "buckets_path": "the_sum"
  }
}
```

- `buckets_path` ：（必需）计算累计和的桶所在路径
- `format`:（可选，字符串）输出值的`DecimalFormat pattern`。如指定，则格式化后的值将返回到聚合结果的 `value_as_string` 属性中

```json
计算每月总销售额的累计总额
POST /sales/_search
{
  "size": 0,
  "aggs": {
    "sales_per_month": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      },
      "aggs": {
        "sales": {
          "sum": {
            "field": "price"
          }
        },
        "cumulative_sales": {
          "cumulative_sum": {
            "buckets_path": "sales" 
          }
        }
      }
    }
  }
}
响应结果
{
   "took": 11,
   "timed_out": false,
   "_shards": ...,
   "hits": ...,
   "aggregations": {
      "sales_per_month": {
         "buckets": [
            {
               "key_as_string": "2015/01/01 00:00:00",
               "key": 1420070400000,
               "doc_count": 3,
               "sales": {
                  "value": 550.0
               },
               "cumulative_sales": {
                  "value": 550.0
               }
            },
            {
               "key_as_string": "2015/02/01 00:00:00",
               "key": 1422748800000,
               "doc_count": 2,
               "sales": {
                  "value": 60.0
               },
               "cumulative_sales": {
                  "value": 610.0
               }
            },
            {
               "key_as_string": "2015/03/01 00:00:00",
               "key": 1425168000000,
               "doc_count": 2,
               "sales": {
                  "value": 375.0
               },
               "cumulative_sales": {
                  "value": 985.0
               }
            }
         ]
      }
   }
}
```

## 8. 数据迁移

### 8.1 在线迁移

```json
# 使用reindex API将数据迁移到新索引
POST _reindex
{    
    "dest": {
        "index": "dest_index"
    },    
    "source": {
        "index": "source_index"        
    }
}
```

### 8.2 离线迁移

使用快照与恢复（Snapshot & Restore）

```json
# 1.在源集群创建快照仓库

PUT /_snapshot/my_backup
{
  "type": "fs",
  "settings": {
    "location": "/mount/backups/my_backup",
    "compress": true
  }
}

# 2.在源集群创建快照
PUT /_snapshot/my_backup/snapshot_1
{  
  "indices": ["index1", "index2"]
}

# 3.将快照仓库同步到目标集群

目标集群配置相同的快照仓库（如挂载同一 NFS 目录或复制快照文件）。

# 4.在目标集群恢复快照
POST /_snapshot/my_backup/snapshot_1/_restore
{
  "indices": ["index1", "index2"]
}
```

```json
# 2.查看快照仓库
GET /_snapshot/my_backup

# 3.查看快照仓库中的快照
GET /_snapshot/my_backup/snapshot_1

# 4.删除快照
DELETE /_snapshot/my_backup/snapshot_1

# 5.删除快照仓库
DELETE /_snapshot/my_backup
```
