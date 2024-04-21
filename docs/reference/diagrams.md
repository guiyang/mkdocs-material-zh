---
icon: material/graph-outline
---

# 图表 Diagrams {#diagrams}

图表有助于展示不同技术组件之间的复杂关系和互联，是项目文档的重要补充。Material for MkDocs 与 [Mermaid.js] 集成，这是一个非常流行且灵活的绘图解决方案。

  [Mermaid.js]: https://mermaid.js.org/

## 配置 {#configuration}

<!-- md:version 8.2.0 -->

此配置启用了对 [Mermaid.js] 图表的原生支持。当页面包含 `mermaid` 代码块时，Material for MkDocs 将自动初始化 JavaScript 运行时：

``` yaml
markdown_extensions:
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
```

无需进一步配置。与自定义集成相比的优点：

- [x] 与[即时加载]一起工作，无需任何额外努力
- [x] 图表自动使用在 `mkdocs.yml` 中定义的字体和颜色[^1]
- [x] 字体和颜色可以通过[额外的样式表]自定义
- [x] 支持浅色和深色配色方案 — _在本页面上试试看！_

  [^1]:
    尽管所有 [Mermaid.js] 功能应该开箱即用，Material for MkDocs 目前只会调整流程图、序列图、类图、状态图和实体关系图的字体和颜色。关于为什么当前未为所有图表实现此功能的更多信息，请参见[其他图表类型]部分。

  [即时加载]: ../setup/setting-up-navigation.md#instant-loading
  [额外的样式表]: ../customization.md#additional-css
  [其他图表类型]: #other-diagram-types

## 用法 {#usage}

### 使用流程图 {#using-flowcharts}

[流程图]是表示工作流或过程的图表。步骤作为各种节点呈现，并通过边连接，描述步骤的必要顺序：

```` markdown title="Flow chart"
``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```
````

<div class="result" markdown>

``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```

</div>

  [流程图]: https://mermaid.js.org/syntax/flowchart.html

### 使用序列图 {#using-sequence-diagrams}

[序列图]描述作为多个对象或参与者之间的顺序交互的特定场景，包括这些参与者之间交换的消息：

```` markdown title="Sequence diagram"
``` mermaid
sequenceDiagram
  autonumber
  Alice->>John: Hello John, how are you?
  loop Healthcheck
      John->>John: Fight against hypochondria
  end
  Note right of John: Rational thoughts!
  John-->>Alice: Great!
  John->>Bob: How about you?
  Bob-->>John: Jolly good!
```
````

<div class="result" markdown>

``` mermaid
sequenceDiagram
  autonumber
  Alice->>John: Hello John, how are you?
  loop Healthcheck
      John->>John: Fight against hypochondria
  end
  Note right of John: Rational thoughts!
  John-->>Alice: Great!
  John->>Bob: How about you?
  Bob-->>John: Jolly good!
```

</div>

  [序列图]: https://mermaid.js.org/syntax/sequenceDiagram.html

### 使用状态图 {#using-state-diagrams}

[状态图]是描述系统行为的绝佳工具，将其分解为有限数量的状态以及这些状态之间的转换：

```` markdown title="State diagram"
``` mermaid
stateDiagram-v2
  state fork_state <<fork>>
    [*] --> fork_state
    fork_state --> State2
    fork_state --> State3

    state join_state <<join>>
    State2 --> join_state
    State3 --> join_state
    join_state --> State4
    State4 --> [*]
```
````

<div class="result" markdown>

``` mermaid
stateDiagram-v2
  state fork_state <<fork>>
    [*] --> fork_state
    fork_state --> State2
    fork_state --> State3

    state join_state <<join>>
    State2 --> join_state
    State3 --> join_state
    join_state --> State4
    State4 --> [*]
```

</div>

  [状态图]: https://mermaid.js.org/syntax/stateDiagram.html

### 使用类图 {#using-class-diagrams}

[类图]是面向对象编程的核心，通过将实体建模为类并描述它们之间的关系来描述系统结构：

```` markdown title="Class diagram"
``` mermaid
classDiagram
  Person <|-- Student
  Person <|-- Professor
  Person : +String name
  Person : +String phoneNumber
  Person : +String emailAddress
  Person: +purchaseParkingPass()
  Address "1" <-- "0..1" Person:lives at
  class Student{
    +int studentNumber
    +int averageMark
    +isEligibleToEnrol()
    +getSeminarsTaken()
  }
  class Professor{
    +int salary
  }
  class Address{
    +String street
    +String city
    +String state
    +int postalCode
    +String country
    -validate()
    +outputAsLabel()
  }
```
````

<div class="result" markdown>

``` mermaid
classDiagram
  Person <|-- Student
  Person <|-- Professor
  Person : +String name
  Person : +String phoneNumber
  Person : +String emailAddress
  Person: +purchaseParkingPass()
  Address "1" <-- "0..1" Person:lives at
  class Student{
    +int studentNumber
    +int averageMark
    +isEligibleToEnrol()
    +getSeminarsTaken()
  }
  class Professor{
    +int salary
  }
  class Address{
    +String street
    +String city
    +String state
    +int postalCode
    +String country
    -validate()
    +outputAsLabel()
  }
```

</div>

  [类图]: https://mermaid.js.org/syntax/classDiagram.html

### 使用实体-关系图 {#using-entity-relationship-diagrams}

[实体-关系图]由实体类型组成，并指定实体之间存在的关系。它描述了特定知识领域中相互关联的事物：

```` markdown title="Entity-relationship diagram"
``` mermaid
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE-ITEM : contains
  LINE-ITEM {
    string name
    int pricePerUnit
  }
  CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
```
````

<div class="result" markdown>

``` mermaid
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE-ITEM : contains
  LINE-ITEM {
    string name
    int pricePerUnit
  }
  CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
```

</div>

  [实体-关系图]: https://mermaid.js.org/syntax/entityRelationshipDiagram.html

### 其他图表类型 {#other-diagram-types}

除了上面列出的图表类型，[Mermaid.js] 还支持[饼图]、[甘特图]、[用户旅程]、[Git图]和[需求图]，所有这些都未被 Material for MkDocs 官方支持。这些图表应该仍能按照 [Mermaid.js] 的说明正常工作，但我们认为它们不是很适合使用，主要是因为它们在移动设备上的表现不佳。

  [饼图]: https://mermaid.js.org/syntax/pie.html
  [甘特图]: https://mermaid.js.org/syntax/gantt.html
  [用户旅程]: https://mermaid.js.org/syntax/userJourney.html
  [Git图]: https://mermaid.js.org/syntax/gitgraph.html
  [需求图]: https://mermaid.js.org/syntax/requirementDiagram.html
