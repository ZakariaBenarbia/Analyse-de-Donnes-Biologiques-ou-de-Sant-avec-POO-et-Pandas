# Male Infertility Analysis System: Data Flow Diagram

This diagram illustrates the flow of data through the male infertility analysis system. It shows how data moves from initial upload through various processing components to final outputs.

```mermaid
flowchart TD
    %% Style definitions
    classDef process fill:#e1f5fe,stroke:#0288d1,stroke-width:2px
    classDef datastore fill:#e8f5e9,stroke:#388e3c,stroke-width:2px
    classDef external fill:#fff3e0,stroke:#ff9800,stroke-width:2px
    
    %% Nodes
    User[User] :::external
    ExcelFile[(Excel File\nMale Infertility Data)] :::datastore
    DataAnalyzer[DataAnalyzer] :::process
    DataCleaning[Data Cleaning Process] :::process
    CompositeColumns[Compute Composite Columns] :::process
    KnowledgeClustering[KnowledgeClustering] :::process
    Visualizer[Visualizer] :::process
    StatResults[Statistical Results] :::external
    VisualReports[Visual Reports] :::external
    
    %% Connections
    User -->|Upload File| DataAnalyzer
    DataAnalyzer -->|Load Data| ExcelFile
    ExcelFile -->|Raw Data| DataCleaning
    DataCleaning -->|Cleaned Data| CompositeColumns
    CompositeColumns -->|Knowledge_Score| KnowledgeClustering
    CompositeColumns -->|Age, Knowledge_Score| Visualizer
    KnowledgeClustering -->|Cluster Labels| Visualizer
    KnowledgeClustering -->|Cluster Frequencies| StatResults
    CompositeColumns -->|Descriptive Stats| StatResults
    Visualizer -->|Histograms| VisualReports
    
    %% Title
    subgraph "Data Flow Diagram: Male Infertility Analysis System"
    end
```

## Diagram Components

### External Entities (Orange)
- **User**: The person who uploads the Excel file and receives the results
- **Statistical Results**: The numerical outputs of the analysis
- **Visual Reports**: The graphical representations generated

### Data Store (Green)
- **Excel File**: The source data containing male infertility information

### Processes (Blue)
- **DataAnalyzer**: Handles loading the data from the uploaded file
- **Data Cleaning Process**: Fills missing values using median/mode
- **Compute Composite Columns**: Creates Knowledge_Score and Age_Group
- **KnowledgeClustering**: Performs KMeans clustering on Knowledge_Score
- **Visualizer**: Generates the visual representations of the data

## Data Flow Description

1. The user uploads an Excel file which is received by the DataAnalyzer.
2. The DataAnalyzer loads the data from the Excel file.
3. The raw data flows to the Data Cleaning Process where missing values are filled.
4. The cleaned data flows to the Compute Composite Columns process which calculates Knowledge_Score and Age_Group.
5. The Knowledge_Score flows to the KnowledgeClustering process, which performs clustering into three categories (Poor, Moderate, Good).
6. Both the computed scores and the cluster labels flow to the Visualizer.
7. The KnowledgeClustering sends cluster frequencies to the Statistical Results.
8. The Compute Composite Columns process sends descriptive statistics to the Statistical Results.
9. The Visualizer generates histograms which are sent to the Visual Reports.

## Implementation Details

This data flow diagram corresponds to the Python code structure with three main classes:
- **DataAnalyzer**: Handles data loading, cleaning, and feature computation
- **KnowledgeClustering**: Performs K-means clustering on Knowledge_Score
- **Visualizer**: Creates visualizations of the data and clustering results