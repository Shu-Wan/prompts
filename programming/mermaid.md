# Mermaid Syntax Guidelines

### 1. Handle All Text and Special Characters Correctly

This is the most common source of rendering errors.

* **Quote All Text:** Enclose any text that contains spaces, special characters, or line breaks in double quotes (`"`).
  * **Before:** `G[My Node Text]`
  * **After:** `G["My Node Text"]`
* **Use `<br>` for Line Breaks:** Do not use `\n` or actual newlines inside a node's text. The only reliable way to create a line break is with the HTML `<br>` tag *inside* the quotes.
  * **Before:** `T[task\n(dataset + model)]`
  * **After:** `T["task<br>(dataset + model)"]`
* **Escape Angle Brackets:** To display literal `<` or `>` characters (like in `<graph_id>`), you must escape them as HTML entities.
  * `&lt;` for `<`
  * `&gt;` for `>`
  * **Example:** `D["data/dataset/&lt;dataset_id&gt;"]`

### 2. Structure the Diagram Logically

A chart must be easy to understand and accurately reflect your system's design.

* **Group with Subgraphs:** Use subgraphs to visually group related components. This is crucial for distinguishing between different conceptual layers, like "on-disk artifacts" vs. "in-memory logic."
* **Represent Relationships Accurately:** Don't just connect nodes sequentially. If one component contains or orchestrates another (like a Benchmark running Tasks), place the child nodes *inside* the parent's subgraph.
* **Label Every Connection:** Always add a descriptive label to every arrow to eliminate ambiguity. This clarifies the exact relationship between the two components.
  * **Before:** `D --> T`
  * **After:** `D -- "feeds" --> T`

### 3. Keep the Code Clean and Maintainable

Well-formatted code is easier to debug and reuse.

* **Separate Definitions from Connections:** Define all your nodes and subgraphs at the top of the script. List all the connections and styling rules in separate blocks at the end. This makes the chart's structure immediately clear.
* **Use `classDef` for Styling:** Instead of applying styles inline, define reusable classes with `classDef`. This keeps your node definitions clean and makes it easy to update styles globally.
  * **Example:**

        ```mermaid
        %% Define styles at the end
        classDef artifact fill:#eee8d5,stroke:#93a1a1
        classDef concept fill:#fdf6e3,stroke:#657b83

        %% Assign styles
        class C,G,D artifact
        class R,T concept
        ```
