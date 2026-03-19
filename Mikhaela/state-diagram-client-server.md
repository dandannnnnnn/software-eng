stateDiagram-v2

    [*] --> Idle

    Idle --> RequestingPage : User opens website
    RequestingPage --> ProcessingRequest : HTTP GET request

    ProcessingRequest --> QueryDatabase : Data needed
    QueryDatabase --> ProcessingRequest : Data returned

    ProcessingRequest --> SendingResponse : HTML generated
    SendingResponse --> DisplayingPage : HTTP Response

    DisplayingPage --> Idle : User waits / next action