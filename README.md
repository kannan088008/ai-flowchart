#Steelsync-AI
'''mermaid
graph TD
    %% External Data Sources
    W_API[Weather API] --> Ext_API[External API]
    T_API[Traffic API] --> Ext_API
    S_API[Stormglass.io API] --> Ext_API
    AIS_API["AIS Hub API<br>(vessel tracking)"] --> Ext_API

    %% Historical Data Sources
    R_Avail[Rate availability] --> Hist_Data[Historical data]
    H_Cong[Historical Congestion] --> Hist_Data
    V_Voy[Vessel Voyage] --> Hist_Data
    P_Cong[Port & congestion] --> Hist_Data
    I_Evac[Inland Evacuation] --> Hist_Data

    %% Data Gathering & Feature Engineering
    Ext_API --> Data_Gather[Data Gathering]
    Hist_Data --> Data_Gather
    Data_Gather --> Pred_AI[Predictive AI]
    Feat_Eng[Feature Engineering Conversion] --> Pred_AI

    %% User Flow & Database
    Login[/Login/] <--> DB[(Database)]
    Login --> File_Up[File Upload]
    File_Up --> DB_Table[DB Table]
    
    %% Missing Details Logic Loop
    File_Up --> Miss_Det{Missing<br>Details}
    Miss_Det -- Yes --> Chat_Q[ChatBot Questions]
    Chat_Q --> MySQL[MySQL table]
    MySQL --> DB_Table
    Chat_Q -->|Loop back| Miss_Det
    Chat_Q --> Gemini[Gemini API]

    %% Routing
    Miss_Det -- No --> Router[The Router]
    Router --> Pred_AI
    Router --> Plan_AI[Planning AI]
    Router --> Gemini

    %% Core AI Processing
    Pred_AI --> Struct_Out[Structuring the Output]
    Struct_Out --> Plan_AI
    
    Plan_AI -- Rules --> Legal_Adv[Legal Advisor]
    Legal_Adv --> Plan_AI
    Legal_Adv --> Gemini

    %% System Outputs & Database Write-backs
    Gemini --> DB
    Legal_Adv --> DB
    Plan_AI --> Plans[Plans]
    Plans --> DB

    %% Plan Breakdown
    Plans --> Time_Eff[Time Efficient]
    Plans --> Bal_Cost_Time[Balanced with time & Cost]
    Plans --> Cost_Eff[Cost Efficient]

    %% Sequential Execution Block
    subgraph Execution Process
        direction TB
        Exec_Rules[Rules] --> Exec_Proc[Process]
        Exec_Proc --> Exec_Time[Time]
        Exec_Time --> Exec_Doc[Documents Required]
    end

    Time_Eff --> Exec_Rules
    Bal_Cost_Time --> Exec_Rules
    Cost_Eff --> Exec_Rules

    %% Final Tracking & Feedback
    Exec_Doc --> What_If[What If ?]
    What_If --> Live_Track[Live Tracking]
    Live_Track --> End((X))
    
    %% Main System Feedback Loop
    Live_Track -->|Feedback Loop| Pred_AI
    '''
