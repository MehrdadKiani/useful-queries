
## Introduction

In this article, you can find a set of *SSIS packages* documentation writing guidelines.  

## Mermaid

It is suggested to use `Mermaid` for showing charts and graphs in any document which explains a complex logic (such as the flow of an ETL package).  

GitLab Flavored Markdown (GLFM) allows Mermaid embedding, so you create diagrams using just *plain text* inside a markdown file.  

- **Mermaid documentation**: https://mermaid-js.github.io/mermaid/
- **Local editor**: You can add an extension like `Markdown Preview Mermaid` to your VS Code to render the mermaid code. https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid

## Rules

In the table below you can find the information about the rules that we need to follow for drawing graphs


|Overview objects     |Mermaid syntax	|Evo Colors |
|---	    |---	                    |---	    |
|Packages   |`subgraph`                 |`#F4F4F4`  |
|Files 	    |File's name   	            |`#FF7182`  |
|Tables	    |Table's name   	        |`#34B2A7`  |
|Externals  |External resource's name   |`#FF7182`  |
|Database   |External resource's name   |`#FF7182`  |
|Notes      |note1`>`your text`]`       |`#FFF2CC`  |
|Links      |`-->`                      |Insert: `#FF7182` <br> Update:`#34B2A7` <br> Other cases: `#000000`|
|Connections|`---`                      |Insert: `#FF7182` <br> Update:`#34B2A7` <br> Other cases: `#000000`|
 
> **Note:**  
> In order to use these colors you can add this snippet at the end of the flowchart, you need to replace your object's name in the sections below. For example, if your file's name is `item.csv`, you can replace it with `file1`.

```text
%% Class Definitions
%% =================Files===========================
class file1 cssClass1;
classDef cssClass1 fill:#FF7182 
%% =================Tables==========================
class obj1, obj2 ssClass2;
classDef cssClass2 fill:#34B2A7   
%% =================Package=========================
class pre,common cssClass3;
classDef cssClass3 fill:#F4F4F4   
```
