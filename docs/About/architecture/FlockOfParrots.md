# Flock of Parrots Concept
``` mermaid
graph TD;
  MasterParrot --> FTS1;
  MasterParrot --> FTS2;
  TAK_client_9 --> FTS2;
  TAK_client_2 --> FTS1;
  TAK_client_3 --> FTS1;
  TAK_client_1 --> FTS1;
  TAK_client_4 --> FTS2;
  TAK_client_6 --> FTS2;
  TAK_client_5 --> FTS2;
  FTS1 --> TAK_client_3;
  FTS1 --> TAK_client_2;
  FTS1 --> TAK_client_1;
  FTS2 --> TAK_client_4;
  FTS2 --> TAK_client_6;
  FTS2 --> TAK_client_5;
  FTS2 --> TAK_client_9;
```


