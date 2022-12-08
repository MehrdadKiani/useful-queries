
## Introduction
In this article, you can find a series of rules to illustrate the overview of the SSIS packages in Gitlab repositories.
Based on our policies we need to use `Mermaid` to show the charts and graphs in our documents.

Using Mermaid markup language:  
Mermaid lets you create diagrams and visualizations using text and code.
- [Mermaid documentation](https://mermaid-js.github.io/mermaid/#/)
- [Live editor](https://mermaid-js.github.io/mermaid-live-editor)

## Policies

### Diagram:
- Use Mermaid [flowchart](https://mermaid-js.github.io/mermaid/#/flowchart)


### Objects:
- In order to show a **package** you can use a `subgraph` annotation inside a flowchart diagram.
```
flowchart TB
    subgraph pre [Ecomm Transaction Preprocessing]
    end
```
- In order to show general objects like **files**, **tables**, and **notes** we should use a simple rectangle. You simply can write the object's name to create a simple rectangle.
```
flowchart LR
    file1
    table1
```
- If the name of the object has a space inside, you can write down the name inside a pair of brackets.
```
flowchart LR
    file1[file number one]
    table1
```

### Links:
Generally, for all connections and links, you can use `-->` and `---` annotations.

### Colors:
- For the background of the files and external resources, you can use the color `#FF7182`
- For the background of the tables in a database you can use the color `#34B2A7`
- For the background of the subgraph (a package), you can use the color `#F4F4F4`
- For the background of the notes, you can use the color `#FFF2CC`
- If you want to illustrate an insertion by a link in the flowchart using this color `#FF7182`
- If you want to illustrate an update by a link in the flowchart using this color `#34B2A7`. In the other case use `#000000`.
