graph TD;
    client[Client User] -->|Uploads Audio File| A[Frontend Static Website on S3];
    A -->|API Call| B[Amazon API Gateway];
    B --> C[AWS Lambda];
    C -->|Put Object| D[S3 Upload Bucket];
    C -->|Get Parameter| E[AWS Systems Manager SSM];
    C -->|Start Transcription Job| F[Amazon Transcribe];
    F -->|Put Object| G[S3 Transcription Bucket];
    C -->|Put Item| H[Amazon DynamoDB];
    A -->|Get Object| G;
    A -->|Access| I[S3 Website Bucket];
    client -->|Accesses Website| I;

    subgraph S3
        D
        G
        I
    end