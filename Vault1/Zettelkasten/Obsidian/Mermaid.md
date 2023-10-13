Created on date 2023-08-03 at 01:47
Status:
Tags: #mermaid

---
# Mermaid

## Flow Chart

Le possibili direzioni possono essere:
- TB - Top to bottom
- TD - Top-down/ same as top to bottom
- BT - Bottom to top
- RL - Right to left
- LR - Left to right

## Tutti i tipi di blocchi

``` mermaid
flowchart LR
	blocco1("blocco1")
	blocco2(["blocco2"])
	blocco3[["blocco3"]]
	blocco4[("blocco4")]
	blocco5(("blocco5"))
	blocco6>"blocco6"]
	blocco7{"blocco7"}
	blocco8{{"blocco8"}}
	blocco9[/"blocco9"/]
	blocco10[\"blocco10"\]
	blocco11[/"blocco11"\]
	blocco12((("blocco12")))
	
```

## Tipi di link

|      Length       |   1   |   2    |    3    |
|:-----------------:|:-----:|:------:|:-------:|
|      Normal       | `---` | `----` | `-----` |
| Normal with arrow | `-->` | `--->` | `---->` |
|       Thick       | `===` | `====` | `=====` |
| Thick with arrow  | `==>` | `===>` | `====>` |
|      Dotted       | `-.-` | `-..-` | `-...-` |
| Dotted with arrow | `-.->` | `-..->` | `-...->` |



``` mermaid
flowchart TB
    c1-->a2
    subgraph one
    a1-->a2
    end
    subgraph two
    b1-->b2
    end
    subgraph three
    c1-->c2
    end
```

## Classi

```mermaid
classDiagram
	class bankAccount
	bankAccount : String proprietario
	bankAccount : double decimale
	class client
	client : String nome
	client : int eta
	client : deposita(amount)
	client --|> bankAccount
```


## Sequence Diagram

``` mermaid
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>Bob: Hi Bob
    Bob->>Alice: Hi Alice
```

``` mermaid
sequenceDiagram
    actor Alice
    actor Bob
    Alice->>Bob: Hi Bob
    Bob->>Alice: Hi Alice
```


``` mermaid
sequenceDiagram
    Alice->John: Hello John, how are you?
    loop Every minute
        John-->Alice: Great!
    end
```

``` mermaid
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    alt is sick
        Bob->>Alice: Not so good :(
    else is well
        Bob->>Alice: Feeling fresh like a daisy
    end
    opt Extra response
        Bob->>Alice: Thanks for asking
    end
```

``` mermaid
sequenceDiagram
    par Alice to Bob
        Alice->>Bob: Hello guys!
    and Alice to John
        Alice->>John: Hello guys!
    end
    Bob-->>Alice: Hi Alice!
    John-->>Alice: Hi Alice!
```


## State Diagram


``` mermaid LR
stateDiagram-v2
    [*] --> s1
    s1 --> s2: A transition
	s2 --> [*]
```

``` mermaid
stateDiagram-v2
    state if_state <<choice>>
    [*] --> IsPositive
    IsPositive --> if_state
    if_state --> False: if n < 0
    if_state --> True : if n >= 0
```

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


## Pie Chart

Drawing a pie chart is really simple in mermaid.

- Start with `pie` keyword to begin the diagram
    - `showData` to render the actual data values after the legend text. This is **_OPTIONAL_**
- Followed by `title` keyword and its value in string to give a title to the pie-chart. This is **_OPTIONAL_**
- Followed by dataSet. Pie slices will be ordered clockwise in the same order as the labels.
    - `label` for a section in the pie diagram within `" "` quotes.
    - Followed by `:` colon as separator
    - Followed by `positive numeric value` (supported up to two decimal places)

[pie] [showData] (OPTIONAL) [title] [titlevalue] (OPTIONAL) "[datakey1]" : [dataValue1] "[datakey2]" : [dataValue2] "[datakey3]" : [dataValue3] . .

``` mermaid
%%{init: {"pie": {"textPosition": 0.5}, "themeVariables": {"pieOuterStrokeWidth": "5px"}} }%%
pie showData
    title Key elements in Product X
    "Calcium" : 42.96
    "Potassium" : 50.05
    "Magnesium" : 10.01
    "Iron" :  5
```

---
# References

[[Reference notes/Mermaid|Mermaid]]
